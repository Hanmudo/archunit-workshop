---
title: "Workshop: implement ArchUnit in your Java Spring Boot project"
revealOptions:
  transition: 'none'
---

# Part 3: Implement Intermediate Rules
Based on dependencies of

- Plain Java
- Junit4
- Junit5

---

## What is an intermediate rule

An intermediate rule is based on a pattern or antipattern

---

### Intermediate rule 1: A common antipattern in microservice architectures

A common pitfall with microservice architecture is the wrong usage of objects from domain libraries.
E.g. The usage of Train domain objects in the Plane service

```java 
@Test
public void domainClassesShouldNotDependOnEachOther() {
    SlicesRuleDefinition.slices()
            .matching("example.(*service).domain")
            .should().notDependOnEachOther()
            .check(classes);
}
```
---

### Intermediate rule 2: Onion Architecture

<img src="../img/onionarchitecture.png" width="200"/>

Onion architecture is a software design pattern that emphasizes the separation of concerns in building applications

---

### Intermediate rule 2: Onion Architecture

> Define the packages which resemble the domainModels, domainServices, etc. 

```java
@Test
public void onion_architecture_is_enforced() {
    onionArchitecture()
            .domainModels("..domain.model..")
            .domainServices("..domain.service..")
            .applicationServices("..application..")
            .adapter("cli", "..adapter.cli..")
            .adapter("persistence", "..adapter.persistence..")
            .adapter("rest", "..adapter.rest..")
            .check(classes);
}
```

---

### Intermediate rule 3: Layered architecture

Use to configure layers from access to other layers.

Exceptions can be made if necessary.

```java
@Test
public void layer_dependencies_are_enforced() {
    layeredArchitecture().consideringAllDependencies()

            .layer("Controllers").definedBy("com.tngtech.archunit.example.layers.controller..")
            .layer("Services").definedBy("com.tngtech.archunit.example.layers.service..")
            .layer("Persistence").definedBy("com.tngtech.archunit.example.layers.persistence..")

            .whereLayer("Controllers").mayNotBeAccessedByAnyLayer()
            .whereLayer("Services").mayOnlyBeAccessedByLayers("Controllers")
            .whereLayer("Persistence").mayOnlyBeAccessedByLayers("Services")

            .check(classes);
}
```
---
### Intermediate rule 3: Layered architecture

Visual representation of the layered architecture or n-tier architecture.

<img src="../img/layered_common.svg" width="200"/>

---

## implement testcases

- Implement microservices antipattern by implementing service A within Service B and vice versa
- Implement Onion architecture archtest by refactoring 
- Implement Layered architecture archtest by refactoring


