# Car Service Intake — Java 6 OOP Exam

Time limit: 120 minutes. Java 6. NetBeans. No Java 8 features. No streams. No java.time.
You may use an external JSON parser (e.g., Gson ≤ 2.2.x or org.json).

## Mandatory
1. Parse `data.json` from disk using FileReader with exception handling.
2. Design an OOP model with:
   - One abstract base class `BaseEntity` with `id` and abstract `String businessKey()`.
   - At least two interfaces used meaningfully (e.g., `Identifiable`, domain-specific like `Billable`/`Schedulable`/`Movable`).
   - Inheritance hierarchy with at least two concrete subclasses.
   - Static member used as registry or counter.
   - Method overloading and overriding. Override `toString()`.
   - Implement `equals(Object)` and `hashCode()` using the business key (document it in comments).
   - Use `ArrayList` as primary collection. Sorting via `Comparator`.
3. I/O:
   - Read `data.json`.
   - Write a `report.txt` with results.
4. Error handling:
   - Custom checked exception `DomainValidationException` for invalid data.
   - Defensive parsing: missing fields → handled gracefully with defaults or exceptions.
5. Git:
   - Initialize a repository. At minimum: initial commit, parsing commit, OOP model commit, final commit.

## Business tasks
- Compute labor and parts cost per work order and overall subtotal.
- If OBD contains P0420 or oil pressure not OK, flag 'Do Not Release'.
- Courtesy car daily fee 15 EUR applies if `meta.courtesyCar` true, max 5 days.
- Output prioritized issues by severity (HIGH > MEDIUM > LOW).

## Required design elements
- Abstract class `BaseEntity` and interfaces used in logic.
- Class hierarchy must reflect polymorphism in data (item types / work order types / course types / movement types).
- Two places must use interfaces/abstracts directly in logic, not only as markers.

## Overloading / overriding
- Provide at least one overloaded constructor and one overloaded method.
- Override `toString`, `hashCode`. 

## Output
- Print a concise summary to console.
- Write `report.txt` with full details.

- GUI: Swing / FX / Android wizard (Next/Back) to select issues and show an estimated quote table.
## Constraints that invalidate full credit
- Use of Java 8+ features or incompatible libs.
- Using Map as the main structure for core tasks instead of ArrayList.
- No custom checked exception.
- No Git commits history.
