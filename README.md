# no-css

An opinionated, lightly-configurable, modern CSS framework to enable rapid building of great-looking sites and apps. See [PROPOSAL.md](https://github.com/JofArnold/no-css/blob/master/PROPOSAL.md) and issues for discussion.

---

### Update 22 Feb 2018

This will be the API

```
<MyComponent styles="flex flex-column items-center fw5 w-50 ... etc" />
```

It will be powered by a CSS-in-JS solution behind the scenes which gets the css styles from splitting the `styles` prop string.

Reasoning:

- No excessive amount of importing: importing styled-components each file is tiresome and I don't want to solve that with babel

- Fast to type: Formats such as `styled-system` e.g. `<View width={1/2} fontSize={3} />` still require excessive typing versus the speed of Tachyons

- Optimised: Can solve the issues of importing a huge style sheet - with unused selectors - as per Tachyons

- It'll work with React Native
