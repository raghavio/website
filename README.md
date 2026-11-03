# Website

Use Hugo **0.169.0** (standard or extended). The version is pinned in
`mise.toml` and `.hugo-version`. With [mise](https://mise.jdx.dev/) installed:

```sh
mise install
mise exec -- hugo server
mise exec -- hugo
```

Alternatively install that Hugo release and run `hugo` directly. Check
`hugo version`: a version file alone does not upgrade a system installation.

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

## Hugo upgrade and deployment

The upgrade from 0.129.0 to 0.169.0 includes the current layout directory names
(`_partials`, top-level base/single/list templates, `home.html`, and `_markup`)
and replaces deprecated `languageCode` with `locale`.

Local comparisons against 0.129.0 preserved all 66 output paths, body text and
link/image/anchor targets across all 28 HTML files, static files, and RSS/sitemap
URLs. Hugo's newer automatic summary generation changes some social metadata
and RSS descriptions. Updated syntax highlighting also changes some spans and
adds a WebKit text-sizing declaration. These are not byte-identical builds.
Browser spot checks covered the main pages and default/custom post styles at
desktop and mobile widths. All 19 sitemap pages and 29 referenced local assets
returned HTTP 200. Live deployment verification has not been performed.

For Cloudflare Pages, set **HUGO_VERSION=0.169.0** in both production and preview
build environments, keep the existing `hugo` build command and output
directory `public`. These dashboard settings are separate from this repository;
the version files do not configure Cloudflare automatically. Review a preview
deployment before promoting it. Keep the previous deployment for rollback.

One-time checks using temporary posts verified default styling, named themes,
overrides, isolation, and missing-file failures. No additional CI workflow or
test step is required.
