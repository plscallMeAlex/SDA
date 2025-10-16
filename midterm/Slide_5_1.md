# Measuring and Governing Arch Char.
Metrics ตัวชี้วัด used to measure the arch char.
Tests used to govern chosen architecture characteristics.
**Govern ?** - กำกับ take care of the arch char that applied to the systems and monitor the char it happened like the document not fake.
## Measuring
For automation governance have a wide enterprise objective for characteristics.
Need to define a precise metrices for each characteristic.
### Operational Measures
Used to measure the operational characteristics like **performance, scalability, elasticity, availability, reliability**
**Example**
- Performance -> average response time of API < 200ms
Using a **runtime metrics**
### Structural Measures
Used to measure the structural characteristics like **modularity, coupling, cohesion**.
**Example**
- Cyclomatic Complexity (CC) -> code level metric for code quality if CC < 10 = acceptable.
Using metric for seeing in the code structure (วัดโครงสร้างจากสูตรที่จารให้ช่วงแรก)
### Process Measures
Use with composite characteristics that connect with the development process.
**Example**
Agility = Testability + Deployability + Maintainability
- Test... -> code coverage of unit test
- Deploy -> success rate deploy, time taken for deploy
- Maintain -> time take to change something in the code.
Using metric from development pipeline/process (วัดทีม dev ทำงานเร็วแค่ไหน)

## Governing Architecture Characteristics
It used to indicate your architecture is surely have this characteristics or not and can provide it all the time ?
- Measure
- Test
- Govern
It used the mechanism to make the design is archive the aims or not by **Fitness Function**
### Fitness Function
It the mechanism to integrity the objective assessment whether it reach the goals of characteristics or the combinations one or not having a lot of tool to integrity. It separate into this
- **Atomic Fitness Function** - handle a single characteristics like performance test of API.
- **Holistic Fitness Function** - handle the combination of characteristic like chaos testing -> availability + fault tolerance + resilience
#### JDepend
It a tool to analyze the dependencies between the packages and classes.
Purpose: **check structural characteristics** like modularity, coupling, and stability.
**Work ?**
- Scans compiled .class files.
- Build a dependency graph.
- Detects cyclic dependencies
- Report metrics like afferent coupling (who depend on me) and efferent coupling (who I depend on)
Fitness function: govern modularity.
#### ArchUnit
Testing lib for java
Purpose is to enforce architecture rules in code (ตรวจสอบการฝ่าฝืนกฎไหม เช่น ui เรียก db ตรงๆ)
How it works:
- Write a tests but instead of testing business logic, we test architecture constraints.
- **Example rule**
```java
@Test
void servicesShouldNotAccessControllers() {
    noClasses()
      .that().resideInAPackage("..service..")
      .should().accessClassesThat().resideInAPackage("..controller..")
      .check(importedClasses);
}
```
The code ensure the layered architecture is respected.
Fitness function: govern layering or modularity.
#### Chaos Engineering (Resilience)
- Netflix's Chaos Monkey -> random kill servers -> to check system's fault tolerance & availability
