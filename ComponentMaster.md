## The Component Master

### Points Of Interest
- prop-driven components
- React for a heavily data-driven UI
- Testability
- Composability
- "Reason"ability
- Reuse when sensible

### Heavily Data Driven Applications
Dashboards.
Spreadsheet replacements.
Data-uploading guis.
Data explorers, reports, analytics, alerts...
These are heavily data-influenced application types. In these use-cases, the data on the screen is probably used to inform a persons time, finances, human resource allocations, company policies, workplace interactions... the list goes on.
When building react components that are parts of applications like these, rigorous standards are worth-while - components should be **trustworthy**
- they show the values they are expected to
- component flexibility is bullet-proof,  && as a developer assuring that all rendering cases are assured to _only_ happen when data 'tells' the component to
	

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