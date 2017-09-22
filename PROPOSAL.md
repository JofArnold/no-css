### Atomic/Tachyons

One class name per CSS property, ala Tachyons

### No build step beyond first configuation

Should not require webpack or other build step to support use in web dev, beyond initial compilation from SASS or similar

### Don't type CSS

Users should be encouraged to *only* use class names

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

