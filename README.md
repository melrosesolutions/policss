# policss
PoliCSS (pronounced Po-lis) will Enforce a CSS methodology, Suppress individual coding styles, Control specificity and Oppress team members.

## What is it?
PoliCSS is a CSS methodology and a PostCSS based linter designed to enforce it.

## Benefits

* Easier maintenance
* Reduce Bugs
* Portable between projects

## Key Concepts

* Use semantically named classes/modules
* Reduce and __Control__ specificity. Keeps as low as possible, without equalling selectors
* Well-defined structure to selectors
  * Order of selectors should not make a difference
  * Module should not care about parent selectors
* n types of selector:
  1. single html tags e.g. `p` - defined in `base` folder
  2. nested html tags. Can only be used for tags that could have different parent tags e.g. `ul li` - defined in `base` folder. Limited to `ul/ol li`, `thead/tbody/tfoot tr/th/td`
  3. microformat selectors - TODO
  4. module selector. single class name e.g. `.foo`. Must have same name as module file i.e. `modules/foo.css`
  5. module sub-tag. Used to target a specific tag inside the module e.g. `.foo h3` or `article.foo`. Cannot be parent element of module
  6. module sub-component. Single class name, prefixed with module name e.g. `.foo-bar` for `bar sub-component`
  7. nested module. Used to alter the css of a child module e.g. `.foo .baz` or `.foo .baz a` where `.baz a` has already been defined in `.baz` module
  8. status. Must be prefixed with `is-` or `has-`. These are classes that are likely to be added/removed to an element at runtime. Typical selectors would be `.foo.is-active` or `.foo.has-children`
  9. Media query. TODO

## how it works
[PostCSS](https://github.com/postcss/postcss)
[cssnext](http://cssnext.io/)
[Stylelint](http://stylelint.io/)

## Folder Structure

`index.css` includes all files in specific folder order. Files within folders imported alphabetically
to reduce chances of order specificity bugs

1. vendor - any 3rd party css files to import e.g. normalise.css
2. variables - all variables are defined here
3. mixins - mixins defined here
4. base - styles for html tags. no `class` or `id` selectors. `status` selectors allowed
5. microformats - (Optional). Standardized class names and markup patterns
5. modules - Most of the development

## Rules

### Enforceable Rules
1. no `div` in selectors - too generic
1. no `span` in selectors - too generic
1. no __id__ selectors - too specific
1. no generic class/module names e.g. `.container`
1. no floating status selectors - must be attached to an element

### Unenforceable Rules
1. no __presentational__ class/module names e.g. `.red-border`
1. no __media query__ restricted class/module names e.g. `.col-md-3`

## FAQs
1. Empty tags are OK. These should be removed by PostCSS plugins
