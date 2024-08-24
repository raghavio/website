---
title: "Clojox: Implementing and Optimizing Lox in Clojure"
date: 2024-08-04T18:25:48+05:30
draft: false
---


#### *This is incomplete and has been sitting in my drafts for a while. I'm publishing it for some accountability to wrap this up quickly.*

## Introduction

I recently got interested in programming language theory and embarked on an exciting journey: implementing the Lox language from Robert Nystrom's fantastic book [Crafting Interpreters](https://craftinginterpreters.com/). The book contains two parts where you implement the Lox language in two different styles. In the first part, you implement a tree-walk interpreter using all the niceties of a high-level language like Java, *jlox*. In the second part, you implement a bytecode interpreter in C, *clox*.

Lox is a dynamically typed, high-level scripting language with features like variables, control flow, functions, closures, classes and interface. It's designed to be simple enough for educational purposes, yet complex enough to demonstrate real-world language implementation challenges.

This is a tree-walk interpreter which covers the part 1 of the book. I've skipped classes and interfaces but it can easily be added.

In this post, I'll take you through my journey of creating *Clojox*, starting with a brief overview of the code, focusing on the performance challenges I faced and the optimizations I applied to speed things up.

## Implementation details


I began the implementation in Java, just like the book, but ended up doing it in a functional style in Clojure. After just writing a little bit of Java, I realized that life is too short to be willingly writing Java. Implementing it in the same language as in the book also makes it less challenging. The urge to simply copy-paste and not use your brain takes over.

Why Clojure? I knew it already, I love it — it's concise, elegant and powerful. As a Lisp dialect running on the JVM, Clojure offers Java interoperability. Which meant I could use some of the code I wrote in Java without reimplementing it. A win-win.

My implementation differs a lot from the jlox implementation in Java. It is a lot simpler codewise and doesn't have the caveats that are mentioned in the book. For example, I don't have a resolver step (Chapter 11) because my environment uses immutable persistent data structures and the resolving isn't mandatory since there's no environment leak[^1].

### Project Structure
```
clojox
├── src
│   ├── clojure <-- Contains Clojure code.
│   │   └── clojox
│   │       ├── core.clj
│   │       ├── parser.clj
│   │       ├── interpreter.clj
│   │       ├── environment.clj
│   │       ├── function.clj
│   │       ├── callable.clj
│   │       ├── native_functions.clj
│   │       ├── evaluate.clj
│   │       └── utils.clj
│   └── jlox    <-- Contains Java code.
│       ├── Scanner.java
│       ├── Lox.java
│       ├── Token.java
│       └── TokenType.java
```

Here's a high-level overview of the key components:

1. **Scanner**: I kept the Java implementation from jlox for tokenizing the source code.
2. **Parser**: Implemented in Clojure, this component takes the tokens from Scanner and produces an Abstract Syntax Tree (AST).
3. **Interpreter**: This evaluates the AST to execute the Lox program.
4. **Error messages** Handing of syntax and runtime errors.

The core of the interpreter revolves around three main concepts:

- **Environment Management**: Handling variable scopes and closures.
- **AST Evaluation**: Traversing and executing the parsed syntax tree.
- **Function Handling**: Managing function calls, returns, and closures.

### 1. Scanner

The Scanner code is written in Java and the implementation is near identical as the book. I used some of the new Java features like `record`. The scanner converts the raw source code into a sequence of tokens, which are then passed to the parser.

The tokens for the code string `var a = 10 - 20;`:

```clojure
[#object[jlox.Token "VAR var null"] #object[jlox.Token "IDENTIFIER a null"]
#object[jlox.Token "EQUAL = null"] #object[jlox.Token "NUMBER 10 10.0"]
#object[jlox.Token "MINUS - null"] #object[jlox.Token "NUMBER 20 20.0"]
#object[jlox.Token "SEMICOLON ; null"] #object[jlox.Token "EOF  null"]]
```

