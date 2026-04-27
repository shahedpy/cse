# Software Estimation

Software Project Estimation is the process of estimating various resources required for the completion of a project.  
Estimation is the process of finding an estimate, or approximation, which is a value that can be used for some purpose even if input data may be incomplete, uncertain, or unstable.  
Effective software project estimation is one of the most challenging and important activities in software development. Proper project planning and control is not possible without a reliable estimate. The software industry doesn’t estimate projects well and doesn’t use estimates appropriately.  

The four basic steps in software project estimation are:
1. **Estimate the size of the development product:** The size can be estimated by using either Lines of Code (LOC) or Function Points (FP).
2. **Estimate the effort** in person-months or person-hours (man-month or man-hour). Man-month is an estimate of personal resources required for the project.
3. **Estimate the schedule** in calendar days /months/ years based on total man-month required and manpower allocated to the project.
4. **Estimate the project cost** in local currency.

## COCOMO (Constructive Cost Model)

The Constructive Cost Model or COCOMO Model estimates the cost for any software development project based on the empirical data obtained from observations and uses a mathematical formula to estimate these parameters.

Software projects under **COCOMO model strategies** are classified into three categories: **Organic**, **Semi-Detached**, and **Embedded**.

## Organic
A software project is said to be an **organic type** if:
- Project is small and simple.
- Project team is small with prior experience.
- The problem is well understood and has been solved in the past.
- Requirements of projects are not rigid.

**Example:** Payroll processing system.

## Semi-Detached
A software project is said to be a **semi-detached type** if:
- Project has complexity.
- Project team contains both experienced and inexperienced members.
- The project has intermediate size and mixed rigid requirements.

**Examples:**
- Transaction processing system (fixed requirements)
- Database Management System (DBMS)
- New unknown operating system
- Difficult inventory management system

## Embedded
A software project is said to be an **embedded type** if:
- Project has fixed requirements of resources.
- Product is developed within very tight constraints.
- Requires the highest level of complexity, creativity, and experience.
- Needs a larger team size than the other two models.

> Three Types of COCOMO model
<img alt="Types-of-COCOMO-Models.png" data-hpc="true" src="https://github.com/shahedpy/cse/blob/main/software_engineering/images/Types-of-COCOMO-Models.png?raw=true" style="max-width: 100%;">

# Basic COCOMO Model

The **Basic COCOMO Model** provides a rough estimate of any project based on the size of the software alone.  
It is suitable for small to medium-sized projects with straightforward requirements.

The model uses constants derived from software project types and defines three modes of development:
- **Organic**
- **Semi-detached**
- **Embedded**

---

## Estimation Formulas



\[
E = a \cdot (KLOC)^b \quad \text{person-months}
\]





\[
D = c \cdot (E)^d \quad \text{months}
\]





\[
P = \frac{E}{D} \quad \text{persons}
\]





\[
\text{Productivity} = \frac{KLOC}{E} \quad \text{KLOC per Person-month}
\]



Where:
- \(E\) = effort applied in person-months  
- \(D\) = development time in months  
- \(P\) = total number of persons required to accomplish the project  
- Productivity = how many lines of code a person can write in one month  

---

## Constants for Basic Model

| Software Project | a   | b    | c   | d    |
|------------------|-----|------|-----|------|
| Organic          | 2.4 | 1.05 | 2.5 | 0.38 |
| Semi-detached    | 3.0 | 1.12 | 2.5 | 0.35 |
| Embedded         | 3.6 | 1.20 | 2.5 | 0.32 |

---

## Practice Problems

1. A software project requires **1000 lines of code** for development.  
   The project is categorized as **organic type**.  
   Using the basic COCOMO model, calculate:
   - Estimated effort  
   - Development time  
   - Number of persons required  
   - Productivity  

2. A software system has **1500 lines of code**.  
   The project is classified as **semi-detached**.  
   Using the basic COCOMO model, calculate:
   - Estimated effort  
   - Development time  
   - Number of persons required  
   - Productivity  

3. A company is estimating the effort for a new software system with **2000 lines of code**.  
   The system is of **embedded type**.  
   Using the basic COCOMO model, calculate:
   - Estimated effort  
   - Development time  
   - Number of persons required  
   - Productivity  

