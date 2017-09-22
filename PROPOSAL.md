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

### Compact output

Generated style sheets in final build should be small. Only include the styles used
