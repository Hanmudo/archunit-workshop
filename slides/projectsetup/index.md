---
title: "Workshop: implement ArchUnit in your Java Spring Boot project" 
revealOptions:
  transition: 'none'
---

# Project Setup

- Clone GitLab repository <a href="https://github.com/Hanmudo/archunit-spring" target="_blank">https://github.com/Hanmudo/archunit-spring</a>
- Check if IDE is correctly configured
- Run application with docker through maven
- \> Or build and run with docker!

<img src="/img/ArchUnit-Logo.png">

---

# Project context 
The sample project we're using for the workshop is based on a Spring Boot API.

The API receives a call to get a ticket object concerning a plane or train.

---

## Configuration

Tasks:
- Run the Dockerfile with a build stage before starting the jar
  - or Run the mvn package docker:build docker:start command with a local maven installation
- (Optional) Install PlantUML plugins/extensions on your IDE

---

### Add ArchUnit dependency

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

## Create your first rule

Create and run your first test.

```java
@Test
public void my_first_architecture_rule() {
    JavaClasses importedClasses = new ClassFileImporter()
            .importPackages(
              "com.example.archunitspring.application.services"
            );

    ArchRule rule = classes()
            .that().resideInAPackage("..services..")
            .and().areAnnotatedWith(Service.class)
            .should().haveSimpleNameEndingWith("ServiceImpl");

    rule.check(importedClasses);
}
```

---
# Tasks

- Add ArchUnit as dependency
- Add an ArchRule in an existing UnitTest
- Test if the project compiles


