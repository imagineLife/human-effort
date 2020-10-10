# Code Review Best Practices

(a reference)[https://google.github.io/eng-practices/review/reviewer/
]

- [Code Review Best Practices](#code-review-best-practices)
  - [The Purposes](#the-purposes)
  - [When Conflicts Arise](#when-conflicts-arise)
  - [Code Review Perspectives](#code-review-perspectives)
    - [Good Things](#good-things)
    - [Functionality](#functionality)
    - [Naming](#naming)
    - [Comments](#comments)
    - [Tests](#tests)
    - [Complexity](#complexity)
- [A Review Method](#a-review-method)
  - [Consider the Big Picture](#consider-the-big-picture)
  - [Review the Primary Elements](#review-the-primary-elements)
  - [Review Details](#review-details)

## The Purposes

Code review assures that the health, hygene, and performance of a piece of proposed functionality to the codebase improves the code.

## When Conflicts Arise

The Code Reviewer(s) and the code author should do their best to come to a consensus. When agreements become complicated, face-to-face meetings or video conferences can be helpful. Some tradeoffs may occur...

- preparing for future scalability v. immediate functionality
- product time constraints

**Do not let merge-requests 'linger' because the author and the reviewer(s) can not come to an agreement.** Request a third set of eyes.

## Code Review Perspectives

Following are a few 'broad' topics to consider when performing code reviews

### Good Things

Telling the developer that they did something well in their code is a great way to beuild confidence in one another! Code review can be a great way to build code design concensus as the product and the team grows.

### Functionality

- Is the proposed functionality good for the _users_ of the code...
  - Is this good _for the product, for the end-user_?
    - does it do what it is expected to, perform the use-case(s)?
    - Will this 'hold up' to any relevant 'edge cases'?
  - Is this good _for other developers, consumers of the direct code_?
    - (_perhaps addressed in more detail in the [Naming](#naming), [Comments](#comments), and [Complexity](#complexity) sections_)

### Naming

- Did the de use expressive names for all things? `A good name is longenough to fully communicate what the it is or does, without being so long that it becomes hard to read`
- Use Descriptive Identifiers
- Perhaps instead of something like...
  ```js
  const arr = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];
  const newArr = arr.filter((d) => d % 2);
  ```
  more expressive naming can be used...
  ```js
  const numbersArr = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];
  const removeEvenNumbers = (d) => d % 2;
  const onlyEvenNumbers = arr.filter(removeEvenNumbers);
  ```

### Comments

Comments can be helpful expressing _why_ a piece of code is used in the proposal.  
When comments explain _what_ the code is doing, consider requesting the developer leverage more [descriptive identifiers](#naming)

- Are there comments?
- Are all comments "necessary"? Using Descriptive Identifiers can aid in replacing comments, making `self-commenting code`

### Tests

The code should have tests.

- Is a new react component involved? Does the component have tests...
  - snapshot
  - props
  - conditional children logic
  - interaction (_clicks, hovers, mouseouts, etc_)
- Is there some javascript involved? Can the javascript be extracted into a stand-along unit of code that is testable?
  - Consider moving a function, or a switch case, to a 'helper' type file && test the function
  -

### Complexity

- Is the logic easy to understand?
- Will other developers, who may not be 'as close to' the code, be able to make sense of the logic, maybe be able to re-use any logic without undue confusion?

# A Review Method

Following is perhaps a step-by-step approach to code reivew:

- consider the 'big picture'
- review 'major' code elements
- review the details

## Consider the Big Picture

Do the changes, in general, 'make sense'? Is the architecture sensible? Is the direction of the implementation(s) in line with the rest of the application? Does the code make way for a coming integrated feature?  
When a merge-request that has 'big picture' concerns, it is best to bring these up before considering further and more granualar implementation details.

- Maybe for a react front-end commit...
  - Do the Components and the component architecture, and the component [composition](https://reactjs.org/docs/composition-vs-inheritance.html) fit together sensibly?
  - Are the pieces in sensible places?
- Maybe for a node/express api commit...
  - do routes, route path strings, and route handlers 'make sense', and follow existing patterns && best-practices?

**Be courteous** when a 'big picture' change seems like a responsible next-step. Respect the dev who put their time, energy, and mental effort into the merge request. They thought it was ready-to-go! Maybe say something like...

```text
  Hey, looks like you put in good effort here, thanks for putting the time in!
  I noticed you took a different approach than we used in SOME_OTHER_PIECE_OF_CODE.
  Can you review that, compare its current implementation, and either
  - update this merge request
  or
  - get back to me and we can review the architecture together with any thoughts you have?
```

## Review the Primary Elements

Once the architecture and the general concepts are clear, review the larger pieces of code next. Find a file that has the most changes. Find the 'parent' container element. Find the complex state-management. Revieweing these will give context to the smaller details.  
When finding design or implementation problems or details that are not clear, it is best to connect with the developer before moving on to smaller implemenation details.

- Is the state management sensible? Is state being stored, managed, and altered in reasonable parts of the merge request?
- Are agreed-upon [DRY](https://deviq.com/don-t-repeat-yourself/) [AHA](https://kentcdodds.com/blog/aha-programming/) principles being leveraged?
- Are application components being leveraged as desired?

**Be courteous** when a 'primary' concern or two seems like a responsible next-step. Respect the dev who put their time, energy, and mental effort into the merge request. At this point, the overall architecture and ''bigger picture' of the merge request should be good-to-go. Any large changes may take some time for the requester to adjust, and letting the dev know ASAP is important. They thought it was ready-to-go! Maybe say something like...

```text
  Hey, the architecture and overall goals of this request look good!
  We are leveraging ComponentX for a very similar use-case, have you reviewed that component?
  Can you review that, compare it to the stuff you have in this merge-request, and either
  - adjust this merge request
  or
  - get back to me and we can review these things together with any thoughts you have
```

## Review Details

With the overall architecture and any major changes already reviewed, look through the remaining implementations of the merge request. Perhaps review the details in a sensible order:

- **front-end** details could be parsed through by component-loading order, or alphabetical order
- **api** details could be parsed through by following an endpoint from url to each response option

- Are css classes written to respect the cascading nature of the stylesheets?
- Is logic parsing data in appropriate places throughout the code?
- Are side-effects 'cleaned-up'?
- are tests assuring reasonable situations, reasonable use-cases?
