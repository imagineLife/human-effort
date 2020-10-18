# When Considering Dependencies

A reasonable practice is to consider, review, add, and remove dependencies from a project. Here are some thoughts when considering dependencies...

## Its Usages

- What is it used for?
- How often will the project _need_ the dependency?
- Can we do it ourselves?

## Its Size + Complexities

- How large is the dependency?
  - Having large dependencies will add 'bloat' to the project
  - Are there other similar dependencies that are smaller that could work?
- How complicated is the api?
  - The more complicated, the more time developers need to use, understand, update, and adjust the usage of the dependency
  - Can people understand and use the dependency with reasonable ease?
