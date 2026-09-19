# Alto Favicon

Alto Favicon generates a focused modern favicon set and its HTML integration
snippet from one SVG or PNG source. It preserves an SVG source for modern
browsers and selects an available rasterizer for the required bitmap outputs.

The default set contains the browser icon, Apple touch icon, HTML snippet, and
either the original SVG or PNG fallbacks. Web App Manifest, Android, maskable,
and search icons are opt-in.

![Generated Apple touch icon from the example source](assets/example/generated/apple-touch-icon.png)

## Documentation

- [Installation](installation.md): install the package and a compatible rasterizer.
- [Getting started](getting-started.md): generate, publish, and use a first favicon set.
- [CLI](cli.md): run the generator and inspect created or skipped files.
- [PHP](php.md): build options, generate files, and read the result report.
- [Configuration](configuration.md): choose paths, colors, optional files, and overwrite behavior.
- [Rasterizers](rasterizers.md): understand SVG and PNG adapter selection and failures.
- [Files](files.md): compare default and optional generated outputs.
- [Errors](errors.md): handle invalid input and unavailable rasterization.

## Boundaries

The package generates static files; the application remains responsible for
serving them from the configured public path and adding the generated tags to
the document head. Rasterizer availability depends on the PHP runtime and
installed executables on the machine performing generation.
