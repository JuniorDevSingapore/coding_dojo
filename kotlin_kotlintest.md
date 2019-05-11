# Kotlin - Bootstrapping Kotlin Test

*__Note__: This guide assumes you have [JDK](https://www.oracle.com/technetwork/java/javase/downloads/index.html) and [Gradle](https://gradle.org/) installed.*

1. Create a new project structure for the code.    
When prompted, use the **default** values for *Project name* and *Source package*.

   (*Assuming the project is named `new_kata`*)

    ```shell
    mkdir new_kata
    cd new_kata
    gradle init --type kotlin-library --dsl kotlin
    ```

2. Modify the generated test file (`new_kata\src\test\kotlin\new_kata\LibraryTest.kt`) with the following content:
    ```kotlin
    package new_kata

    import kotlin.test.Test
    import kotlin.test.assertEquals

    class LibraryTest {
        @Test 
        fun testSomeLibraryMethod() {
            val classUnderTest = Library()
            assertEquals(classUnderTest.Add(1, 2), 3)
        }
    }
    ```

2. Modify the generated implementation file (`new_kata\src\main\kotlin\new_kata\Library.kt`) with the following content:
    ```kotlin
    package new_kata

    class Library {
        fun Add(x: Int, y: Int): Int = x + y;
    }
    ```

4. Run the test.
    ```shell
    gradle test
    ```
    You should see this:
    
    ```shell
    BUILD SUCCESSFUL in 3s
    3 actionable tasks: 3 up-to-date
    ```


Checkout the [Kotlin Reference](https://kotlinlang.org/docs/reference/) to know more about the language.