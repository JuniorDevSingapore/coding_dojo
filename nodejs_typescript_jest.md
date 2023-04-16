# NodeJS TypeScript - Bootstrapping Jest Test Suite

Here's instructions on installing Jest and bootstrapping for TypeScript for Node.

*__Note__: This guide assumes you have NodeJS installed.*

1. Create a new project folder for the code:

    (*Assuming project name is `new_kata`*)

    ```bash
    mkdir new_kata
    cd new_kata
    ```

2. In the new project folder, create `package.json`

    ```bash
    npm init -y
    ```

3. Add packages

    ```bash
    npm install typescript
    npm install --save-dev @types/node ts-node jest ts-jest @types/jest
    ```

4. Add test running script in `package.json`

    ```json
    "scripts": {
      "test": "jest",
      "test:watch": "jest --watch"
    }
    ```

5. Create a `ts-jest` config file:

    ```bash
    ./node_modules/.bin/ts-jest config:init
    ```

6. Create a `tsconfig.json` file:

    ```bash
    ./node_modules/.bin/tsc --init
    ```

7. Create a code (`sum.ts`) file

    ```typescript
    function sum(a: number, b: number): number {
      return a + b;
    }
    export default sum;
    ```

8. Create a test (`sum.test.ts`) file

    ```typescript
    import sum from './sum';

    describe('sum module', () => {
      test('adds 1 + 2 to equal 3', () => {
        expect(sum(1, 2)).toBe(3);
      });
    });
    ```

9. You can run the test:

    ```bash
    npm test
    ```

    You should see this:

    ```bash
    ➜ npm run test

    > demo@1.0.0 test
    > jest

    PASS  src/sum.test.ts
      sum module
        ✓ adds 1 + 2 to equal 3 (1 ms)

    Test Suites: 1 passed, 1 total
    Tests:       1 passed, 1 total
    Snapshots:   0 total
    Time:        1.788 s
    Ran all test suites.
    ```

10. Read up more about the types of test matchers available in Jest: <https://jestjs.io/docs/en/using-matchers>
