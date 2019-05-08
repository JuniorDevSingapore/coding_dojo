# Java - Bootstrapping JUnit

Here's instructions on bootstrapping a Java project with Gradle and JUnit4

*__Note__: This guide assumes you have Java installed.*

1. Install gradle:

    with __Homebrew__:
    ```bash
    $ brew install gradle
    ```
    
    Manually:
    ```bash
    $ wget https://services.gradle.org/distributions/gradle-5.4.1-bin.zip
    $ sudo mkdir /opt/gradle
    $ sudo unzip -d /opt/gradle gradle-5.4.1-bin.zip
    $ export PATH=$PATH:/opt/gradle/gradle-5.4.1/bin
    ```
    
    Run the following your installation went through correctly 
    ```bash
    $ gradle -v
    ```
    
2. Create a new project folder for the code:
    ```bash
    $ mkdir <project-name>
    $ cd <project-name>
    ```

3. Initialise the project as a Gradle project. 

    This will create the necessary files and folders, along with a gradle wrapper  
    ```bash
    $ gradle init
    ```
    Run the following to ensure everything is configured as expected:
    ```bash
    $ ./gradlew -v
    ```
    You should see the same result as above
    
4. Create the directories corresponding to the standard Java directory structure:
    ```bash
    $ mkdir src && cd src
    $ mkdir main
    $ mkdir test
    $ mkdir main/java
    $ mkdir test/java
    ```
    Your project structure should now look like:
    ```
   .
   ├── build.gradle
   ├── gradle
   │   └── wrapper
   │       ├── gradle-wrapper.jar
   │       └── gradle-wrapper.properties
   ├── gradlew
   ├── gradlew.bat
   ├── settings.gradle
   └── src
       ├── main
       │   └── java
       └── test
           └── java
   ```
5. Create a class under `src/main/java`. For example,

    *HelloWorld.java*
    ```java
    public class HelloWorld {
        public String say() {
            return "Hello, World!";
        }
    }
    ```
6. Create a corresponding test class under `src/main/test`.

    *HelloWorldTest.java*
    ```java
    import org.junit.Test;
    import org.junit.Assert;
    
    public class HelloWorldTest {
        @Test
        public void shouldSayHelloWorld() {
            HelloWorld helloWorld = new HelloWorld();
    
            Assert.assertEquals("Hello, World!", helloWorld.say());
        }
    
    }
    ```
    This does not compile just yet. To make it compile, you need to add JUnit as a dependency to your project.

7. Add JUnit to the project. Add the following content in your `build.gradle` file:

    ```groovy
    apply plugin: 'java'
    
    repositories {
        mavenCentral()
    }
    
    dependencies {
        testImplementation 'junit:junit:4.12'
    }
    ```
8. Run the build as follows:
    ```bash
    $ ./gradlew build
    ```    
    You should see:
    ```bash    
    BUILD SUCCESSFUL in 0s
    4 actionable tasks: 4 up-to-date
    ```

__You are all set now with your Java project__