# NodeJS - Bootstrapping Cucumber

> Cucumber is a tool that supports Behavior Driven Development (BDD).

*__Note__: This guide assumes you have NodeJS installed.*

1. Create a new project directory

  ```bash
  mkdir new_kata
  ```

2. Create `package.json` inside the new project

```bash
cd new_kata
npm init -y
```

3. Add `cucumber` and `chai` packages

```bash
npm install --save-dev cucumber chai
```

*__Note__: We will use `chai` for making assertions.*


4. Add test running script in `package.json`

```json
"scripts": {
    "test": "cucumber-js"
}
```

5. Create a feature file inside `features` directory

```bash
mkdir features
touch features/Calc.feature
```

```gherkin
Feature: Calculator
  As a budding developper
  I want to learn BDD
  So that there will be less misinterpretation of spec

  Scenario: A Simple calculator
    Given there is a calculator
     When we add 1 and 2
     Then the result should be 3
```

6. Generate step definitions.

Running `npm test` should produce a warning about undefined steps and print the snippets for missing `Given`, `When` and `Then`. Copy them to `features/steps/CalcSteps.js` and change as follows:

```javascript
const { Given, When, Then } = require('cucumber')
const { expect } = require('chai')
const { Calc } = require('../../src/Calc')

let calc, result

Given('There is a calculator', function () {
  calc = new Calc()
})

When('we add {int} and {int}', function (first, second) {
  result = calc.add(first, second)
})

Then('the result should be {int}', function (expected) {
  expect(result).to.equal(expected)
})
```

7. Implement the calculator in `src/Calc.js`.

```javascript
class Calc {
  add(a, b) {
    return a + b
  }
}

module.exports = { Calc }
```

8. Run the test

```bash
npm test
```

You should see this:

```bash
> new_kata@1.0.0 test /YOUR-HOME/PATH-TO/new_kata
> cucumber-js

...

1 scenario (1 passed)
3 steps (3 passed)
0m00.002s
```

Your working directory should look like:

```text
$ tree
.
|____src/
| |____Calc.js
|____features/
| |____Calc.feature
| |____steps/
| | |____CalcSteps.js
|____package.json
|____package-lock.json
```

9. References

* [Cucumber](https://cucumber.io/docs/guides/)
* [Chai](https://www.chaijs.com/)
