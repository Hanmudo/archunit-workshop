---
title: "Workshop: implement ArchUnit in your Java Spring Boot project" 
revealOptions:
  transition: 'none'
---

# Part 2: Implement Basic Rules
Based on dependencies of

- Plain Java
- Junit4 or Junit5

---

## What is a basic rule

A basic architecture test is based on low complexity or logical behaviour

---
## Writing tests

> ArchTests live among the Unit tests in the test folder.
> 
> Recommended is the use of a seperate folder or artifact which stores the arch tests

---

Plain java was used for the project setup, again:

Maven
```xml
<dependency>
    <groupId>com.tngtech.archunit</groupId>
    <artifactId>archunit</artifactId>
    <version>1.3.0</version>
    <scope>test</scope>
</dependency>
```

Gradle
```groovy
dependencies {
    testImplementation 'com.tngtech.archunit:archunit:1.3.0'
}
```
---
Junit4 dependency

Maven
```xml
<dependency>
    <groupId>com.tngtech.archunit</groupId>
    <artifactId>archunit-junit4</artifactId>
    <version>1.3.0</version>
    <scope>test</scope>
</dependency>
```

Gradle
```groovy
dependencies {
    testImplementation 'com.tngtech.archunit:archunit-junit4:1.3.0'
}
```
---

Junit4 ArchUnit example

```java
@RunWith(ArchUnitRunner.class)
@AnalyzeClasses(packages = "com.example.archunitspring.application.services")
public class ArchUnitJunit4Test {

    @ArchTest
    public static ArchRule services_should_be_prefixed =
            classes()
                    .that().resideInAPackage("..services..")
                    .and().areAnnotatedWith(Service.class)
                    .should().haveSimpleNameStartingWith("Service");
}
```

---
Junit5 dependency

Maven
```xml
<dependency>
    <groupId>com.tngtech.archunit</groupId>
    <artifactId>archunit-junit5</artifactId>
    <version>1.3.0</version>
    <scope>test</scope>
</dependency>
```

Gradle
```groovy
dependencies {
    testImplementation 'com.tngtech.archunit:archunit-junit5:1.3.0'
}
```
---

Junit5 ArchUnit example

```java
import static com.tngtech.archunit.lang.syntax.ArchRuleDefinition.classes;

@AnalyzeClasses(packages = "com.example.archunitspring.application.services")
public class ArchUnitJunit5Test {

    @ArchTest
    static ArchRule services_should_be_prefixed =
            classes()
                    .that().resideInAPackage("..services..")
                    .and().areAnnotatedWith(Service.class)
                    .should().haveSimpleNameStartingWith("Service");
}
```
---

## Basic rule 1: DAO Classes must reside in a package

```java 
@Test
public void dao_must_reside_in_dao_package() {
    classes().that().haveNameMatching(".*Dao").should().resideInAPackage("..dao..")
        .as("DAOs should reside in a package '..dao..'")
        .check(classes);
}
```
---

## Basic rule 2: No directly coupled code to return type  of the module

```java
@Test
public void the_controller_layer_should_return_API_response_wrappers() {
    methods()
            .that().areDeclaredInClassesThat().resideInAPackage("..anticorruption..")
            .and().arePublic()
            .should().haveRawReturnType(WrappedResult.class)
            .because("we do not want to couple the client code directly to the return types of the encapsulated module")
            .check(classes);
}
```

---

## Basic rule 3: Classes shouldn't throw generic exceptions

```java
@Test
public void classes_should_not_throw_generic_exceptions() {
    NO_CLASSES_SHOULD_THROW_GENERIC_EXCEPTIONS.check(classes);
}
```

---

## Basic Rule 4: Don't permit the use of java util logging

```java
 @Test
public void classes_should_not_use_java_util_logging() {
    NO_CLASSES_SHOULD_USE_JAVA_UTIL_LOGGING.check(classes);
}
```

---

## Tasks

- Switch to the 'basicrules' branch
- Implement 3 test cases with ClassFileImporter
- Implement 3 test cases with AnalyzeClasses and ArchTest annotation.

---

### Test cases

1. Check the naming convention of the services match in package services and end with ServiceImpl 
2. Check if the class of the scheduleEndpoint has dependencies in the services layer 
3. Check if the models doesn't have dependencies towards service package or repository package 
4. Check if no generic Exceptions are thrown