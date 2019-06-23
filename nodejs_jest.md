# NodeJS - Bootstrapping Jest Test Suite

Here's instructions on installing Jest and bootstrapping for [ES6 module compilation][babel] for Node.

*__Note__: This guide assumes you have NodeJS installed.*

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
	yarn add --dev jest @babel/core @babel/preset-env
	```

	or

	```bash
	npm install --save-dev jest @babel/core @babel/preset-env
	```

4. Add test running script in `package.json`

	```json
	"scripts": {
	  "test": "jest",
	  "test:watch": "jest --watch"
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

6. Create a code (`sum.js`) file

	```javascript
	const sum = (a, b) => a + b
	export default sum
	```

7. Create a test (`sum.test.js`) file

	```javascript
	import sum from './sum'

	test('adds 1 + 2 to equal 3', () => {
	  expect(sum(1, 2)).toBe(3);
	});
	```

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
	yarn run v1.9.4
	$ jest
	 PASS  ./sum.test.js
	  ✓ adds 1 + 2 to equal 3 (3ms)

	Test Suites: 1 passed, 1 total
	Tests:       1 passed, 1 total
	Snapshots:   0 total
	Time:        1.286s
	Ran all test suites.
	✨  Done in 2.39s.
	```

9. Read up more about the types of test matchers available in Jest: [https://jestjs.io/docs/en/using-matchers][jest-matchers]

[babel]: https://babeljs.io/docs/en/
[babel-preset-env]: https://babeljs.io/docs/en/babel-preset-env
[jest-matchers]: https://jestjs.io/docs/en/using-matchers
[sp-nexus-npm]: https://code.in.spdigital.io/sp-digital/sp-devops-docs/blob/master/how-tos/nexus/how-to-npmjs.md