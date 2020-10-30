## A React Aficionado

- [A React Aficionado](#a-react-aficionado)
  - [Build Components in order](#build-components-in-order)
    - [Start With Props](#start-with-props)
    - [Build With Defaults](#build-with-defaults)
    - [Test Often](#test-often)
  - [Building For Easy Dev Work](#building-for-easy-dev-work)
  - [Fix Bugs](#fix-bugs)
    - [Take Advice](#take-advice)
    - [Look for advice](#look-for-advice)
  - [Understand the Code](#understand-the-code)
    - [Explain your code](#explain-your-code)
    - [Attempt to understand dependencies](#attempt-to-understand-dependencies)
    - [Learn More JS](#learn-more-js)
    - [Master all the react](#master-all-the-react)
  - [Heavily Data Driven Applications](#heavily-data-driven-applications)
    - [Data Driven Components](#data-driven-components)
  - [Reusability in action](#reusability-in-action)
  - [Persistence Ignorant Components](#persistence-ignorant-components)
- [A Shorthand React Checklist](#a-shorthand-react-checklist)

**Extra Credit**

- [Understand the Code](#understand-the-code)
  - [Explain It](#explain-your-code)
  - [Dig in to dependencies](#attempt-to-understand-dependencies)
  - [Learn More JS](#learn-more-js)
  - [Master React](#master-react)
- A note on [Data-Driven Applications](#heavily-data-driven-applications)

---

### Build Components in order

#### Start With Props

Instead of starting a new component with content _inside_ the jsx, start with the content passes as props...
**instead of...**

```
const Header = () => (<h1>Prop-Driven Text Here</h1>)

(rendering with)
<Header />
```

**start with...**

```
const Header = ({txt}) => (<h1>{txt}</h1>)

(rendering with)
<Header txt="Prop-Driven Text Here" />
```

#### Build With Defaults

Assert a default value
**instead of...**

```
const Header = ({txt}) => (<h1>{txt}</h1>)

(rendering with)
<Header txt="Prop-Driven Text Here" />
```

**start with...**

```
const Header = ({txt}) => (<h1>{txt}</h1>)


. . . . . .


//HERE, '-' is the 'default'
let [headerText, setHeaderText] = useState('-')

//trigger a CHANGE in the headerText val
useEffect(() => {
	//fetch some text
	setHeaderText(fetchedText)
}, [])

//this will render the 1x with '-' as a default text
//this will render the 2x with the text that was fetched
<Header txt={headerText} />
```

**or another way of setting a default value...**

```
const Header = ({txt}) => {
  //here, the default text is set internally
  let resText = txt || '-'
  return (<h1>{resText}</h1>)
}
```

**or maybe...**

```
const Header = ({txt}) => {
  return (<h1>{resText || '-'}</h1>)
}
```

#### Test Often

_"Every single time a bug is encountered, user trust erodes."_ [Kent Dodds](https://testingjavascript.com/)

Start with testing...

- html output from props
- interaction
- conditional rendering of any 'child' elements
- integrated JS logic

Even a trivial component like this Header example above could have tests to assert prop-driven ui content:

- the txt prop is passed as expected
- the 'default' text value is populated when no prop is passed

```
import {mount} from 'enzyme';
describe('<Header />', () => {
  it('renders "-" when no txt val', () => {
    const Comp = mount(<Header />)
    expect(Comp.find('h1').text()).toBe("-");
  })
  it('renders prop val when passed', () => {
    const Comp = mount(<Header txt={'demo here'}/>)
    expect(Comp.find('h1').text()).toBe("demo here");
  })
})
```

Test JS logic.  
Break a 'filter', 'map', or 'reduce' callback out into a testable javascript function. Move a conditional-logic switch statement into a testable javascript function.

Tests give trust:

- trust that the **component does what it is 'supposed' to do**
- **trust from other developers** that the code is understandable, sensible, well thought-through, and well cared for beyond 'it works for me'
- trust **from those outside the immediate front-end role**, like ci-cd specialists, api specialists, stakeholders

### Building For Easy Dev Work

Abstract away implentation details by sensibly naming props.
Go for boolean props instead of prop-&-value combos. Put the _implementation details_ of component logic inside the component code itself, and make the component simpler to use for the developers around you, by using

- Shoot for a prop name like `border` as a prop instead of `className="border"`. Put the border _logic_ inside the component itself, and give the developer a simpler component api.
- Shoot for `large` as a prop instead of `className="button-wide font-xl button-tall"`. Make the component internals interpret the one-word prop and set the component with all appropriate details.

### Fix Bugs

(_...before continuing with new features!_)

We may have the luxury of working on a few features 'at once', or at least be able to start something while our last pieces of code get reviewed by peers or q folks. Once those details you've already worked on, and submitted for approval, and have been found to have bugs...  
... fix the bugs.  
Before you continue on the new feature(s) you are currently working on.

#### Take Advice

Listen to those who are ahead of you. They might have solved the exact problems you are working on.

#### Look for advice

Look for people who have what you want. They can give you insights.

### Understand the Code

#### Explain your code

In English. (_assuming you're reading this in its native language_)
Without Digging into syntax.  
Practice explaining what your code does.
Maybe even in front of your peers. Or even your superiors.
This can bring greater understanding to what the code is doing, and may clear up unintended messes in the code... maybe even reduce complexitites or redundancies.

#### Attempt to understand dependencies

We can become over-dependant on dependencies.  
We may be using dependencies that introduce dozens, even hundreds of lines of logic into our code, just to save ourselves 3-4 lines of manual effort.  
We may not realize that we can do the same thing a dependency does! Maybe even sometimes resulting in less confusion, more simplicity, and even more trust in the code!
We might find oursevles programming to fit the depndency that has breaking changes, just to solve the same problem that was solved before the break.

#### Learn More JS

Learn that JS detail that you might be sort-of interested in...  
Call.  
Bind.  
Reduce.  
Currying.  
Async / Await.

#### Master all the react

useMemo.
useRef.  
Suspense.  
cloneElement.  
React's Diffing smarts.  
React DevTools.  
Compound Components.
Render Props.
Implicit props.  
Context.

Apply these things as fast as you learn them. This will crystalize the understanding process. Maybe even explain the code to some folks.

### Heavily Data Driven Applications

Dashboards.
Spreadsheet replacements.
Data-uploading guis.
Data explorers, reports, analytics, alerts...
These are heavily data-influenced application types. In these use-cases, the data on the screen is probably used to inform a persons time, finances, human resource allocations, company policies, workplace interactions... the list goes on.

#### Data Driven Components

When building react components that are parts of applications like these, rigorous standards are worth-while - - components should be

- **trustworthy:**
  - they show the values they are expected to
  - the 'default' value is expected
- **flexible**
  - component flexibility expecttions are clear, tested, and in-use

---

- ### Points Of Interest
- prop-driven components
- React for a heavily data-driven UI
- Testability
- Composability
- "Reason"ability
- Reuse when sensible

---

### Reusability in action

Component Developers often find ourselves in familiar dev territory, re-writing similar code constantly. Shoot for sensible re-usability:
...Making another 'box' that looks _slightly different_ from the other 4 boxes on the page?  
...Making another table-cell that has a few of the same classes as other table cells on the page?

When building flexible && re-usable components, rely on tests to assure that all cases happen when && only when the use-cases are instructed to by data....

- have a border that only shows up in **xyz** circumstance? test it.
- have a header or footer that only shows up when **bcd** is true? test it.

### Persistence Ignorant Components

Consider making **as much 'state' logic as possible** outside the scope of a component:

- need to **fetch** some data? do it in a provider
- need to **trigger a new fetch**? call a fn that's been passed through a prop, or a fn that is imported through using a context
- need to **respond to new data**? ... react can do this well already!

## A Shorthand React Checklist

When building & reviewing a react frontend, here's a short-hand set of items to assure:

- [ ] **State is de-coupled appropriately**, leveraging agreed-upon state-management tooling, like [React's own Context](https://reactjs.org/docs/context.html)
- [ ] Component Props are tested
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
