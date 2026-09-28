# Java 6 OOP Exam — Comprehensive Practical (4 Variants)

This repository contains the **final Object-Oriented Programming (OOP) practical exam** for 2nd-year Informatics students.

The exam assesses practical understanding of:

- Java 6 OOP fundamentals
- inheritance and abstraction
- interfaces and polymorphism
- file I/O
- exception handling
- JSON parsing
- collections
- defensive programming
- data validation
- business logic
- Git usage
- reasoning about imperfect real-world data

Each student or group will be assigned **one of four real-world exam variants of comparable complexity**.

---

## Exam variants overview

| Variant | Topic | JSON theme | Difficulty | GUI |
|---|---|---|---|---|
| 1 | **Webshop Order System** | Orders, items, customers, transactions | Medium–Hard | Required for grade 10 |
| 2 | **Car Service Intake System** | Vehicles, repairs, diagnostics, invoices | Medium–Hard | Required for grade 10 |
| 3 | **Heavy Machinery Parts & Dismantling** | Tractors, bulldozers, parts, compatibility, second-hand machines | Medium–Hard | Required for grade 10 |
| 4 | **Warehouse Management** | Products, suppliers, stock movements | Medium–Hard | Required for grade 10 |

Each variant contains:

- `data.json` — realistic nested JSON input
- `README.md` — variant-specific requirements and grading criteria
- intentionally invalid or inconsistent data
- required report output
- invalid-record output
- business tasks that require processing the supplied data

---

## Repository structure

```text
/
├── variant_1_webshop/
│   ├── data.json
│   └── README.md
│
├── variant_2_car_service/
│   ├── data.json
│   └── README.md
│
├── variant_3_heavy_machinery/
│   ├── data.json
│   └── README.md
│
├── variant_4_warehouse/
│   ├── data.json
│   └── README.md
│
└── README.md
```

---

## Technical environment

The exam must be completed using:

- **Java 6**
- **NetBeans**
- standard Java 6 APIs
- an external JSON parser compatible with Java 6

Recommended JSON libraries include:

- Gson compatible with Java 6
- `org.json`

The following are not allowed:

- Java 8 or newer language features
- streams
- lambda expressions
- method references
- `java.time`
- Java 8 collection utilities unavailable in Java 6

Students are responsible for ensuring that any external library used is compatible with Java 6.

---

## Learning objectives

Students must demonstrate the following competencies.

### Class design and encapsulation

Students must demonstrate:

- appropriate classes for the domain
- encapsulation
- private fields where appropriate
- getters and setters
- constructors
- appropriate access modifiers
- separation of responsibilities between classes

### Inheritance and abstraction

Each solution must contain at least one abstract base class.

Example:

```java
public abstract class BaseEntity {

    protected String id;

    public abstract String businessKey();
}
```

The concrete hierarchy must represent meaningful domain concepts.

Inheritance must not exist only to satisfy the exam requirement.

### Interfaces

Students must implement at least **two meaningful interfaces**.

Interfaces must participate in application logic.

Declaring an empty interface or implementing an interface without ever using the interface type does not satisfy this requirement.

Possible examples include:

```java
Identifiable
Billable
Sellable
Compatible
Dismantlable
```

The appropriate interfaces depend on the assigned variant.

### Polymorphism

Students must demonstrate polymorphism using:

- abstract class references, or
- interface references

At least two parts of the application must operate on an abstraction rather than only on concrete classes.

Example:

```java
ArrayList<Sellable> items;
```

or:

```java
public static void printPrice(Sellable item) {
    System.out.println(item.getSellingPrice());
}
```

The actual concrete object must determine the behavior where appropriate.

### Overriding

Students must override methods where appropriate.

Required examples include:

```java
toString()
equals(Object)
hashCode()
businessKey()
```

Subclasses should override domain behavior where meaningful.

### Equality and business keys

`equals(Object)` must compare objects using a meaningful business key.

Students must document in a short comment what they selected as the business key.

Example:

```java
// Business key: partNumber because it uniquely identifies a part
```

`hashCode()` must be consistent with `equals()`.

### Overloading

Students must demonstrate:

- at least one overloaded constructor
- at least one overloaded method

Example:

```java
calculatePrice()
calculatePrice(double discount)
```

### Static members

At least one meaningful static member must be used.

Examples:

- object counter
- registry
- generated identifier sequence
- shared utility state

A static member added but never used does not satisfy the requirement.

---

## Collections

`ArrayList` must be the primary collection used for the main domain objects and business operations.

Students must demonstrate:

- adding objects
- iterating through collections
- filtering
- searching
- grouping or combining data where required
- sorting where required by the business task

`Map` may be used where justified, but must not replace `ArrayList` as the primary structure for the core exam tasks.

Students may use any Java 6-compatible sorting approach appropriate for their solution.

---

## JSON parsing

Each application must read its supplied:

```text
data.json
```

from disk using `FileReader`.

Example:

```java
FileReader reader = new FileReader("data.json");
```

Proper exception handling is mandatory.

The supplied JSON files intentionally contain a mixture of:

