---
title: "Workshop: implement ArchUnit in your Java Spring Boot project" 
revealOptions:
  transition: 'none'
---

Workshop: implement ArchUnit in your Java Spring Boot project

<img src="img/ArchUnit-Logo.png">

By: Ricky van Rijn

---

<div style="display: flex; justify-content: center; align-items: center;">
<h3>Ricky van Rijn, Practice Lead JTech</h3>
</div>

<div style="display: flex; justify-content: center; align-items: center;">
    <img src="img/profileRicky.jpg" width="200"/>
</div>

<div>
    <div style="display: flex; justify-content: center; align-items: center;">
        <img src="img/github.svg" width="32"/> 
        : @Hanmudo
    </div>
    <div style="display: flex; justify-content: center; align-items: center;">
        <img src="img/x.svg" width="32"/>
        : @RickyvanRijn
    </div>
</div>

Work experience: Java for 10+ years <br />
Hobby's: Taekwondo, Hapkido, Fitness, Robotics

---

## Why this workshop?

- Customer project
- Lot of deprecated documentation
- Lot of different architecture designs
- Code != Architecture

> Note that the example project is completely fictional

---

## What about you?
> - Who has already looked into ArchUnit?
> - Who has a worked with PlantUML?
> - Who thinks architectural tests are useful?

Note:
- Who has already looked into ArchUnit?
- Who's familiar with the book "Gang of four" based on Design Patterns?
- Who thinks architectural tests are useful?

---

## Why use ArchUnit?

> Why test the architecture?

> Who's behind? Architecture or Development?

> Clean architecture/ Clean code

---

### What is ArchUnit about?

[<img src="img/ArchUnit-Logo.png" width="300"/>](image.png)

> Plain Java

> JUnit4/5 compatible

---

## What does ArchUnit

> ArchUnit library is created to test, assert and specify architectural rules.

> This can be a simple dependency, a design pattern or custom rules.

---

## How does ArchUnit work behind the scenes?

> Analyzing bytecode

> Importing all files into a java code structure

---

## How does ArchUnit work in front of the scenes?

> - ArchRule
> - ClassFileImporter
> - FreezingArchRule
> - PlantUML diagram
> - Caching
>
---

### ArchRule

> The ArchRule object represents a rule to specify a set of object of interest
> 
> The ArchRule object is linked to ArchRuleDefinitions which you can use by the factory methods

---

### ArchRule part 2

> The ArchRule can be used to create a custom ArchRule
>
> The ArchRule can be given a custom object by specifying a transformer to handle the classes


---

### ClassFileImporter

> The ClassFileImporter object is mainly used by the plain java tests
> 
> Imports all classes for example from a package

---

### FreezingArchRule

> Similar to @Disable for unit tests but different
> 
> Stores violations in a Violation Store
> 
> Violation Store is text based
> 
> By default the rule is indicated with an UUID

---

### FreezingArchRule part 2

> The Violation Store name can be set through a property
> 
> The default filename is stored.rules
> 
> The default path can be set in the archunit.properties file in the test/resources folder
> 
> Violation Store can be persisted

---

### PlantUML diagram

> The ArchUnit library can use a puml file as source for ArchUnit tests
> 
> Architecture patterns are easiliy tested this way
> 
> Don't forget to ignore the java JDK dependencies

---

### Caching

> ClassFileImporter analyzes all imported classes
> 
> Larger projects take some time as the ClassFileImporter is often used on base package level
> 
> Use @AnalyzeClasses annotation with @ArchTest annotation for reuse of imported classes

---

### Slices

> Slices are subsets of classes that can be tested against another slice
>
> SliceRule and SliceRuleDefinition objects are used

---

## Part 1: Basic project setup

> First start with checking our example project

Dockerfile phases:
- Maven build + test
- Start application

> Task: Add ArchUnit to the project 

[Go to project setup](/slides/projectsetup/index.md)

Note:
Use the Docker environment for the Dockerfile(s) in the projects

---

## Part 2: Basic rules

The basic rules apply on simple cases with low complexity

[Go to basic rules](/slides/basicrules/index.md)

Note: 
Check for the right usage of packages
---

## Part 3: Intermediate rules

Check on patterns and antipatterns

[Go to intermediate rules](/slides/intermediaterules/index.md)

Note:
The intermediate rules are for checking on patterns and anti-patterns

---

## Part 4: Integrate in build process

* Debug and test
* Freeze for performance (Heap memory)
* Freeze default

[Go to CI/CD](/slides/cicd/index.md)

Note: Old concurrency the thread was a wrapper around an OS thread. The loom variant has taken control towards inside the JVM.

---

## Part 5: Advanced rules

- Implement custom rules based on the ArchRule API
- Implement check on design patterns or guidelines
- Use of PlantUML file

[Go to advanced rules](/slides/advancedrules/index.md)

---

## Best practices + Community

- Create a artifact of the architectural tests for easy maintenance
- Get connected in the wide community of ArchUnit/PlantUML


---

# The End.
## Questions?
