# Funarchy assets

- `index.html` — exact static key art with a clickable GitHub lockup.
- `parallax.html` — six-layer cursor/touch autonomous parallax implementation.
- `keyart-1920x1080.png` — approved full 16:9 key art.
- `layers.json` — layer order and depth manifest; names each layer by
  extensionless base, with the served format preference order.

Both HTML files are dependency-free and can be opened directly or served as static files.

## Image formats

The PNGs are the archival masters. Each also ships as AVIF and WebP, and
both pages request those through `<picture>`, falling back to PNG only on
browsers that support neither. AVIF is encoded at 4:4:4 chroma so the
hairline strokes and small type stay clean.

Regenerating after an art change (`avifenc` from libavif, `cwebp` from
webp):

    avifenc -q 78 -y 444 -s 4 keyart-1920x1080.png keyart-1920x1080.avif
    cwebp -q 90 -m 6 -sharp_yuv keyart-1920x1080.png -o keyart-1920x1080.webp

    # layers carry alpha
    avifenc -q 72 -y 444 -s 5 --qalpha 90 layer-N.png layer-N.avif
    cwebp -q 88 -m 6 -sharp_yuv -alpha_q 100 layer-N.png -o layer-N.webp

The banner is uploaded to platforms that want PNG, so its master is also
kept losslessly optimized (`oxipng -o max --strip safe`) alongside AVIF
and WebP copies for embedding on the web.

## License

This repository holds two kinds of work, licensed separately.

**Code — [MIT](LICENSE).** `index.html`, `parallax.html`, `layers.json`.
Take the parallax implementation and use it for anything.

**Artwork and brand assets — [CC BY-SA 4.0](LICENSE-ART).**
The key art, banner, parallax layers, wordmark, glyph, and icons, in
every format they ship in (`.png`, `.avif`, `.webp`, `.svg`). Remix and
redistribute freely, with attribution, sharing derivative artwork under
the same terms.

**The Funarchy name and marks.** The licenses above cover copyright in
these files, not the use of the name "Funarchy" to identify a project.
Forks and derivatives are welcome — the charter celebrates them — but
please don't present your fork as being Funarchy itself.

The `wordmark.svg` glyphs are converted to paths and no font files are
vendored here, so this repository carries no font license obligations.
See [FONTS.md](FONTS.md) for the source family.
