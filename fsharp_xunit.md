# F# - Bootstrapping xUnit

*__Note__: This guide assumes you have [.NET Core](https://dotnet.microsoft.com/download/core) installed.*

1. Create a new project folder for the code.

   (*Assuming the project is named `new_kata`*)

    ```shell
    dotnet new xunit -o new_kata -lang F#
    cd new_kata
    dotnet add package FsUnit.xUnit
    ```
2. Delete the following files:
    ```
    Program.fs
    Tests.fs
    ```
3. Open the project file (`new_kata.fsproj`) in a text editor and replace the ItemGroup section with the following:    
    ```xml
    <ItemGroup>
        <Compile Include="Arithmetic.fs" />
        <Compile Include="ArithmeticTests.fs" />
    </ItemGroup>
    ```

4. Inside the project folder (`new_kata`), create a test file (`ArithmeticTests.fs`) with the following content:
    ```fsharp
    module ArithmeticTests

    open FsUnit.Xunit
    open Xunit

    open Arithmetic

    [<Fact>]
    let ``Test that 1 + 2 is 3`` () =
        Add(1, 2) |> should equal 3 
    ```

5. Inside the project folder (`new_kata`), create the implementation file (`Arithmetic.fs`) with the following content:
    ```fsharp
    module Arithmetic 

    let Add(x: int, y: int): int = x + y
    ```

6. Run the test.
    ```shell
    dotnet test
    ```
    You should see this:
    
    ```shell
    Starting test execution, please wait...

    Total tests: 1. Passed: 1. Failed: 0. Skipped: 0.
    Test Run Successful.
    ```


Checkout the [F# Guide](https://docs.microsoft.com/en-us/dotnet/fsharp/) to know more about the language.