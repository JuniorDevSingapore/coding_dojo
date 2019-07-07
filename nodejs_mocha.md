# NodeJS - Bootstrapping Mocha Test Suite

Here's instructions on installing Mocha and Chai for Node.

*__Note__: This guide assumes you have NodeJS installed.*

> Mocha is an alternative test framework used in javascript.
> Chai is an assertion library that is used along with Mocha.

1. Create a new project folder for the code:

	(*Assuming project name is `new_kata`*)

	```bash
	mkdir new_kata
	cd new_kata
	```

2. In the new project folder, create `package.json`

	```bash
	yarn init
	```

	or

	```bash
	npm init
	```

3. Add packages

	```bash
	yarn add --dev mocha chai @babel/core @babel/preset-env @babel/register
	```

	or

	```bash
	npm install --save-dev mocha chai @babel/core @babel/preset-env @babel/register
	```

4. Add test running script in `package.json`

	```json
	"scripts": {
	  "test": "mocha --require @babel/register",
	  "test:watch": "mocha --require @babel/register --watch"
	}
	```

5. Create a `.babelrc` with these content for a [smart preset babel configuration][babel-preset-env]

	```json
	{
		"presets": [
			["@babel/preset-env",
				{
					"targets": {
						"node": "10"
					}
				}
			]
		]
	}
	```

6. Create two directories, src and test

	```bash
	mkdir src
	mkdir test
	```

7. Create a code (`sum.js`) file and store in `src` directory

	```javascript
	const sum = (a, b) => a + b
	export default sum
	```

8. Create a test (`sum.test.js`) file and store in `test` directory.

	```javascript
	import { expect } from 'chai'
	import sum from '../src/sum'

	it( '1 + 2 should be 3', function() {
		expect( sum( 1, 2 ) ).to.equal( 3 )
	} )
	```
> For mocha, it's important that the test scripts are stored in the test directory becuase
> the mocha test runner will look for test script in the test directory.

9. You can run the test:

	```bash
	yarn test
	```

	or

	```bash
	npm test
	```

	You should see this:

	```bash
	$ mocha

	✓ 1 + 2 should be 3

	1 passing (5ms)
	```

10. Read up more about this set of test frameworks:

	* For test framework: [Mocha](https://mochajs.org/)
	* For assertion framework: [Chai](https://www.chaijs.com/)
	* For mocking framework: [Sinon](https://sinonjs.org/)

_Reference: [My Node.js Setup (Mocha & Chai, Babel7, ES6)](https://dev.to/bnorbertjs/my-nodejs-setup-mocha--chai-babel7-es6-43ei)_

[babel-preset-env]: https://babeljs.io/docs/en/babel-preset-env