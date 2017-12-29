# Contribution to the ScaleIT Platform Documentation

## Adding Custom Fonts 

Some SVG files for example require special fonts. Sphinx creates automatically creates a `/build/html/_static/fonts` and `/build/html/_static/fonts` directory where it copies the referenced images and the fonts located in `/source/_static/fonts`.

Links to special embeded fonts inside the SVG need to point to the proper location:

```css
@font-face {
    font-family: ArialMT_9;
    src: url("/_static/fonts/ArialMT_9.woff") format("woff");
}
```

## Adding SVGs with Transparent Background

Some SVG files have a `fill` property set to certain color. In order to blend in with the rest of the documentation, the fill must be set to `none`.

```xml
</defs>
<path d="M0,0
L0,239
L1376,239
L1376,0 Z " 
fill="none" stroke="none" />
<path d="M0,239.9l1376.5,0L1376.5,0L0,0L0,239.9Z" class="g1_1" />
```