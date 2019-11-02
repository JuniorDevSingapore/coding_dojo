# Dart - Bootstrapping Test

*__Note__: This guide assumes you have [Dart SDK](https://dart.dev/get-dart) and [stagehand](https://github.com/dart-lang/stagehand) installed.*

1. Create a new project structure for the code.

   (*Assuming the project is named `new_kata`*)

    ```shell
    mkdir new_kata
    cd new_kata
    stagehand package-simple
    pub get
    ```

2. Modify the generated implementation file (`new_kata\test\new_kata_test.dart`) with the following content:
    ```dart
    import 'package:new_kata/new_kata.dart';
    import 'package:test/test.dart';

    void main() {
        group('Coding Dojo Test Suite', () {
            KataLib library;

            setUp(() {
                library = KataLib();
            });

            test('Simple Addition Test', () {
                expect(library.add(1, 2), 3);
            });
        });
    }
    ```

3. Modify the generated implementation file (`new_kata\lib\src\new_kata_base.dart`) with the following content:
    ```dart
    class KataLib {
        int add(int x, int y) => x + y;
    }
    ```

4. Run the test.
    ```shell
    pub run test
    ```
    You should see something like this:
    
    ```shell
    00:04 +1: All tests passed!
    ```

Checkout the [Dart Language Tour](https://dart.dev/guides/language/language-tour) to know more about the language.