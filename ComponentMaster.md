
## The Component Ninja

### Points Of Interest
- prop-driven components
- React for a heavily data-driven UI
- Testability
- Composability
- "Reason"ability
- Reuse when sensible
- [Building Components Sensibly](#building-components-in-order)
	- [Start With Props](#start-with-props)
	- [Build with Defaults](#build-with-defaults)
	- [Test Often](#test-often)

### Heavily Data Driven Applications
Dashboards.
Spreadsheet replacements.
Data-uploading guis.
Data explorers, reports, analytics, alerts...
These are heavily data-influenced application types. In these use-cases, the data on the screen is probably used to inform a persons time, finances, human resource allocations, company policies, workplace interactions... the list goes on.

#### Data Driven Components
When building react components that are parts of applications like these, rigorous standards are worth-while - - components should be **trustworthy:**
- they show the values they are expected to
- component flexibility is bullet-proof,  && as a developer assuring that all rendering cases are as expected

###  Reusability in action  
Component Developers often find ourselves in familiar dev territory, re-writing similar code constantly. Shoot for sensible re-usability:
...Making another 'box' that looks _slightly different_ from the other 4 boxes on the page?  
...Making another table-cell that has a few of the same classes as other table cells on the page?

When building flexible && re-usable components, rely on tests to assure that all cases happen when && only when the use-cases are instructed to by data....
- have a border that only shows up in **xyz** circumstance? test it.
- have a header or footer that only shows up when **bcd** is true? test it.
-  

### Testable
_"Every single time a bug is encountered, user trust erodes."_ [Kent Dodds](https://testingjavascript.com/)

Tests give trust:
- trust that the **component** does what it is 'supposed' to do
- trust **from other front-end developers** that the code is understandable, sensible, well thought-through, and well cared for beyond 'it works for me'
- trust **from those outside the immediate front-end role**, like ci-cd specialists, api specialists,  stakeholders

**TESTING COMPONENTS**
- assure that **props** are passed to their expected UI elements
	- **Perhaps Skip Testing Prop values**
		- [Enzyme](https://enzymejs.github.io/enzyme/) offers testing features that can assure that a react prop, itself, is as expected, something like ```expect(wrapper.prop('propNameHere')).to.equal('ExpectedPropVal');``` Although this tests that props are as expected, this is not as strong a test as assuring that the prop _value_ is passed to the dom expectedly
	- **Test Prop-Driven UI Content**
		- When a Ui element is populated from props, testit...
			- text
			- element presence
			- number of elements
		- When component 'inner logic' is based off props, perhaps extract the 'inner logic' to an external function. Then, the once tightly-coupled component logic can be tested as stand-alone javascript functional logic 
			- when a class is determined from a prop value...
				- ``` const classString = (prop) => prop ? 'class-one' : 'class-two'```
			- when a conditional 'info' component is present
				- ```const isPresent = prop => prop > 2 ? true : false``` 


### Building Components in order  
#### Start With Props
Instead of starting with content _inside_ the jsx, start with the content passes as props...
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

**or another way...**
```
const Header = ({txt}) => {
  //here, the default text is set internally
  let resText = txt || '-'
  return (<h1>{resText}</h1>)
}
```

#### Test Often
Even a trivial component like this could have tests to assert prop-driven ui content:
- the txt prop is passed as expected
- the 'default' text value is populated when no prop is passed
```
import {shallow} from 'enzyme';
describe('<Header />', () => {
  it('renders "-" when no txt val', () => {
    const Comp = shallow(<Header />)
    expect(Comp.find('h1').text()).toBe("-");
  })
  it('renders prop val when passed', () => {
    const Comp = shallow(<Header txt={'demo here'}/>)
    expect(Comp.find('h1').text()).toBe("demo here");
  })
})
```

#### Fix Bugs (_...before continuing with new features!_)
We may have the luxury of working on a few features 'at once', or at least be able to start something while our last pieces of code get reviewed. Once those details you've already worked on, and submitted for approval, and have been found to have bugs...  
... fix the bugs.  
Before you continue on the new featture(s) you are working on.

#### Explain your code  
In English. (_assuming you're reading this in its native language_)
Without Digging into syntax.  
Practice explaining what your code does.
Maybe even in front of your superiors.
This can bring greater understanding to what the code is doing, and may clear up messes, reduce complexitites or redundancies, and make the code and the project better.   


#### Take Advice  
Listen to those who are ahead of you. They might have solved the exact problems you are working on.  

#### Look for advice   
Look for people who have what you want. They can give you insights.  







