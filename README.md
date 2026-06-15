# Academic Organization Ontology

An OWL 2 DL ontology built using Protégé to model the domain of an academic institution, including its members, programs, courses, and examination structures. This project demonstrates semantic modeling, class hierarchies, property restrictions, and automated reasoning.

## 🌐 Ontology IRI
`http://www.example.org/academic-organization`

## 🏗️ Ontology Architecture

### 1. Class Hierarchy (Taxonomy)
* `Person` (Disjoint: Student, Professor, AdministrativeStaff)
  * `Student`
  * `Professor`
  * `AdministrativeStaff`
* `Organization`
  * `Department`
* `AcademicProgram`
* `Course`
* `Classroom`
* `Exam`
* `DegreeLevel`
  * `Bachelor`
  * `Master`

### 2. Properties, Domains, and Ranges
* **Object Properties:**
  * `enrolledIn` (Domain: `Student` -> Range: `Course`)
  * `teaches` (Domain: `Professor` -> Range: `Course`)
  * `belongsToDepartment` (Domain: `Professor` -> Range: `Department`)
  * `offeredBy` (Domain: `Course` -> Range: `Department` [Exactly 1])
  * `partOfProgram` (Domain: `Course` -> Range: `AcademicProgram`)
  * `studiesIn` (Domain: `Student` -> Range: `AcademicProgram`)
  * `takesExam` (Domain: `Student` -> Range: `Exam`)
  * `examForCourse` (Domain: `Exam` -> Range: `Course` [Exactly 1])
  * `heldIn` (Domain: `Course` -> Range: `Classroom`)
* **Data Properties:**
  * `hasName` (Domain: `Person` -> Range: `xsd:string`)
  * `studentID` (Domain: `Student` -> Range: `xsd:string`)
  * `employeeID` (Domain: `Professor` -> Range: `xsd:string`)
  * `courseCode` (Domain: `Course` -> Range: `xsd:string`)
  * `credits` (Domain: `Course` -> Range: `xsd:integer`)
  * `examDate` (Domain: `Exam` -> Range: `xsd:date`)

### ⚡ 3. Advanced Reasoning & Defined Classes
* **`ActiveStudent`**: Defined as a logical equivalent class: 
  `Student and (enrolledIn some Course)`

## 🧠 Reasoning Verification
Using the **HermiT 1.4.3** Description Logic reasoner, individuals are dynamically classified based on their contextual attributes rather than manual assignment:
* **Asserted State:** Individuals `ImanolAbbete`, `Sofia`, and `UsmanRais` are declared as basic `Student` instances. Only `UsmanRais` is explicitly asserted with an `enrolledIn` relationship to a `Course`.
* **Inferred State:** Upon executing the reasoner, the system automatically evaluates the definitions and infers that **only** `UsmanRais` belongs to the `ActiveStudent` class.

## 📁 Files Included
* `academic-organization.owl`: The structural OWL/XML file containing all axioms.
* `screenshots/`: Visual verification of the active reasoner and inferred classification.
