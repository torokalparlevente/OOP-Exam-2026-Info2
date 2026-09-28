# Warehouse Management — Java 6 OOP Exam (Offline Edition)

**Duration:** 90 minutes  
**Tools:** NetBeans 8 or earlier, Java 6 SDK only  
**Internet:** Not allowed  
**External libraries:** Not allowed (no Gson, Jackson, etc.)  

You will process a local JSON file named `data.json`.  

---

## 1. Objectives

Apply the main OOP principles:

- Abstract class and one interface  
- Inheritance, overriding, overloading  
- `ArrayList` usage  
- Static members  
- File I/O 
- Proper `toString()` methods  

---

## 2. Classes to implement

1. **`BaseEntity`** (abstract)  
   - Field: `id`  
   - Abstract method: `String businessKey()`  

2. **`Supplier`**, **`Product`**, **`StockMovement`**, **`Warehouse`**  
   - Extend or contain `BaseEntity` as appropriate  
   - Override `toString()`  

3. **`Printable`** (interface)  
   - Method: `void printSummary()`  

---

## 3. Suggested class structure (hint)

```java
abstract class BaseEntity {
    protected String id;
    public BaseEntity(String id) { this.id = id; }
    public abstract String businessKey();
}

interface Printable {
    void printSummary();
}

class Supplier extends BaseEntity { ... }
class Product extends BaseEntity { ... }
class StockMovement extends BaseEntity { ... }
class Warehouse extends BaseEntity implements Printable { ... }
```

- Use **overloading** for methods such as  
  `adjustStock(int qty)` and `adjustStock(StockMovement m)`.
- Use **static members**, e.g. `movementCounter` in `Warehouse`.

---

## 4. Tasks

1. **Read** `data.json` from disk.  
2. **Store** products, suppliers, and stock movements in `ArrayList`s.  
3. **Apply stock movements:**  
   - `IN` adds quantity  
   - `OUT` subtracts quantity  
4. **Compute** new stock per product.  
5. **Detect** products below `reorderPoint`.  
6. **Write** results to `report.txt` in this format:

   ```
   SKU | Name | Stock | Status
   HAM-100 | Hammer 16oz | 75 | OK
   NAI-50 | Nails 50mm | 70 | REORDER
   GLV-M | Work Gloves M | 20 | REORDER
   ```
7. **Print** the same summary to the console.  
8. **Use a static counter** to track how many stock movements were processed.  
9. **Handle errors gracefully** using `try–catch`.

---

## 5. Example output (`report.txt`)

```
WAREHOUSE: Targu Mures Central

Processed stock movements: 3

SKU | Name | Stock | Status
----------------------------------------
HAM-100 | Hammer 16oz | 75 | OK
NAI-50 | Nails 50mm | 70 | REORDER
GLV-M | Work Gloves M | 20 | REORDER
----------------------------------------
Total products: 3
Products below reorder: 2
```

---

## 6. Grading (max 10 points)

| Criterion | Points |
|------------|--------|
| JSON reading & error handling | 2 |
| Class design (abstract + interface) | 2 |
| Inheritance, overriding, overloading | 2 |
| Stock computation logic | 2 |
| File I/O and report output | 1 |
| Code structure & style | 1 |
| **Total** | **10** |

---


## 7. Restrictions

- No internet or AI tools.  
- Work individually; projects will be checked line by line.


