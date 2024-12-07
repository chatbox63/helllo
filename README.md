To integrate **TestNG** with **Maven**, you need to configure your Maven project so that it can run TestNG tests. This involves modifying the **`pom.xml`** file and including the necessary dependencies and plugin configurations.

Here's a step-by-step guide:

### 1. **Create a Maven Project**
If you don't already have a Maven project, you can create one using your IDE (like IntelliJ IDEA, Eclipse, etc.) or by running this command in the terminal:
```bash
mvn archetype:generate -DgroupId=com.example -DartifactId=testng-maven-integration -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
```

### 2. **Add TestNG Dependency to `pom.xml`**
Open your `pom.xml` file and add the TestNG dependency inside the `<dependencies>` section:

```xml
<dependencies>
    <!-- TestNG Dependency -->
    <dependency>
        <groupId>org.testng</groupId>
        <artifactId>testng</artifactId>
        <version>7.8.0</version> <!-- Or the latest version -->
        <scope>test</scope>
    </dependency>
</dependencies>
```

### 3. **Add Maven Surefire Plugin to Run Tests**
The Maven Surefire Plugin is used to run tests during the build process. Add the following configuration to your `pom.xml` file, inside the `<build>` section:

```xml
<build>
    <plugins>
        <!-- Surefire Plugin to Run TestNG Tests -->
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-surefire-plugin</artifactId>
            <version>3.0.0-M5</version> <!-- Or latest version -->
            <configuration>
                <suiteXmlFiles>
                    <suiteXmlFile>src/test/resources/testng.xml</suiteXmlFile> <!-- Optional: Specify the path to your TestNG suite -->
                </suiteXmlFiles>
            </configuration>
        </plugin>
    </plugins>
</build>
```

### 4. **Create TestNG Test Class**
Create a simple TestNG test class under the `src/test/java` directory:

```java
package com.example;

import org.testng.Assert;
import org.testng.annotations.Test;

public class SampleTest {

    @Test
    public void testMethod() {
        Assert.assertEquals(1, 1);
    }
}
```

### 5. **Create a TestNG XML Suite (Optional)**
Optionally, you can create a TestNG suite configuration file (`testng.xml`) under the `src/test/resources` directory. This file allows you to group your tests and specify the order of execution.

Here's a basic `testng.xml` example:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<suite name="TestNG Suite">
    <test name="Sample Test">
        <classes>
            <class name="com.example.SampleTest"/>
        </classes>
    </test>
</suite>
```

### 6. **Run the Tests Using Maven**
Once everything is configured, you can run your TestNG tests with the following Maven command:

```bash
mvn test
```

This will trigger Maven to run the tests defined in your project. The Surefire Plugin will look for the TestNG tests and execute them.

### 7. **View the Results**
The results of the tests will be printed to the terminal, and you can also find detailed reports in the `target/surefire-reports` directory, including files like `TEST-com.example.SampleTest.xml`.

---

### Complete Example `pom.xml`

Here's a complete example of a `pom.xml` for integrating TestNG with Maven:

```xml
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>com.example</groupId>
    <artifactId>testng-maven-integration</artifactId>
    <version>1.0-SNAPSHOT</version>

    <dependencies>
        <!-- TestNG Dependency -->
        <dependency>
            <groupId>org.testng</groupId>
            <artifactId>testng</artifactId>
            <version>7.8.0</version>
            <scope>test</scope>
        </dependency>
    </dependencies>

    <build>
        <plugins>
            <!-- Surefire Plugin to Run TestNG Tests -->
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-surefire-plugin</artifactId>
                <version>3.0.0-M5</version>
                <configuration>
                    <suiteXmlFiles>
                        <suiteXmlFile>src/test/resources/testng.xml</suiteXmlFile> <!-- Optional -->
                    </suiteXmlFiles>
                </configuration>
            </plugin>
        </plugins>
    </build>

</project>
```

### Summary
1. Add the TestNG dependency in `pom.xml`.
2. Configure the Maven Surefire Plugin.
3. Create a TestNG test class.
4. Optionally, create a `testng.xml` suite file.
5. Run the tests using `mvn test`.

This setup will integrate TestNG into your Maven project and allow you to run TestNG tests as part of your build process.
