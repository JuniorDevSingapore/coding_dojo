# Rust - Bootstrapping Cargo Test

*__Note__: This guide assumes you have [Rust](https://www.rust-lang.org/tools/install) installed.*

1. Create a new project structure for the code.

   (*Assuming the project is named `new_kata`*)

    ```shell
    cargo new new_kata --lib
    cd new_kata
    mkdir tests
    ```

2. Inside the tests folder (`tests`), create a test file (`lib.rs`) with the following content:
    ```rust
    extern crate new_kata;

    #[test]
    fn one_plus_two_is_three() {
        assert_eq!(3, new_kata::add(1, 2));
    }
    ```

3. Inside the src folder (`src`), replace the content of the implementation file (`lib.rs`) with the following:
    ```rust
    pub fn add(x: i32, y: i32) -> i32 {
        x + y
    }
    ```

4. Run the test.
    ```shell
    cargo test
    ```
    You should see this section:
    
    ```shell
    running 1 test
    test one_plus_two_is_three ... ok

    test result: ok. 1 passed; 0 failed; 0 ignored; 0 measured; 0 filtered out
    ```


Checkout the [Rust Book](https://doc.rust-lang.org/book/) to know more about the language.