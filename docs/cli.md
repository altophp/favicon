# CLI

The `vendor/bin/favicon` executable generates a favicon set from one required
SVG or PNG input path.

```text
vendor/bin/favicon <input> [options]
```

| Option | Default | Purpose |
| --- | --- | --- |
| `--output`, `-o` | `public` | Filesystem output directory |
| `--public-path` | `/` | URL prefix used in HTML and the manifest |
| `--app-name` | `App` | Application name used in the manifest |
| `--theme-color` | `#0b0b0b` | Browser UI and manifest theme color |
| `--background-color` | `#ffffff` | Manifest background color |
| `--manifest` | Disabled | Generate the Web App Manifest and Android icons |
| `--search-png` | Disabled | Generate the 48 by 48 Google Search PNG |
| `--force`, `-f` | Disabled | Overwrite existing generated files |

## Minimal set

```bash
vendor/bin/favicon assets/logo.svg
```

## Complete optional set

```bash
vendor/bin/favicon assets/logo.svg --manifest --search-png
```

## Custom paths and colors

```bash
vendor/bin/favicon assets/logo.svg \
    --output public/assets/favicons \
    --public-path /assets/favicons \
    --app-name "My App" \
    --theme-color "#00b7ff" \
    --background-color "#050608"
```

Colors must use six hexadecimal digits. Invalid colors fail before generation.
The command exits successfully after printing the output directory, the status
of each file, and the generated HTML snippet.

## Rerun and diagnose

Existing outputs are skipped unless `--force` is supplied. This allows a safe
rerun but does not detect that your source changed. To refresh an existing set:

```bash
vendor/bin/favicon assets/logo.svg --output public/favicons --public-path /favicons --manifest --app-name "My App" --force
```

Check input existence, a supported SVG/PNG extension, and six-digit color
values first. If rasterization fails, check [available adapters](rasterizers.md).
If writing fails, confirm the PHP process can create and write the output
directory. Filesystem paths and public URL prefixes are independent options.
