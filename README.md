# ScaleIT Platform Documentation

Welcome to the ScaleIT platform!

* For the full documentation of ScaleIT, visit: http://scaleit-platform-documentation.readthedocs.io

* In order to setup your own instance of the ScaleIT platform, visit: https://github.com/ScaleIT-Org/spcm-rancher-server

* If you wish to create your own App, visit: https://github.com/ScaleIT-Org/documentation/blob/master/source/appguideline_en.md

* If you wish to analyse your requirements regarding Apps, visit our ScaleIT App Workshop Kit: https://github.com/ScaleIT-Org/workshop-app-prototyping

# Development

You may check out this repository and use the sphinx tools.

Run `sphinx-autobuild source/ build/html/` to compile and locally host the documentation. Note that you need sphinx installed.

For working with the project, go over to http://docs.readthedocs.io/en/latest/getting_started.html and follow the instructions.

## Localization/Translation

This project uses the sphinx-intl toolset as per [read the docs translation documentation](https://docs.readthedocs.io/en/latest/guides/manage-translations.html).

To help with the translation, we use the open source platform [Zanata](http://zanata.org/) using [this guide](https://jareddillard.com/blog/documentation-internationalization-using-sphinx-and-zanata.html).

## SVG Graphics 

### Background

SVG Code (add fill-opacity and change the class of the first path). This may vary according to how the SVG was built. We used PowerPoint PDF export + [IdrSolutions Online Conversion](https://www.idrsolutions.com/online-pdf-to-svg-converter/)

```
...
]]></style>

</defs>
<path d="M0,0 L0,695 L1431,695 L1431,0 Z " fill="#FFFFFF" fill-opacity="0" stroke="none"/>
<path d="M0,0H1431.5V695.1H0Z" class="g0_1x"/>
```

CSS (the class may be used elsewhere, rename). Don't forget, styles cascade.

```
.g0_1x{
    fill-opacity: 0;
}
```

----

The ScaleIT project was funded by the German Federal Ministry of Education and Research (BMBF) in the program "Innovations for Production, Service and the Work of Tomorrow" (02P14B180ff) and managed by the lead partner Karlsruhe PTKA. Responsibility for the content of this publication lies with the authors.

MIT License, Copyright 2017 Andrei Miclaus
