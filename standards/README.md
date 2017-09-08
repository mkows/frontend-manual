# Standards

## Coding Standards

Coding standards are intended to provide convention. The point of coding standards are not to say one style is objectively better than another. Instead, they are to set up known expectations on how code is going to look.

Our reason for established coding standards is best encapsulated in this quote:

> All code in any code-base should look like a single person typed it, no matter how many people contributed. – [Principles of Writing Consistent, Idiomatic JavaScript](https://github.com/rwaldron/idiomatic.js/)

### Philosophy

In order to keep things as simple as possible and encourage the fastest path to production, we believe coding standards should only be *enforced* when there are applicable linting rules. Otherwise, we can end up with excessive, outdated documentation, and unenforced rules. All of our linting rules are **strictly** required; meaning the linter is not simply providing suggestions, but instead **mandatory** notices.

### Implementation

#### Stylistic Standards
All frontend codebases **must** use the following linting for each applicable language:

- JavaScript: [eslint](https://eslint.org)
  - Required preset: [@hbc/eslint-config](https://github.com/hbc-tech/eslint-config)
- CSS / Sass: [stylelint](https://stylelint.io/)
  - Required preset: [@hbc/stylelint-config](https://github.com/hbc-tech/stylelint-config)

#### Testing Standards
Proper testing is imperative to the health of any software. These are our best practices when it comes to testing code:

- Whichever testing framework you use, you should be writing tests!
- Strive to write many, small, pure functions, and minimize where mutations occur.
- Be cautious about stubs and mocks - they can make your tests more brittle.
- All UI should have snapshot testing.
- 100% test coverage is a good goal to strive for, even if it’s not always practical to reach it.
- Whenever you fix a bug, _write a regression test_. A bug fixed without a regression test is almost certainly going to break again in the future.

### Further Improvements

The frontend development landscape is constantly changing. If you would like to propose a change to any of our rules, please raise a Github issue in the respective preset's repository so the team can review it and draw consensus.
