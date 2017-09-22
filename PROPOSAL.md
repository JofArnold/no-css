### Functional CSS

One class name per CSS property, ala Tachyons / BassCSS / AtomicCSS

### No build step beyond first configuation

We don't want to add yet another build step to already complex toolchains. You only build when you update your styles.


### Don't type CSS

Users should be encouraged to *only* use class names and avoid using custom components style.

### Ban or lint-against overrides and conflicts

`class="mb5 mb4"` should not be permitted. User generated `h1.mb4` should also not be permitted.

### Responsive layouts out of the box

Probably using Bootstrap-style col-xs-6 (see https://github.com/GraphQLTraining/graphqltraining.github.io/blob/develop/src/layouts/flexgrid.scss)

### Performance

Must take full advantage of browser's internal abilities (rendering, caching, pre-fetching)

### Customisable but with opinionated defaults

Must have defaults, like Tachyons, that pretty much guarantee good-looking output and vertical rhythm. Some customisation such as gutter widths

### Must work with React-style components

### Should work with React Native

Even if it requires a compilation step. That's ok here

### Must support naked tags (e.g. h1, h2, p, div)

Probably via composition. See https://github.com/GraphQLTraining/graphqltraining.github.io/blob/develop/src/layouts/globals.scss

Reason: because some tools, such as markdown, may output naked tags without user control. User must be able to style them using only the existing styles. E.g. as per how example above composes Tachyons in a CSS Modules like way:


```
h1 {
  @extend .f5;
  @extend .mb5-l;
  @extend .mb4;
}
```

### Compact output

Generated style sheets in final build should be small. Only include the styles used

### Configurable media breakpoints out of the box

Consider fully fluid layouts? How would this be represented as a class name?

### No "between" media queries

E.g. not "min: 60, max: 90". Reason; it's confusing.

### Media queries are mobile first

E.g. desktop would be achieved by a class like `md5-l` meaning "apply 5th margin value above large width" as opposed to `md5-mobile` meaning "apply 5th margin up to the maximum mobile size"


### No nested/child/sibling selectors? (Except pseudo classes)

Not sure about this one...

### All native styled stripped by default?

### How should it handle leakage from third-party style sheets?

### Styles should always be editable in dev tools

This means clear, global class names (not obfuscated hashes). If possible should ensure styles don't become read-only as per frequent Hot Module Replacement issues.

### The building blocks we need

1. A way to univerally write functional styling that output CSS but maybe other things. postCSS / SASS like are options but we need more output options than CSS. A react renderer could be a solution.
1. With the above, it should become easy to generate variables and loops to generate functionnal CSS
1. Provide one or many example libraries people can use as is or fork for their own projects.