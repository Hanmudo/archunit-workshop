---
title: "Workshop: implement ArchUnit in your Java Spring Boot project" 
revealOptions:
  transition: 'none'
---

# Part 5: Implement Advanced Rules

- Create custom rule
- Run an Archtest with a PlantUML diagram

---

## What is an advanced rule

An advanced rule is based on a customization or external party

---

### Advanced rule 1: A custom ArchRuleDefinition

A common pitfall with microservice architecture is the wrong usage of objects from domain libraries.

E.g. The usage of Train domain objects in the Plane domain object(s)

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

### Advanced rule 2: Use a PlantUML diagram

A PlantUML diagram can be used for an ArchTest.

Make sure you exclude the java jdk packages to validate.

```java
private final JavaClasses classes = new ClassFileImporter().importPackages("com.tngtech.archunit.example.shopping");
private final URL plantUmlDiagram = PlantUmlArchitectureTest.class.getResource("shopping_example.puml");

@Test
public void classes_should_adhere_to_shopping_example_considering_only_dependencies_in_diagram() {
    classes().should(adhereToPlantUmlDiagram(plantUmlDiagram, consideringOnlyDependenciesInDiagram()))
            .check(classes);
}
```
---
### Advanced rule 3: Create a PlantUML diagram

>- Download PlantUML and start it or use docker
>   - https://github.com/plantuml/plantuml-server
>   - `docker run -d -p 8080:8080 plantuml/plantuml-server:jetty`
> More on the next slide >>

---
### Install PlantUML

> - https://plantuml.com/download
    >   - Intellij Plugin: https://plugins.jetbrains.com/plugin/7017-plantuml-integration
>   - Eclipse Plugin: https://plantuml.com/eclipse
>   - Live Editor > https://github.com/plantuml/plantuml-server
>
> Dependency of PlantUML: https://graphviz.org/download/
> 
> When a error occurs of the **dot** application, you'll need to (re-)install graphviz
---
## Implement testcases

- Create a custom archrule 
- Implement an ArchTest with the use of the given PlantUML diagram
- Implement an ArchTest with a custom created PlantUML
