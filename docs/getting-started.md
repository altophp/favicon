# Getting started

Generate a favicon set, publish its files, and connect them to a page. Follow
[Installation](installation.md) first; SVG input needs one of the documented
rasterizers. Download the [example SVG](https://raw.githubusercontent.com/altophp/favicon/main/docs/assets/example/source.svg) as
`assets/logo.svg`, creating `assets/` if needed. This original illustration is
provided under the repository's MIT license.

From your Composer project root, run:

```bash
vendor/bin/favicon assets/logo.svg --output public/favicons --public-path /favicons
```

`public/favicons` is the filesystem destination; `/favicons` is the URL where
your web server exposes it. The generator creates the destination directory.
The first run reports these files as created:

| File | Result |
| --- | --- |
| `icon.svg` | created |
| `favicon.ico` | created |
| `apple-touch-icon.png` | created |
| `favicon.html` | created |

| Source | Actual 180 x 180 Apple icon |
| --- | --- |
| ![Example white letter A on a dark teal square](assets/example/source.svg) | ![Generated Apple touch icon](assets/example/generated/apple-touch-icon.png) |

The report also prints this HTML, saved in `favicon.html`:

```html
<link rel="icon" href="/favicons/favicon.ico" sizes="32x32">
<link rel="icon" href="/favicons/icon.svg" type="image/svg+xml">
<link rel="apple-touch-icon" href="/favicons/apple-touch-icon.png">
<meta name="theme-color" content="#0b0b0b">
```

Copy those tags into your page's `<head>` and expose `public/` as your server's
web root. Open the page to see the icon in its browser tab. The repository's
[generated preview](https://altophp.com/favicon/assets/example/preview.html) uses the same files with
relative URLs so `docs/assets/example/preview.html` also opens directly from a
checkout. The hosted preview is available once these documentation assets
are published.

## Run it again

Existing files are reported as `skipped`, not as failures. After changing the
source or options, rerun with `--force` to replace the generated files. Check
that the output directory is writable if creation fails.

For manifest and search icons, continue with [CLI](cli.md) or [PHP](php.md).
[Files](files.md) lists the different SVG and PNG output
sets. [Rasterizers](rasterizers.md) explains how to recover when no adapter
can process your input.