It is a list of `Token` objects where `Token` is a Java record:

```java
public record Token(TokenType type, String lexeme, Object literal, int line) {
    @Override
    public String toString() {
        return type + " " + lexeme + " " + literal;
    }
}
```
The object includes details like lexeme, token type, and the literal value of the token. The line number is used for error messages.

### 2. Parser

The parser takes the tokens produced by the scanner and constructs an Abstract Syntax Tree (AST).

The implementation of the recursive descent parser is similar to the book. The only change is I pass around the tokens in a functional manner. I rely heavily on destructuring and passing the remaining set of tokens to the next grammar function.

Here's a snippet showing the implementation of `print` statement:

```clojure
(defn- print-statement
  [tokens]
  (let [[[next-token & remaining :as tokens] expr] (expression tokens)]
    (when-not (match? next-token TokenType/SEMICOLON)
      (throw-error tokens "Expect ';' after value."))
    [remaining expr]))

(defn- statement
  [[token & remaining :as tokens]]
  (case (.name (.type token))
    "PRINT" (print-statement remaining)
    ...))

(defn parse
  "Takes a vector of Token class object from the Java implementation for Scanner."
  [tokens]
  (loop [tokens tokens
         statements []]
    (if (empty? tokens)
      statements
      (let [[remaining stmt] (statement tokens)]
        (recur remaining (conj statements stmt))))))
```

Each grammar rule is implemented as a separate function. Grammar function returns a list of length 2, containing a list of remaining tokens that are yet to be processed and the AST map.

### 3. Interpreter

The interpreter, the heart of the language, consists of several components. Let's take a look at them.

#### a. Environment Management

