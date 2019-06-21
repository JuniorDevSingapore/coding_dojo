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
	yarn add --dev mocha chai
	```

	or

	```bash
	npm install --save-dev mocha chai
	```

4. Add test running script in `package.json`

	```json
	"scripts": {
	  "test": "mocha",
	  "test:watch": "mocha --watch"
	}
	```

5. Create two directories, src and test

	```bash
	mkdir src
	mkdir test
	```

6. Create a code (`sum.js`) file and store in src directory

	```javascript
	const sum = (a, b) => a + b
	module.exports = sum;
	```

7. Create a test (`sum.test.js`) file and store in test directory.

	```javascript
	const { expect } = require( 'chai' );
	const sum = require( '../src/sum' );

	it( '1 + 2 should be 3', function() {
		expect( sum( 1, 2 ) ).to.equal( 3 );
	} );
	```
> For mocha, it's important that the test scripts are stored in the test directory becuase
> the mocha test runner will look for test script in the test directory.

8. You can run the test:

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

9. Read up more about this set of test frameworks:
* For test framework: [Mocha](https://mochajs.org/)
* For assertion framework: [Chai](https://www.chaijs.com/)
* For mocking framework: [Sinon](https://sinonjs.org/)