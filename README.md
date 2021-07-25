# Dark-mode-sensitive SVG in GitHub markdown tests

### Inlined `<img src="test.svg">` does not work

<img src="test.svg">

### Inlined `<svg>` does not work

<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 100 100" style="background: transparent">
  <style>
    /* assume light theme by default and use black ink */
    circle { fill: #000; }
    /* if dark theme is detected, override with dark-mode styles and use light ink */
    @media (prefers-color-scheme: dark) { circle { fill: #eee; } }

    /* The above doesn't work. How about if we try the following? */
    html[data-color-mode="dark"] circle { fill: #acf; }
    /* This is based on GitHub's html, which looks like the following (simplified):
        〈html data-color-mode="dark"〉〈img src="this.svg"〉...
    This assumes that this CSS-in-SVG can use a selector that matches
    an ancestor element in the containing document and then traverses
    into the contained SVG document to match a descendant element,
    but this doesn't work either. */
  </style>
  <circle cx="50" cy="50" r="50"/>
</svg>
<!-- Can you embed svg elements with no internal style elements? -->
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 100 100" style="background: transparent">
  <circle cx="50" cy="50" r="50"/>
</svg>
