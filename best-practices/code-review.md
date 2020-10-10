# Code Review Best Practices

(a reference)[https://google.github.io/eng-practices/review/reviewer/
]

## The Purposes

Code review assures that the health, hygene, and performance of a piece of proposed functionality to the codebase improves the code.

## When Conflicts arise

The Code Reviewer(s) and the code author should do their best to come to a consensus. When agreements become complicated, face-to-face meetings or video conferences can be helpful. Some tradeoffs may occur...

- preparing for future scalability v. immediate functionality
- product time constraints

**Do not let merge-requests 'linger' because the author and the reviewer(s) can not come to an agreement.** Request a third set of eyes.

## Code Review Perspectives

### Good Things

Telling the developer that they did something well in their code is a great way to beuild confidence in one another! Code review can be a great way to build code design concensus as the product and the team grows.

### Functionality

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

### Tests

### Complexity

### Design
