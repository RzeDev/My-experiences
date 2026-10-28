```css
/* Persian RTL support for Obsidian */

/* Reading view: Persian text */
.markdown-preview-view p,
.markdown-preview-view li,
.markdown-preview-view blockquote,
.markdown-preview-view h1,
.markdown-preview-view h2,
.markdown-preview-view h3,
.markdown-preview-view h4,
.markdown-preview-view td,
.markdown-preview-view th {
    direction: rtl;
    unicode-bidi: normal;
    text-align: right;
}

/* Editing view: Persian text */
.markdown-source-view.mod-cm6 .cm-line {
    direction: rtl;
    unicode-bidi: normal;
    text-align: right;
}

/* Inline code and technical expressions */
.markdown-preview-view code,
.markdown-source-view.mod-cm6 .cm-inline-code {
    direction: ltr;
    unicode-bidi: isolate;
}

/* Code blocks */
.markdown-preview-view pre,
.markdown-preview-view pre code,
.markdown-source-view.mod-cm6 .HyperMD-codeblock {
    direction: ltr;
    unicode-bidi: isolate;
    text-align: left;
}