- valid records
- missing values
- invalid values
- incorrect data types
- inconsistent JSON structures
- duplicate business identifiers
- invalid references
- suspicious but potentially valid business data

Students must not assume that successful JSON parsing means that the data is valid.

They must distinguish between:

```text
valid JSON syntax
valid Java object structure
valid business data
```

---

## Defensive parsing

Some records are intentionally structured incorrectly.

Examples may include:

- a field that normally contains an array containing a string instead
- a numeric field containing incompatible data
- an object reference pointing to a non-existing entity
- duplicated business identifiers
- missing fields
- null values
- unexpected enum-like values

A single invalid record must not unnecessarily terminate processing of all valid records.

Students are expected to handle parsing errors using appropriate exception handling and continue processing valid data where reasonably possible.

Simply calling:

```java
gson.fromJson(reader, Root.class);
```

and allowing the entire application to terminate because of one malformed record is not considered defensive parsing.

Students may choose their own parsing strategy.

They must be able to explain that strategy during evaluation.

---

## Validation

Every variant requires a custom checked exception:

```java
DomainValidationException
```

Example:

```java
public class DomainValidationException extends Exception {

    public DomainValidationException(String message) {
        super(message);
    }
}
```

Domain validation must be separate from basic JSON parsing where appropriate.

For example:

```json
"quantity": -5
```

may be perfectly valid JSON and may deserialize correctly into Java while still being invalid according to the business rules.

Students must identify such cases themselves.

Depending on the situation, invalid data may:

- reject the complete record
- generate a warning
- use a justified default value
- be excluded from a calculation

Students must be able to justify important validation decisions.

---

## Important distinction: parsing vs validation

Students are expected to understand the difference between structural parsing problems and domain validation problems.

### Example 1 — structural problem

Expected:

```json
"compatibleModels": ["D6T", "D6R"]
```

But supplied:

```json
"compatibleModels": "D6T"
```

This may cause Gson deserialization to fail if the Java model expects:

```java
ArrayList<String> compatibleModels;
```

This must be handled as a parsing problem.

### Example 2 — domain validation problem

```json
"quantity": -5
```

This may deserialize successfully into:

```java
int quantity;
```

but should still be detected as invalid business data.

The student is responsible for recognizing both categories.

---

## File I/O

Each variant requires at least three file-related operations.

### Input

```text
data.json
```

### Main output

```text
report.txt
```

This must contain the detailed results of the business tasks.

### Invalid data output

Depending on the variant:

```text
invalid_items.txt
```

or another equivalent filename defined by the variant README.

The invalid-data file must contain enough information to identify:

- the problematic record
- the reason it was rejected or flagged

---

## Error handling

Students must demonstrate appropriate handling of:

- `FileNotFoundException`
- `IOException`
- JSON parsing exceptions
- custom domain validation exceptions
- invalid references between objects where applicable

Empty catch blocks are not acceptable.

The application must not silently ignore important errors.

Example:

```java
try {
    validateItem(item);
} catch (DomainValidationException e) {
    // write invalid item and reason to file
}
```

---

## Business logic

Each variant contains domain-specific tasks.

### Variant 1 — Webshop Order System

Possible tasks include:

- calculating order totals
- validating transactions
- processing customers
- checking products
- computing purchase totals
- detecting invalid orders or items

### Variant 2 — Car Service Intake System

Possible tasks include:

- calculating repair costs
- handling diagnostics
- processing service records
- calculating invoice totals
- evaluating vehicle histories
- detecting invalid service records

### Variant 3 — Heavy Machinery Parts & Dismantling

The domain contains:

- tractors
- bulldozers
- new parts
- second-hand parts
- machines for resale
- machines purchased for dismantling
- compatibility between parts and machines

Possible tasks include:

- calculating inventory value
- separating new and used parts
- identifying compatible parts
- calculating dismantling value
- calculating potential salvage profit
- identifying machines worth dismantling
- detecting duplicate parts
- detecting invalid source-machine references
- processing questionable or invalid machine data

Not every unusual machine or part is automatically invalid.

For example:

- an old tractor can still be valid
- a part with zero stock may simply be out of stock
- a selling price lower than its purchase price may be financially undesirable but still valid data
- a second-hand part may not necessarily have originated from a machine currently present in inventory

Students must make reasonable validation decisions and be prepared to explain them.

### Variant 4 — Warehouse Management

Possible tasks include:

- calculating inventory totals
- processing suppliers
- processing stock movements
- detecting low-stock products
- validating incoming and outgoing quantities
- detecting inconsistent warehouse records

---

## Critical thinking

The supplied datasets intentionally contain records that require interpretation.

Not every unusual value is automatically invalid.

Students are expected to distinguish between:

- technically malformed data
- clearly invalid business data
- unusual but valid data
- incomplete data
- data requiring a business decision

Examples:

- an old machine is not automatically invalid
- a product with zero stock is not necessarily invalid
- a selling price lower than purchase price is not necessarily malformed data
- an empty optional field may be acceptable
- a missing mandatory identifier may invalidate an entire record
- a reference to a missing object may require rejection or a warning depending on the business rule

Students should not invent arbitrary validation rules merely to remove inconvenient data.

