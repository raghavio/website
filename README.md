# Website

## Per-post appearance

Keep the shared `mi-casa` templates. Existing posts retain their appearance;
no extra styles load unless an individual post opts in. Remove the fields below
to return to the default. `post_theme: default` explicitly selects the default.

Select the included example in a post's YAML front matter:

```yaml
post_theme: paper
```

Reusable themes live in `assets/css/post-themes/<name>.css`. Copy `paper.css`
to create another. Names use lowercase letters, digits, and hyphens.

For a completely individual design, use a Hugo page bundle:

```text
content/posts/my-post/
  index.md
  style.css
  sidebar.webp
```

In `index.md` front matter, add:

```yaml
post_theme: paper      # optional starting point
post_css: style.css    # loaded last, only on this post
```

Example `style.css`:

```css
:root {
  --post-sidebar-image: url("/posts/my-post/sidebar.webp");
  --post-sidebar-background: #292521;
  --post-sidebar-size: cover;
  --post-sidebar-repeat: no-repeat;
  --post-sidebar-position: center;
  --post-sidebar-color: white;
  --post-nav-highlight: #69553b;
  --post-page-background: #fff8eb;
  --post-background: #fff8eb;
  --post-color: #302b24;
  --post-link-color: #805522;
  --post-font: Georgia, serif;
  --post-heading-font: "Space Grotesk", sans-serif;
  --post-max-width: 48em;
  --post-margin-left: 0;
  --post-margin-right: auto;
  --post-text-align: left;
}
```

The article currently has centered **margins**, while its text is already
left-aligned. The margin variables move the entire article to the left; text
alignment is independent. Existing mobile layout rules remain in effect.
Use `--post-sidebar-image: none` for a solid sidebar color.

CSS can also contain arbitrary selectors and media queries for more extensive
designs. The adapter's available variables and defaults are in
`assets/css/post-theme.css`. Fonts must exist on the device or be loaded via
`@font-face` in your CSS; setting a family name does not download a font.
Use root-relative image/font URLs (as above), since stylesheets have their own
URLs. Images in `static/pictures/` are available at `/pictures/...`.

For existing standalone `content/posts/name.md` files, store CSS in
`assets/css/posts/name.css` and set `post_css: css/posts/name.css`; converting
to a bundle is optional. Bundle resources take priority over shared assets.
Styles are fingerprinted for cache invalidation. Unknown themes or missing
stylesheets fail the build. The options apply only to individual posts, never
the homepage, post listing, books, or about pages.
