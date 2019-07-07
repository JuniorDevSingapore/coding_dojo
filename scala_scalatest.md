# Scala - Bootstrapping with ScalaTest

Prerequisites: JDK - please download and install from [AdoptOpenJDK](https://adoptopenjdk.net)

## Steps

1. Install sbt:

    Mac:
    ```bash
    $ brew install sbt@1
    ```

    Windows:
    Install msi from [here](https://www.scala-sbt.org/release/docs/Installing-sbt-on-Windows.html)

    Linux:
    [Installation instructions](https://www.scala-sbt.org/release/docs/Installing-sbt-on-Linux.html)

2. Create new project from seed:

    ```bash
    $ sbt new sbt/scala-seed.g8
    ```

    After installing everything, you will be prompted for the project name:

    ```bash
    A minimal Scala project.

    name [Scala Seed Project]:
    ```

    Enter `kata` and then `cd kata`

3. You will find an example source file at `src/main/scala/example/Hello.scala` and an example test file at `src/test/scala/example/HelloSpec.scala`.

4. You may run the tests with:

    ```bash
    sbt test
    ```

    To have sbt watch the file system for changes(run tests on save), use

    ```bash
    sbt ~test:compile
    ```

## Explanation

The seed is a template that can be found [here](https://github.com/scala/scala-seed.g8). It sets up a new sbt project with some sensible defaults.

Structure of the project:
```
   ├── build.sbt // contains settings for the build, for e.g. Scala version, project version and project name
   ├── project // build support files
   │   └── Dependencies.scala // lists dependencies
   │   └── build.properties // defines sbt version
   ├── target // temporary folder for build output
   └── src
       ├── main
       │   └── scala // Scala code goes here
       └── test
           └── scala // Scala tests go here
```

## References
- [Scala language guide](https://docs.scala-lang.org/tour/tour-of-scala.html)
- [Scala for Java programmers](https://docs.scala-lang.org/tutorials/scala-for-java-programmers.html)
- [sbt documentation](https://www.scala-sbt.org/release/docs/Getting-Started.html)
- [ScalaTest documentation](http://www.scalatest.org/user_guide/writing_your_first_test)
- [ScalaTest matchers](http://www.scalatest.org/user_guide/using_matchers)