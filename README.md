# markmap

Visualize your Markdown as mindmaps.

This project is heavily inspired by [dundalek's markmap](https://github.com/dundalek/markmap).

👉 [Try it out](https://markmap.js.org/repl).

👉 [Read the documentation](https://markmap.js.org/docs) for more detail.

## Packages

- [markmap-lib](https://github.com/gera2ld/markmap/tree/master/packages/markmap-lib)

  Transform Markdown to data used by markmap.

- [markmap-view](https://github.com/gera2ld/markmap/tree/master/packages/markmap-view)

  Render markmap in browser.

- [markmap-cli](https://github.com/gera2ld/markmap/tree/master/packages/markmap-cli)

  Use markmap in command-line.

- [coc-markmap](https://github.com/gera2ld/markmap/tree/master/packages/coc-markmap)

  Use with [coc.nvim](https://github.com/neoclide/coc.nvim) in Vim / Neovim, creating markmaps from your text buffer.

## Related

- Markmap for VSCode: <https://marketplace.visualstudio.com/items?itemName=gera2ld.markmap-vscode>

## Usage

### Transform

Transform Markdown to markmap data:

```js
import { transform, getUsedAssets, getAssets } from 'markmap-lib';

// 1. transform markdown
const { root, features } = transform(markdown);

// 2. get assets
// either get assets required by used features
const { styles, scripts } = getUsedAssets(features);
// or get all possible assets that could be used later
const { styles, scripts } = getAssets();
```

Now we are ready for rendering a markmap in browser.

### Render

Create an SVG element with explicit width and height:

```html
<script src="https://cdn.jsdelivr.net/npm/d3@5"></script>
<script src="https://cdn.jsdelivr.net/npm/markmap-view"></script>

<svg id="markmap" style="width: 800px; height: 800px"></svg>
```

Render a markmap to the SVG element:

```js
// We got { root } data from transforming, and possible extraneous assets { styles, scripts }.

const { Markmap, loadCSS, loadJS } = window.markmap;

// 1. load assets
if (styles) loadCSS(styles);
if (scripts) loadJS(scripts, { getMarkmap: () => window.markmap });

// 2. create markmap

Markmap.create('#markmap', null, root);

// or pass an SVG element directly
const svgEl = document.querySelector('#markmap');
Markmap.create(svgEl, null, data);
```
