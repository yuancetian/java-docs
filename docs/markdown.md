# Markdown configuration

**docsify** uses [marked](https://github.com/markedjs/marked) as its Markdown parser. You can customize how it renders your Markdown content to HTML by customizing `renderer`:

```js
window.$docsify = {
  markdown: {
    smartypants: true,
    renderer: {
      link() {
        // ...
      },
    },
  },
};
```

?> Configuration Options Reference: [marked documentation](https://marked.js.org/#/USING_ADVANCED.md)

You can completely customize the parsing rules.

```js
window.$docsify = {
  markdown(marked, renderer) {
    // ...

    return marked;
  },
};
```

## Supports mermaid

```js
// Import mermaid
//  <link rel="stylesheet" href="//cdn.jsdelivr.net/npm/mermaid/dist/mermaid.min.css">
//  <script src="//cdn.jsdelivr.net/npm/mermaid/dist/mermaid.min.js"></script>

let num = 0;
mermaid.initialize({ startOnLoad: false });

window.$docsify = {
  markdown: {
    renderer: {
      code(code, lang) {
        if (lang === 'mermaid') {
          return /* html */ `
            <div class="mermaid">${mermaid.render(
              'mermaid-svg-' + num++,
              code,
            )}</div>
          `;
        }
        return this.origin.code.apply(this, arguments);
      },
    },
  },
};
```
