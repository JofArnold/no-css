_tl;dr: use React to generate your functional styling library targetting both the web and native_

# The original issue

We love functional CSS but it does not work as-is for React Native which requires JS(ON) object of style properties.

# We actually need two things


## react-style

We have an existing library generated from postcss but we can't generate anything else than CSS with it.

We need a universal way of describing and generating style libraries targetting any platform.

React seems like a really good fit.

```js
import React from 'react'
import { Library, Set, Classname } from 'react-style'

const colors = [
  {
    name: 'red',
    value: '#CC0000',
  },
  {
    name: 'green',
    value: '#00CC00',
  },
  {
    name: 'blue',
    value: '#0000CC',
  },
]

const spacings = [
  {
    name: 'small',
    value: 5,
  },
  {
    name: 'regular',
    value: 10,
  },
  {
    name: 'large',
    value: 20,
  },
]

export function SliteStyle() {
  return <Library>
    <Set name="colors">
      <Description name="colors" values={Object.map(({ name }) => name)}/>
      {colors.map(({ name, value }) => ([
        <Classname name={name} property="color" value={value}/>
        <Classname name={`background-${name}`} property="background-color" value={value}/>
        <Classname cssOnly name={`background-${name}-on-hover`} selector={`background-${name}-on-hover:hover`} property="background-color" value={value} />
      ]))}
    </Set>

    <Set name="spacing">
      // ...
    </Set>

  </Library>
}
```

Now we need to actually output it to CSS and JSON.

```js
import renderToCSS from 'react-style-css'
import renderToJSON from 'react-style-json'
import renderToHTML from 'react-style-doc'
import SliteStyle from './slite'

const cssString = renderToCSS(<SliteStyle/>, { minified: false })
// object of the form `{[set-name]: <string>}`
// where string is
// /* colors: red, green, blue */
// .red { color: #CC0000 }
// .background-red { background-color: #CC0000 }
// .background-red-on-hover:hover { background-color: #CC0000 }
// etc...

const jsonStyle = renderToJSON(<SliteStyle/>)
/* outputs
{
  colours: {
    'red': { prop: 'color', value: '#CC0000' }
    'background-red': { prop: 'background', value: '#CC0000' }
  },
  spacing: {
  }
}
*/

const styleDoc = generateDoc(<SliteStyle/>)
// whatever is need to generate the HTML documentation of the library
```

## classnamesToStyle

We'd love to write React Native compoments the same way we write regular React DOM components:

```js
function Button({children}) {
  return <button className="border-radius-small white background-blue"></button>
}
```

But the problem is that there is no CSS in React Native, no className, just style.

We need a way to translate class names into style objects which shouldn't be hard at all as long as we have a map such as:

```js
const classToStyleMap = {
  'padding-small': { prop: 'padding', value: '5' },
  'padding-bottom-large': { prop: 'paddingBottom', value: '20' },
  'background-blue': { prop: 'backgroundColor', value: 'blue' },
  'background-red': { prop: 'backgroundColor', value: 'red' },
}

classnamesToStyle('padding-small background-blue')
// { padding: 5, backgroundColor: blue }
```

A template string processor generating HOC à la styled-components would be perfect.

```js
import { TouchableArea, Text } from 'react-native'
import { classnamesToStyleHOC } from 'classnames-to-style'

const Button = ({label, style}) => <TouchableArea style={style}>
  <Text>{Label}</Text>
</TouchableArea>

const StyledButton = classnamesToStyleHOC('background-red border-radius-smnall')(Button)
```

## Unsorted thoughs

* We need a proper way to filter out classes depending on the plaform (:hover makes no sense in React Native) or translate to usable output.
* It can handle nesting, which means we could generate BEM as well.
* It could export whatever is needed to target iOS / Android native platforms

