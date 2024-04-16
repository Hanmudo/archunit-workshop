---
title: "Workshop: implement ArchUnit in your Java Spring Boot project" 
revealOptions:
  transition: 'none'
---

# Project Setup

- Clone GitLab repository [Demo project]("https://gitlab.com/RickyvanRijn/archunit-spring")
- Check if IDE is correctly configured
- Run application with docker through maven

<img src="img/ArchUnit-Logo.png">

---

# Project context 
The sample project we're using for the workshop is based on an API.

The API receives a call to get a plane ticket or train ticket.

---

# Configuration

Tasks:
- Run the Dockerfile with a build stage before starting the jar
- Install PlantUML plugins/extensions on your IDE

---

# Add ArchUnit dependency

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
# Tasks

- Add ArchUnit as dependency
- Add an ArchRule in an existing UnitTest
- Test if the project compiles


