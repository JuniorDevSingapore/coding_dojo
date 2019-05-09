# C# - Bootstrapping xUnit

*__Note__: This guide assumes you have [.NET Core](https://dotnet.microsoft.com/download/core) installed.*

1. Create a new project folder for the code.

   (*Assuming the project is named `new_kata`*)

    ```shell
    dotnet new xunit -o new_kata
    cd new_kata
    rm .\UnitTest1.cs
    ```

2. Inside the project folder (`new_kata`), create a test file (`TestArithmetic.cs`) with the following content:
    ```csharp
    using System;
    using Xunit;

    namespace new_kata
    {
        public class TestArithmetic
        {
            [Fact]
            public void TestThat1Plus2Is3()
            {
                Assert.Equal(3, Arithmetic.Add(1, 2));
            }
        }
    }
    ```

3. Inside the project folder (`new_kata`), create the implementation file (`Arithmetic.cs`) with the following content:
    ```csharp
    namespace new_kata
    {
        public static class Arithmetic
        {
            public static int Add(int x, int y) => x + y; 
        }
    }
    ```

4. Run the test.
    ```shell
    dotnet test
    ```
    You should see this:
    
    ```shell
    Starting test execution, please wait...

    Total tests: 1. Passed: 1. Failed: 0. Skipped: 0.
    Test Run Successful.
    ```


Checkout the [C# Guide](https://docs.microsoft.com/en-us/dotnet/csharp/) to know more about the language.