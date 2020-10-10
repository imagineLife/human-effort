# Code Review Best Practices

(a reference)[https://google.github.io/eng-practices/review/reviewer/
]

- [Code Review Best Practices](#code-review-best-practices)
  - [The Purposes](#the-purposes)
  - [When Conflicts arise](#when-conflicts-arise)
  - [Code Review Perspectives](#code-review-perspectives)
    - [Good Things](#good-things)
    - [Functionality](#functionality)
    - [Naming](#naming)
    - [Comments](#comments)
    - [Tests](#tests)
    - [Complexity](#complexity)

## The Purposes

Code review assures that the health, hygene, and performance of a piece of proposed functionality to the codebase improves the code.

## When Conflicts arise

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
