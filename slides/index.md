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

### What is ArchUnit about?

[<img src="img/ArchUnit-Logo.png" width="300"/>](image.png)

> Plain Java

> JUnit compatible

---

## This is the way

> ArchUnit is created to test, assert and specify architectural rules.

> This can be a simple dependency, a design pattern or custom rules.

Let's UnitTest our architecture!

---

## Basic project setup

> First start with checking our example project

Dockerfile phases:
- Maven build + test
- Start application

> Task: Add ArchUnit to the project 

[Go to project setup](/projectsetup.md)

Note:
Use the Docker environment for the Dockerfile(s) in the projects

---

Basic rules (first tell something, then let people do)

Clone the following Git repository: ""
Implement the following basic rules:
- Check if the class of the plannerService has dependencies in the repository layer
- Check if the models doesn't have dependencies towards service package or repository package

Note: 
Check for the right usage of packages
---

Intermediate rules

- Check on patterns and anti-patterns

Note:
The intermediate rules are for checking on patterns and anti-patterns

---

Integrate in build process

* Maven build and test

Note: Old concurrency the thread was a wrapper around an OS thread. The loom variant has taken control towards inside the JVM.

---

Advanced rules

- Implement custom rules based on the ArchRule API
- Implement check on design patterns or guidelines
- Use of PlantUML file

---

Continuous Integration
- Freeze for performance (Heap memory)
- Freeze default
---

Best practices + Community

- Create a artifact of the architectural tests for easy maintenance
- Get connected in the wide community of ArchUnit/PlantUML


---

The End.
Questions?
