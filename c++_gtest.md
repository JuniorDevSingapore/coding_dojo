# C++ - Bootstrapping Googletest

*__Note__: This guide assumes you have a C++ compiler installed.*

1. Install [cmake]:

    - Mac

        ```shell
        $ brew install cmake
        ```

    - Linux
       
        ```shell
        $ DIR=`mktemp -d`
        $ cd $DIR
        $ wget https://github.com/Kitware/CMake/releases/download/v3.15.4/cmake-3.15.4-Linux-x86_64.sh
        $ sudo mkdir /opt/cmake
        $ sudo sh cmake-3.15.4-Linux-x86_64.sh --skip-license --exclude-subdir --prefix=/opt/cmake
        $ rm cmake-3.15.4-Linux-x86_64.sh
        ```
        *__Note__: CMake 3.15.4 is the latest version at the time of writing*

        Optionally add CMake to the PATH variable
        ```shell
        echo 'export PATH=/opt/cmake/bin:$PATH' >> ~/.bashrc
        ```
    Verify that the installation was successful
    ```shell
    cmake --version
    ```

2. Create a new project folder for the code:
    
    ```shell
    $ mkdir <project-name>
    $ cd <project-name>
    ```

3. Setup CMake to auto download [googletest]:
    
    Add a file called `AutoDownloadGTest.cmake` under `cmake/modules` with the below contents
    ```cmake
    include(FetchContent)

    FetchContent_Declare(
    googletest
    GIT_REPOSITORY https://github.com/google/googletest.git
    GIT_TAG        release-1.10.0
    )

    FetchContent_GetProperties(googletest)
    if(NOT googletest_POPULATED)
    FetchContent_Populate(googletest)
    add_subdirectory(${googletest_SOURCE_DIR} ${googletest_BINARY_DIR})
    endif()

    include(GoogleTest)
    ```

4. Create a `CMakeLists.txt` in your __project root__ to wire it all together:
    ```cmake
    cmake_minimum_required(VERSION 3.11)

    project(CodingDojo LANGUAGES CXX)
    set(CMAKE_CXX_STANDARD 11)
    list(APPEND CMAKE_MODULE_PATH ${PROJECT_SOURCE_DIR}/cmake/modules)

    enable_testing()
    include(AutoDownloadGTest)

    set(${PROJECT_NAME}_CXX_FLAGS -Wall -Wextra -Werror -g3)
    set(${PROJECT_NAME}_DEBUG_CXX_FLAGS -O0)
    set(${PROJECT_NAME}_RELEASE_CXX_FLAGS -O3)

    function(add_solution SOLUTION)
        add_executable(${SOLUTION} ${SOLUTION}.cc)
        target_compile_options(${SOLUTION} PUBLIC
            "${${PROJECT_NAME}_CXX_FLAGS}"
            "$<$<CONFIG:DEBUG>:${${PROJECT_NAME}_DEBUG_CXX_FLAGS}>"
            "$<$<CONFIG:RELEASE>:${${PROJECT_NAME}_RELEASE_CXX_FLAGS}>")
        target_link_libraries(${SOLUTION} PUBLIC gmock_main)
        gtest_discover_tests(${SOLUTION} TEST_PREFIX "${SOLUTION}.")
    endfunction()

    add_solution(CodingDojo)
    ```

5. Create a `CodingDojo.cc` file in your __project root__ to test:
    ```c++
    #include <gmock/gmock.h>
    #include <string>

    class HelloWorld {
      public:
        std::string say() {
            return "Hello, World!";
        }
    };

    TEST(HelloWorldTest, shouldSayHelloWorld) {
        ASSERT_EQ("Hello, World!", HelloWorld().say());
    }
    ```

6. Build and test that all works:

    ```shell
    $ mkdir build
    $ cd build
    $ cmake ../
    $ make all test
    ```

    You should see an output like below:
    ```cmake
    [ 10%] Building CXX object _deps/googletest-build/googlemock/gtest/CMakeFiles/gtest.dir/src/gtest-all.cc.o
    [ 20%] Linking CXX static library libgtest.a
    [ 20%] Built target gtest
    [ 30%] Building CXX object _deps/googletest-build/googlemock/CMakeFiles/gmock.dir/src/gmock-all.cc.o
    [ 40%] Linking CXX static library libgmock.a
    [ 40%] Built target gmock
    [ 50%] Building CXX object _deps/googletest-build/googlemock/CMakeFiles/gmock_main.dir/src/gmock_main.cc.o
    [ 60%] Linking CXX static library libgmock_main.a
    [ 60%] Built target gmock_main
    [ 70%] Building CXX object CMakeFiles/CodingDojo.dir/CodingDojo.cc.o
    [ 80%] Linking CXX executable CodingDojo
    [ 80%] Built target CodingDojo
    [ 90%] Building CXX object _deps/googletest-build/googlemock/gtest/CMakeFiles/gtest_main.dir/src/gtest_main.cc.o
    [100%] Linking CXX static library libgtest_main.a
    [100%] Built target gtest_main
    Running tests...
    Test project /var/folders/4s/wtz_xy4d2mz_gw8sclcb8x2c0000gn/T/tmp.BD5tu8Xj/project/build
        Start 1: CodingDojo.HelloWorldTest.shouldSayHelloWorld
    1/1 Test #1: CodingDojo.HelloWorldTest.shouldSayHelloWorld ...   Passed    0.01 sec

    100% tests passed, 0 tests failed out of 1

    Total Test time (real) =   0.01 sec
    ```
    
    For more detailed test output run:
    ```shell
    $ ./CodingDojo
    Running main() from gmock_main.cc
    [==========] Running 1 test from 1 test case.
    [----------] Global test environment set-up.
    [----------] 1 test from HelloWorldTest
    [ RUN      ] HelloWorldTest.shouldSayHelloWorld
    [       OK ] HelloWorldTest.shouldSayHelloWorld (0 ms)
    [----------] 1 test from HelloWorldTest (0 ms total)

    [----------] Global test environment tear-down
    [==========] 1 test from 1 test case ran. (0 ms total)
    [  PASSED  ] 1 test.
    ```
__You are all set now with your C++ project__

[cmake]: https://cmake.org
[googletest]: https://github.com/google/googletest