The initial implementation used a [parent-pointer-tree](https://en.wikipedia.org/wiki/Parent_pointer_tree) data structure just like the book. The difference is, in the book, the entire scope block is a mutable reference. This means if I were to update a variable, it will get reflected to statements (closures) that were executed before this update. That would make sense in dynamic scoping but not in static (lexical) scoping.

Consider this example:
```kotlin
var a = "global";
{
  fun showA() {
    print a;
  }

  showA();
  var a = "block";
  showA();
}
```

The correct output of this program should print 'global' twice. When `showA` was defined, to close over that function (closure), it needs to use the enviornment as of that point. The value of `a`, defined in the parent scope, is 'global'. Later in the code, we created a new `a` in this block. This `a` is defined in the same scope as the function `showA`. When `showA` is called again, it looks for `a` in the environment and finds this newly created `a`. This is where the bug lies. This happens because the entire scope block is a mutable reference and an update to it will get reflected everywhere.

![Looking up the a variable in the environment tree.](/clojox/environment-5.png "Picture taken from the Crafting Interpreters book.")

The book solves this issue by adding a resolver step. The resolver step, comes between parsing and interpretation, statically determines the scope and binding of each variable, eliminating runtime lookups.

I took a different approach. To implement proper lexical scoping, I have used a combination of immutable persistent maps and Clojure atoms for value referencing. Here, each environment value is a reference instead of the entire scope block. Consider the below example and the environment value added as comment next to it.

```javascript
var a = 2; // Env {:bindings {clock #atom[...$reify__320], a #atom[2.0]}, :parent nil}
print a; => 2
{
    var b = 10; // Env {:bindings {b #atom[10.0]}, :parent {:bindings {clock #atom[...$reify__320], a #atom[2.0]}, :parent nil}}
    print a + b; => 12
    // Updating the `a` variable in the parent scope.
    a = 10; // Env {:bindings {b #atom[10.0]}, :parent {:bindings {clock #atom[...$reify__320], a #atom[2.0]}, :parent nil}}
}
print a; => 10
```

Here is how the lookup function for an environment value works. Since it's nested, it traverses the scope until the value is found, or raises an exception.
```clojure
(defn lookup
  [env identifier]
  (if env
    (if-let [val (get (:bindings env) (.lexeme identifier))]
      @val
      (recur (:parent env) identifier)) ;; Search the parent scope if value not present.
    (throw (ex-info (str "Undefined variable '" (.lexeme identifier) "'.")
                    {:token identifier}))))
```

Stay tuned because we are going to make the environment handling a lot simpler (which seems obvious in the hindsight) in the optimization section.

#### b. Function Handling

Functions consists of 3 parts. Function definition, calling the function and the environment as of function definition (closure).
I created a protocol to define callable objects. This can be used for functions, classes and interfaces.

```clojure
(defprotocol ClojoxCallable
  (call [this arguments])
  (arity [this])
  (to-string [this]))
```

We implement the above protocol for user-defined functions:

```clojure
(defrecord Function [fn-ast closure]
  ClojoxCallable
  (call [_ arguments]
    ;; Function call implementation
    )
  (arity [_]
    (count (:params fn-ast)))
  (to-string [_]
    (str "<fn " (.lexeme (:identifier fn-ast)) ">")))
```

#### c. Native Functions

This is to implement built-in functions for Lox, such as `clock()`, by again implementing the `ClojoxCallable` protocol. The `reify` macro is used to create an anonymous implementation of our protocol. 
```clojure
(def clock
  (reify ClojoxCallable
    (call [_ _arguments]
      (/ (System/currentTimeMillis) 1000.0))
    (arity [_] 0)
    (to-string [_] "<native fn>")))
```


#### d. Core Evaluation Logic

Clojure has stellar support for expression problem. Instead of visitor pattern, there's multimethods and Protocols. I initially started with multimethods for interpreting the ASTs.

>Clojure supports sophisticated runtime polymorphism through a multimethod system that supports dispatching on types, values, attributes and metadata of, and relationships between, one or more arguments.

In our case, the `evaluate` multimethod dispatches based on the AST node type:

Here's an example of the interpretation of the `print` statement:

``` clojure
(defmulti evaluate (fn [ast _env] (:type ast)))

(defmethod evaluate :print
  [{:keys [expression]} env]
  (let [[value env] (evaluate expression env)]
    (println (stringify value))
    [nil env]))

(defn interpret
  "Loop over and evaluate all the AST nodes received from the parser.
  Returns the error code 70 to signify the runetime error."
  [statements]
  (try
    (loop [statements statements
           env (environment/create nil {"clock" (atom native-functions/clock)})]
      (if (empty? statements)
        nil
        (let [[_evaluated-expr env] (evaluate (first statements) env)]
          (recur (rest statements) env))))
    (catch clojure.lang.ExceptionInfo e
      (utils/error (ex-message e) (.line (:token (ex-data e))))
      70 ;; Exit code for runtime error.
      )))
```

The dispatch function returns a list containing the value returned (`nil` for the print method) and the environment map.

### Grammar addition

Because of the way we implemented our environment, we broke mutual recursion. Consider this code example:

```kotlin
fun isOdd(n) {
  if (n == 0) return false;
  return isEven(n - 1);
}

fun isEven(n) {
  if (n == 0) return true;
  return isOdd(n - 1);
}
```

The `isEven()` function isn't defined yet when we are looking at the body of `isOdd()` where it's called. If we define `isEven()` before, same problem persists. This form of recursion is called mutual recursion. This might seem a fuckall way to find if a number is even or odd, and it is too, but mutual recursion is fundamental to functional programming. It is heavily used in recursive descent parsers, the same kind we have used for this language.

Why does this not work for our implementation? 

Because our environment is an immutable map. `isOdd()`'s closure does not contain any reference to `isEven`, it won't get reflected there even if it gets defined later. A closure is a set of symbols in an environment that closes over a function. [No, it doesn't mean a function that contains another function](https://stackoverflow.com/a/36878651).

Okay, how to solve for it then? It's crucial so we've got to figure something out.

I took inspiration from how [Clojure handles it](https://clojuredocs.org/clojure.core/declare) by making *forward declarations* and added a `declare` keyword. You declare the name before it's fully defined.

```kotlin
declare isEven;

fun isOdd(n) {
...
```

By doing this, we have defined `isEven` in outer scope and it is now part of `isOdd()`'s closure. This is how the environment will look now at the time `isOdd` is defined. The value of it is `nil`, but that's all right.

```clojure
{:bindings {clock #atom[...$reify__320], isEven #atom[nil]}, :parent nil}
```

Once we define the `isEven` function. Its value gets re-assigned and the earlier environment gets updated to this.

```clojure
{:bindings {clock #atom[...$reify__320], isEven #atom[#clojox.function.Function{...}]}, :parent nil}
```

It wasn't necessary to add a new syntax for this declaration. We are simply creating an empty variable. We could've also done

``` kotlin
var isEven;
```

But, why not ¯\_(ツ)_/¯.

### Main Entry Point

This file ties everything together, providing the main entry point for the interpreter:

```clojure
(defn run [source]
  (let [scanner (Scanner. source)
        tokens (.scanTokens scanner)
        ast (parse tokens)]
    (interpret ast)))
```

This structure allows Clojox to read Lox source code, tokenize it using the Java scanner, parse it into an AST, and then interpret that AST to execute the program.

The initial implementation, while functional, had significant performance issues. These issues set the stage for the optimization journey, which we'll explore in the following sections.

## Performance Challenges

With the initial implementation complete, I was excited to run some benchmarks. I chose to calculate the 33rd Fibonacci number as my test case, as it's computationally intensive enough to reveal performance issues.

```kotlin
fun fib(n) {
  if (n < 2) return n;
  return fib(n - 1) + fib(n - 2);
}
var before = clock();
print fib(33);
print clock() - before;
```

The results were...sobering:

- jlox (the Java implementation from the book): 2.5 seconds
- Clojox: 21 minutes

Clearly, something was terribly wrong with my implementation. It was time to dive into optimizations.

## Optimization Journey

It was time to profile the code. I'm using [clj-async-profiler](https://github.com/clojure-goes-fast/clj-async-profiler) to create a Flame Graph. The graphs are interactive and embedded in this page via iframe.

<iframe src="/clojox/pre_optimizations_og.html?hide-sidebar=true" style="height:558px;width:100%"></iframe>

This is not very helpful as is. Let's make some adjustments. We will collapse the recursive steps, remove the JVM Garbage Collection stuff you see on the right side, and reverse it to highlight the functions with the highest self time.

<iframe src="/clojox/pre_optimizations.html?hide-sidebar=true" style="height:558px;width:100%"></iframe>

This is much better. Let's dig in.

### Disabling JVM stacktrace

I see a lot of things that I didn't directly write in my Clojure code. You can see Stacktraces, Throwable and other JVM related stuff that I'm clueless about. I figured this is related to my `return` statement implementation. To return from a function, we raise an exception to exit the code block and pass control to the outside body.

I ignored a step in the book that talks about implementing a custom exception class to implementing the `return`.

```java
public class Return extends RuntimeException {
    public final Object value;

    public Return(Object value) {
        super(null, null, false, false); // Disable stacktrace and other functionality.
        this.value = value;
    }
}
```

Here, we are creating custom exception class to be able to raise an exception with no message, no cause, suppression disabled and stack trace disabled.

and change the code to use our new class instead of ex-info.

```diff
(defmethod evaluate :return
  [{:keys [expr]} env]
  (let [[return-value env] (when expr
                             (evaluate expr env))]
- (throw (ex-info nil {:return-value return-value :env env}))))
+ (throw (Return. return-value))))
```

<iframe src="/clojox/after_jvm_stacktraces.html?hide-sidebar=true" style="height:638px;width:100%"></iframe>

All the yellow JVM stuff has gone from the graph now. After this trivial change, the execution time got reduced to 172.3 seconds from 1260 seconds. That's massive improvement. Still slow though.

### Switching to Protocols

We use multimethods in our interpreter to dispatch based on AST type. Clojure also offers a faster form of polymorphism with Protocols. Protocols are like interfaces in other languages. They dispatch only based on the type of the first argument, which is faster than runtime dispatch of multimethods.

Since we are only working with types, we can switch to Protocols for better performance.

```clojure
(defprotocol Evaluate
  (evaluate [this env])
)
(defrecord Print [expression]
  protocols/Evaluate
  (evaluate [_ env]
    (let [[value env] (evaluate expression env)]
      (println (stringify value))
      [nil env])))
```

After this change, the program now takes 135.75 seconds.

### Resolving reflections

We use the Token java class throughout in the codebase. However, we didn't add any type hints and hence the flamegraph shows most of the time is spend in resolving reflections. // explain what reflections mean and why it's slow.

we add type hints whereever we used the Token class.
```diff
// Code to check if the token is keyword 'or'.
-(if (= (.type op) TokenType/OR)
+(if (= (.type ^Token op) TokenType/OR)
```

<iframe src="/clojox/reflections.html?hide-sidebar=true" style="height:494px;width:100%"></iframe>

The time has now come down to 19.79 seconds. All the `java.lang.reflect` functions are gone now. Not bad. Running the benchmark doesn't warrant a quick insta doom scroll session anymore.

If you notice, I've highlighted the env lookup function. We are going to fix that next.

### Flattening the Environment

You've seen the nested environment implementation above. After using references as values along with persistent data structures, turns out the nesting isn't required and we can simply flatten our environment.

The lookup function which earlier used to use a loop can now simply do an O(1) fetch.

```clojure
(defn lookup
  [env identifier]
  (if-let [val (get env (.lexeme ^Token identifier))]
    @val
    (throw (ex-info (str "Undefined variable '" (.lexeme ^Token identifier) "'.")
                    {:token identifier}))))
```


Considering the example we saw earlier, this is how the environment values look like now:

```javascript
var a = 2; // Env {clock #atom[...$reify__331], a #atom[2.0]}
print a; => 2
{
    var b = 10; // Env {clock #atom[...$reify__331], a #atom[2.0], b #atom[10.0]}
    print a + b; => 12
    // Updating the `a` variable in the parent scope.
    a = 10; // Env {clock #atom[...$reify__331], a #atom[10.0], b #atom[10.0]}
} // Env {clock #atom[...$reify__331], a #atom[10.0]}
print a; => 10
```

<iframe src="/clojox/flat_env.html?hide-sidebar=true" style="height:494px;width:100%"></iframe>

The highlighted function from the last graph has now moved from the second spot to further down.

The program now takes 11.3 seconds to execute.

### Function call improvements

<iframe src="/clojox/flat_env_reduce_highlight.html?hide-sidebar=true" style="height:494px;width:100%"></iframe>

Here's the function call code to create new env from the closure (parent env) and function arguments.

```clojure
(call [this args]
  (let [params-vals (map vector params args)
        env (reduce (fn [env [param arg]]
                      (environment/define env param arg))
                    closure
                    params-vals)]
        ...))
```
I slightly changed the above code to avoid the computation of adjoined `params-value` and instead send a range to my reduce function.

```clojure
(call [this args]
  (let [env (reduce (fn [env i]
                      (environment/define env (nth params i) (nth args i)))
                    closure
                    (range (count params)))]
        ...))
```

<iframe src="/clojox/reduce_improved_2.html?hide-sidebar=true" style="height:494px;width:100%"></iframe>

As we can see, the reduce function that earlier took 31.41% of time, is now reduced to 9.39%. I can't seem to figure out why such a small change would impact this drastically. I generated these flamegraphs twice and the results were the same. I'll take it though. The program time has not come down to 10.2 seconds.

// add a conclusion to this optimization journey.

## Conclusion

