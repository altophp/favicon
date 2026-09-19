# Rasterizers

ALTO Favicon selects rasterizer adapters according to the source extension and
tries each available adapter until one succeeds.

## SVG pipeline

`SvgRasterizer` tries these adapters in order:

1. `rsvg-convert`.
2. Inkscape.
3. ImageMagick CLI through `magick` or `convert`.
4. The Imagick PHP extension.

The original SVG is copied to `icon.svg`, while the selected adapter produces
the PNG sizes used by the remaining output files.

## PNG pipeline

`PngRasterizer` tries the Imagick PHP extension first and GD second. PNG input
also produces 16 by 16 and 32 by 32 PNG fallbacks because there is no vector
icon to publish.

## Failure behavior

An adapter failure is logged and the next adapter is tried. Generation raises
`RasterizerUnavailableException` only when no compatible adapter completes the
requested conversion.

Applications can inject their own `RasterizerInterface` implementations into
`FaviconGenerator`:

```php
$generator = new FaviconGenerator(rasterizers: [$customRasterizer]);
```

The custom rasterizer must declare whether it supports the input file and write
the requested square PNG to the supplied destination.

## Check adapter availability

Check executables from the same environment that runs PHP; a web worker can
have a different `PATH` from a terminal. For PNG input, verify `imagick` or
`gd` appears in that runtime's `php -m` output. A present adapter can still
reject an input through its installed delegates or security policy. Inspect
the injected PSR logger's adapter errors before changing the source or adapter.