Important decisions should be justifiable from the domain and supplied dataset.

---

## AI usage

AI tools may be used during the exam unless specifically restricted by the instructor.

Using AI does **not** remove the requirement to understand the submitted solution.

Students are responsible for:

- every class they submit
- every method they submit
- every library they use
- every validation decision
- every algorithm
- every generated line of code

During evaluation, students may be asked to:

- explain any part of their code
- explain why a class hierarchy was chosen
- explain an interface
- explain parsing or validation logic
- identify a bug
- modify a method
- change a validation rule
- add a small new requirement
- change how an invalid record is handled

A solution that runs correctly but cannot be explained or modified by the student does not demonstrate the required understanding.

---

## Git requirements

Each project must be stored in a Git repository.

At minimum, the commit history must demonstrate the development process.

Expected logical stages include:

1. initial project
2. JSON parsing
3. OOP model
4. business logic
5. final solution

Commit names do not need to match these exact words, but they should clearly describe the work completed.

Example:

```text
Initial project setup
Add Gson parsing
Implement domain hierarchy
Add validation and business logic
Add report generation and GUI
```

A repository containing only one final commit does not satisfy the Git requirement.

---

## GUI requirement

For grade 10, each variant requires a simple Java Swing GUI.

The GUI should provide a visual representation of meaningful domain data and at least one interaction.

Possible Swing components include:

- `JTable`
- `JComboBox`
- `JButton`
- `JLabel`
- `JTextArea`
- `JTextField`

Possible GUI features include:

- filtering
- selecting records
- calculating values
- displaying details
- showing results
- filtering by category, type, customer, vehicle, machine, supplier, etc.

The GUI does not need advanced styling.

Correct behavior and integration with the OOP model are more important than appearance.

Use **Swing** for the exam GUI.

---

## Evaluation method

The instructor will evaluate each project directly in NetBeans.

Evaluation includes:

1. opening the repository
2. reviewing Git history
3. compiling the project
4. running the application
5. testing JSON parsing
6. checking generated files
7. checking invalid-data handling
8. reviewing the OOP structure
9. checking required business tasks
10. testing the GUI where required

Students will also answer questions about their implementation.

Possible questions include:

- Why did you create this class?
- Why did you use inheritance here?
- Why is this an interface rather than a parent class?
- What is the business key of this entity?
- How does `equals()` work?
- Why did you reject this JSON record?
- Why did you accept this unusual value?
- What happens when Gson encounters this field?
- What is the difference between parsing and validation?
- Why does this method throw `DomainValidationException`?
- What would happen if this field were missing?
- How did you process or sort the required results?
- Where is polymorphism used?
- What does this static member represent?
- Why did you model this field as an `ArrayList`?
- Why did you choose this validation rule?

The instructor may request a small modification during evaluation.

Examples:

```text
Change the sorting from ascending to descending.
```

```text
Reject quantities greater than 100.
```

```text
Add another supported machine type.
```

```text
Allow one additional product condition.
```

```text
Change a validation error into a warning.
```

The purpose is to verify that the student understands the submitted solution.

---

## Notes for students

- Work independently.
- Copied submissions may be disqualified.
- Keep the project organized.
- Commit regularly.
- Use meaningful Git commit messages.
- Follow Java naming conventions.
- Classes should normally use `PascalCase`.
- Methods and variables should normally use `camelCase`.
- Do not optimize for line count.
- Do not create unnecessary classes only to satisfy requirements.
- Prefer understandable code over unnecessarily complicated solutions.
- Handle invalid input deliberately.
- Do not assume the supplied data is perfect.
- Read the complete variant README before starting.
- Be prepared to explain any submitted code.
- Be prepared to modify your solution during evaluation.

---

## Important restrictions

Full credit cannot be awarded when the solution contains major violations such as:

- Java 8+ features
- streams or lambda expressions
- libraries incompatible with Java 6
- no abstract class
- missing required interfaces
- interfaces that are never used in logic
- meaningless inheritance added only to satisfy the requirement
- no meaningful polymorphism
- no custom checked `DomainValidationException`
- no defensive error handling
- application terminates because of the first invalid data record
- no `ArrayList`-based core processing
- missing `equals()` or `hashCode()`
- missing report output
- missing invalid-data output
- no Git commit history
- student cannot explain or modify significant parts of the submitted solution

---

## General grading philosophy

The exam does not evaluate only whether the final program produces the expected numbers.

The solution is evaluated based on:

- correctness
- OOP design
- code structure
- defensive programming
- exception handling
- data validation
- use of abstractions
- understanding of the domain
- ability to reason about imperfect input
- ability to explain technical decisions
- ability to modify the submitted implementation

A program that produces correct output using poor OOP design is not equivalent to a well-designed OOP solution.

Likewise, successfully parsing `data.json` does not prove that the supplied data has been correctly understood or validated.

The goal is not only to make the program work.

The goal is to demonstrate that the student understands **why it works, what can fail, and how the design handles those failures**.

---

_Repository maintained for educational use at the University of Medicine, Pharmacy, Science and Technology “George Emil Palade” Târgu Mureș — Informatics, Year 2._
