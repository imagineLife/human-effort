- [A React + Frontend Best Practices Checklist](#a-react--frontend-best-practices-checklist)
  - [Components are explained](#components-are-explained)
  - [State is handled & scoped appropriately](#state-is-handled--scoped-appropriately)
    - [State is Scoped](#state-is-scoped)
    - [State is Owned By React](#state-is-owned-by-react)
  - [Components are Tested](#components-are-tested)
  - [JavaScript is extracted](#javascript-is-extracted)
  - [Styles are scoped](#styles-are-scoped)

# A React + Frontend Best Practices Checklist

When building & reviewing a frontend app using React, here's a set of items to assure:

## Components are explained

- [ ] A comment block at the top of a component page explains details about the component
  - [ ] its use-cases
  - [ ] overview of props && their impact on the component (\_perhaps in combination with [a 'type' system](https://flow.org/)

## State is handled & scoped appropriately

### State is Scoped

- [ ] State is stored at relevant component 'level' in the rendering tree
  - [ ] available by all components that use the state
  - [ ] not too 'high' that state-changes cause re-renders of irrelevant componnents
  - [ ] not too 'low' that similar states are duplicated across components
  - [ ] **de-coupled appropriately**, leveraging agreed-upon state-management tooling, like [React's own Context](https://reactjs.org/docs/context.html)

### State is Owned By React

- [ ] State is given to React for rendering control
  - [ ] dom manipulation handled by [useRef](https://reactjs.org/docs/hooks-reference.html#useref)
  - [ ] side-effects are handled by [useEffect](https://reactjs.org/docs/hooks-reference.html#useeffect)
  - [ ] changable state that affects rendering is handled by [useState](https://reactjs.org/docs/hooks-reference.html#usestate) or through a prop
  - [ ]

## Components are Tested

- [ ] State-Informing props are tested with various states:
  - [ ] When no state data is passed
  - [ ] When little state data is passed
  - [ ] when 'lots' of state data is passed
- [ ] Style-Informing props are tested with expected options
  - [ ] props that inform classnames
  - [ ] props that inform styles
- [ ] Conditional-element controlling props are tested
  - [ ] Children &/or elements show when expected
  - [ ] Children &/or elements are not show when expected to not be shown
  - [ ] 'disabline' states are tested
  - [ ] conditional element positioning is tested
- [ ] Interaction-Handling Callbacks are tested
  - [ ] onClick's are called when expected
  - [ ] mouse events are triggered/handled

## JavaScript is extracted

- [ ] Javascript logic is extracted when possible
  - [ ] a function that consumes props or state and outputs ui-consumable content can be extracted && tested as a stand-alone function

## Styles are scoped

- [ ] A Component has a 'root' class corresponding with itself
  - EXAMPLE: a `<Header/>` component has a `header` class at the 'root' of the component's styles
- [ ] Components allow props to control custom use-case styling:
  - A 'className' prop
    - EX. `<Header className="fancy light" />` will build html with `class="header fancy light"`, addings styles like `font-size: 24px; text-align: left; font-style: italics; font-weight: 200;`
  - Props that are interpreted by js & converted to class strings inside the component
    - EX. `<Header fancy bold />` could build html with `class="header fancy bold"`, addings styles like `text-align: left; font-size: 24px; font-style: italics; font-weight: 800;`
