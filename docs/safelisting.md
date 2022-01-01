---
title: Safelisting | PurgeCSS
lang: en-US
meta:
  - name: description
    content: To avoid PurgeCSS to remove unused CSS that you want to keep, you can safelist selectors.
  - itemprop: description
    content: To avoid PurgeCSS to remove unused CSS that you want to keep, you can safelist selectors.
  - property: og:url
    content:  https://purgecss.com/safelisting
  - property: og:site_name
    content: purgecss.com
  - property: og:image
    content: https://i.imgur.com/UEiUiJ0.png
  - property: og:locale
    content: en_US
  - property: og:title
    content: Remove unused CSS - PurgeCSS
  - property: og:description
    content: To avoid PurgeCSS to remove unused CSS that you want to keep, you can safelist selectors.
---

::: tip
The documentation is for PurgeCSS 3.0 and above. To see the documentation for PurgeCSS 2.x, click [here](https://github.com/FullHuman/purgecss/tree/5314e41edf328e2ad2639549e1587b82a964a42e/docs)
:::

# Safelisting

You can indicate which selectors are safe to leave in the final CSS. This can be accomplished with the PurgeCSS option `safelist`, or directly in your CSS with a special comment.

## Specific selectors

You can add selectors to the safelist with `safelist`. 

```js
const purgecss = new Purgecss({
    content: [], // content
    css: [], // css
    safelist: ['random', 'yep', 'button']
})
```

In the example, the selectors `.random`, `#yep`, `button` will be left in the final CSS.

## Patterns

You can safelist selectors based on a regular expression with `safelist.standard`, `safelist.deep`, and `safelist.greedy`.

```js
const purgecss = new Purgecss({
    content: [], // content
    css: [], // css
    safelist: {
      standard: [/red$/],
      deep: [/blue$/],
      greedy: [/yellow$/]
    }
})
```

In the example, selectors ending with `red` such as `.bg-red`, selectors ending with `blue` as well as their children such as `blue p` or `.bg-blue .child-of-bg`, and selectors that have any part ending with `yellow` such as `button.bg-yellow.other-class`, will be left in the final CSS.

Patterns are regular expressions. You can use [regexr](https://regexr.com) to verify the regular expressions correspond to what you are looking for.

## In the CSS directly

You can safelist directly in your CSS with a special comment.
Use `/* purgecss ignore */` to safelist the next rule.

```css
/* purgecss ignore */
h1 {
    color: blue;
}
```

Use `/* purgecss ignore current */` to safelist the current rule.

```css
h1 {
    /* purgecss ignore current */
    color: blue;
}
```

You can use `/* purgecss start ignore */` and `/* purgecss end ignore */` to safelist a range of rules.

```css
/* purgecss start ignore */
h1 {
  color: blue;
}

h3 {
  color: green;
}
/* purgecss end ignore */

h4 {
  color: purple;
}

/* purgecss start ignore */
h5 {
  color: pink;
}

h6 {
  color: lightcoral;
}

/* purgecss end ignore */
```

### Gotchas

Some CSS optimising tools such as PostCSS or cssnano will strip comments before PurgeCSS runs in your build process, this can go unnoticed as often these steps are disabled in development. To prevent these comments being removed you can mark as important with an exclamation mark.

```css
/*! purgecss start ignore */
h5 {
  color: pink;
}

h6 {
  color: lightcoral;
}

/*! purgecss end ignore */
```
