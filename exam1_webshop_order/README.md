# Webshop Order — Java 6 OOP Exam

Time limit: 90 minutes. Java 6. NetBeans. No Java 8 features. No streams. No java.time.
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
- Compute order totals with taxes and discounts per line.
- Identify digital/service items vs physical items and compute shipping eligibility.
- Apply extra 5% discount to GOLD customer on physical goods only.
- Output items sorted by total line value.

## Required design elements
- Abstract class `BaseEntity` and interfaces used in logic.
- Class hierarchy must reflect polymorphism in data (item types / work order types / course types / movement types).
- Two places must use interfaces/abstracts directly in logic, not only as markers.

## Overloading / overriding
- Provide at least one overloaded constructor and one overloaded method.
- Override `toString`, `equals`, `hashCode`. Equals must use business key.

## Output
- Print a concise summary to console.
- Write `report.txt` with full details.

- GUI: Swing / FX / Android panel to edit quantity of an item with live recompute and per-line discount visibility.
## Constraints that invalidate full credit
- Use of Java 8+ features or incompatible libs.
- Using Map as the main structure for core tasks instead of ArrayList.
- No custom checked exception.
- No Git commits history.


