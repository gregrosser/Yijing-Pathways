# dvisvgm howto

Converting a PDF to SVG with `dvisvgm`, for pulling diagram assets into
Inkscape/Blender for this project.

## Basic conversion

```
dvisvgm --pdf input.pdf -o output.svg
```

Requires a `dvisvgm` build with PDF support (linked against `libpoppler`).
Check with:

```
dvisvgm --version
```
— look for "with PDF support" (or similar) in the output. Most distro
packages and TeX Live's bundled version have this.

## Multi-page PDFs

By default only page 1 converts. To pick a page or range:

```
dvisvgm --pdf --page=2 input.pdf -o output.svg
dvisvgm --pdf --page=1-3 input.pdf -o output-%p.svg
```

`%p` in the output filename is replaced by the page number when converting
multiple pages.

## Font/text handling

Affects whether individual glyphs come out as separately editable path
outlines in Inkscape, vs. `<text>`/`<use>` elements referencing `<defs>`
glyphs (harder to select/edit per-letter):

```
dvisvgm --pdf --no-fonts input.pdf -o output.svg   # glyphs as path outlines
dvisvgm --pdf --font-format=woff input.pdf -o output.svg   # embedded webfont
```

Use `--no-fonts` if you need to individually select/edit letterforms as
shapes in Inkscape.

## Trimming whitespace

```
dvisvgm --pdf --bbox=min input.pdf -o output.svg     # tight crop to content
dvisvgm --pdf --bbox=papersize input.pdf -o output.svg
```

## If PDF support isn't compiled in

Fall back to a dedicated PDF→SVG tool instead, e.g. `pdf2svg` or
`inkscape --pdf-poppler ...`.
