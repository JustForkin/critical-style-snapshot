## Critical Style Snapshot

<p align="center">
    <img width="440" src="/src/promotional.png?raw=true" text-align="center">
</p>

Capture CSS above the fold with one click. Works for most websites, this extension captures 99% of the of the currently active media query CSS. Selectors like pseudo-elements don't get captured (yet), so in some cases minor tweaking is nessescary.

Inspired by [CriticalCSS Bookmarklet and Devtool Snippetjs](https://gist.github.com/PaulKinlan/6284142)

## Features
- Capture your webpage above the fold CSS with one click
- Copy the CSS with one extra click
- Preview the captured CSS

## Installation
No setup required, [Install it directly from the Chrome Webstore](https://chrome.google.com/webstore/detail/critical-snapshot/gkoeffcejdhhojognlonafnijfkcepob)

## Usage
Resize your browser window to the desired device width and click the capture icon ![icon](/src/icon19.png "icon") in your chome extensions bar. Copy the outputted style, then paste it in a style element just before the first `<link rel="stylesheet" href="style.css" ../>` element. This way your project CSS will override the "above the fold" CSS when it is loaded.

Example:
```
<style>
    ..output css
</style>
`<link rel="stylesheet" href="style.css" ../>`
```

### @media queries

This plugin only outputs CSS that is **currently active**, meaning you have full control over the media specific styles you capture by resizing your browser window.

Example:
```
<style>
    ..mobile screen output css
    
    @media screen and (min-width: 768px) {
        ..tablet screen output css    
    }
    
    @media screen and (min-width: 1024px) {
        ..desktop screen output css
    }
    
    ..etc
</style>
`<link rel="stylesheet" href="style.css" ../>`
```

### Optimization
As you might guess, the plugin does not (yet) optimize the CSS, meaning every time you capture the CSS for a specific media query, you will (most likely) get some CSS that is already captured for smaller screens double. For this I recommend you run all your "above the fold" CSS through some CSS optimizers.

[PostCSS](https://github.com/postcss/postcss)
>PostCSS is a tool for transforming styles with JS plugins. These plugins can lint your CSS, support variables and mixins, transpile future CSS syntax, inline images, and more.

[PostCSS Merge Selectors](https://github.com/georgeadamson/postcss-merge-selectors) **Get rid of (most) duplicate selectors and rules**
>PostCSS plugin to combine selectors that have identical rules. Can be configured to only merge rules who's selectors match specific filters.

[Autoprefixer](https://github.com/postcss/autoprefixer) **Autoprefixing to make your above the fold CSS compatible with most browsers**
>PostCSS plugin to parse CSS and add vendor prefixes to CSS rules using values from Can I Use. It is recommended by Google and used in Twitter, and Taobao.

[PostCSS Clean](https://github.com/leodido/postcss-clean) **Minify the CSS**
>PostCss plugin to minify your CSS

Using these optimizations I was able to reduce the ourputted CSS size by around 80%. Ofcourse you are free to choose any other CSS optimization tools, this is just what worked best for me 😉

## TODO
- Implement loader for the slower `getMatchedCSSRules()` polyfill
- Support pseudo elements
- Re-capture on window-resize for easy media-query capturing
- Auto prefixing
- Auto optimize
