---
title: "Workshop: implement ArchUnit in your Java Spring Boot project" 
revealOptions:
  transition: 'none'
---
# Part 4: Integrate in build process
Integrate in build process / agile workflow

---

## Freeze

> Freeze is the forced passing of a rule and document for later use.
> 
> Violation Store holds all the frozen rules
> 
> Used when implementing ArchUnit in an existing project
> 
---

## Violation Store

- Create file archunit.properties in the folder src/test/resources
- Set the property in the src/test/resources/archunit.properties file:

```properties
freeze.store.default.path=src/test/resources/frozen
```
---
## Violation Store

> stored.rules is the default Violation Store filename. 
> 
> It's stored in the folder which we set earlier

---
## Freeze

> When an archtest is planned to resolve later
> 
> Use freeze(...) to store the violation and let it pass

```java
@Test
public void no_classes_should_use_the_EntityManager() {
    freeze(noClasses().should().dependOnClassesThat().areAssignableTo(EntityManager.class))
            .check(classes);
}
```
---
## AnalyzeClasses and ArchTest
> For more performance the analyzeclasses annotation can be used
> 
> This results in efficient memory usage due to reuse of classes

---
## Ignore Violations
> The ability to completely ignore Violations can be done in the archunit_ignore_patterns.txt file
> 
> This file is in the root folder of the claspath
---
## Ignore Violations
> The rules are inserted with a regex on each line

```regexp
# There are many known violations where LegacyService is involved; we'll ignore them all
.*some\.pkg\.LegacyService.*
```

---
## implement testcases

- Setup archunit.properties with a custom stored.rules path
- Implement an archtest which fails and freeze this
- <em>ADVICE: Use @AnalyzeClasses and @ArchTest in your test(s)</em>
- Implement an archtest which fails and **ignore** this violation