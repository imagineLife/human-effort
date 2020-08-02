## The Component Master

### Points Of Interest
- prop-driven components
- React for a heavily data-driven UI
- Testability
- Composability
- "Reason"ability

### Testable
_"Every single time a bug is encountered, user trust erodes."_ [Kent Dodds](https://testingjavascript.com/)
Testable React Components
- assure that **props** are passed to their expected UI elements
	- **Perhaps Skip Testing Prop values**
		- [Enzyme](https://enzymejs.github.io/enzyme/) offers testing features that can assure that a react prop, itself, is as expected, something like ```expect(wrapper.prop('propNameHere')).to.equal('ExpectedPropVal');``` Although this tests that props are as expected, this is not as strong a test as assuring that the prop _value_ is passed to the dom expectedly
	- **Test Prop-Driven UI Content**
		- When a Ui element is populated from props, testit...
			- text
			- element presence
			- number of elements
		- When component 'inner logic' is based off props, perhaps extract the 'inner logic' to an external function
			- when a class is determined from a prop value...
				- ``` const classString = (prop) => prop ? 'class-one' : 'class-two'```
			- when a conditional 'info' component is present
				- ```const isPresent = prop => prop > 2 ? true : false``` 