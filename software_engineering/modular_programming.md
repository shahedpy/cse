# Modular Programming

Modular programming is a way of writing software by breaking it into small, separate parts called modules, where each module does one specific job. These modules can work on their own and can be reused in other programs.

## Cohesion

Cohesion defines to the degree to which the elements of a module belong together. Thus, cohesion measures the strength of relationships between pieces of functionality within a given module. For example, in highly cohesive systems, functionality is strongly related. A module has high cohesion when all its functions are closely related and work together to perform one specific task. A module has low cohesion when its functions are unrelated or loosely related, doing different kinds of tasks.

## Coupling

In software engineering, the coupling is the degree of interdependence between software modules. Two modules that are tightly coupled are strongly dependent on each other. However, two modules that are loosely coupled are not dependent on each other. Uncoupled modules have no interdependence at all within them.  

A good design is the one that has low coupling. Coupling is measured by the number of relations between the modules. That is, the coupling increases as the number of calls between modules increase or the amount of shared data is large. Thus, it can be said that a design with high coupling will have more errors.

### Difference between Coupling and Cohesion

| **Cohesion** | **Coupling** |
|--------------|--------------|
| 1. Cohesion is the degree to which the elements inside a module belong together. | Coupling is the degree of interdependence between the modules. |
| 2. A module with high cohesion contains elements that are tightly related to each other and united in their purpose. | Two modules have high coupling (or tight coupling) if they are closely connected and dependent on each other. |
| 3. A module is said to have low cohesion if it contains unrelated elements. | Modules with low coupling among them work mostly independently of each other. |
| 4. Highly cohesive modules reflect higher quality of software design. | Loose coupling reflects the higher quality of software design. |

