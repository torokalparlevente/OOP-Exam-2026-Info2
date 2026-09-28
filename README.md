# Java 6 OOP Exam — Comprehensive Practical (4 Variants)

This repository contains the **final Object-Oriented Programming (OOP)** exam for 2nd-year Informatics students.  
It is designed to assess understanding of **Java 6 OOP fundamentals**, **file I/O**, **exception handling**, and **JSON data processing** through **four real-world case studies** of comparable complexity.

Each student or group will be assigned **one of the four exam variants**.

---

## 🧭 Exam Variants Overview

| Variant | Topic | JSON Theme | Difficulty | GUI Bonus |
|----------|--------|-------------|-------------|------------|
| 1 | **Webshop Order System** | Orders, items, customers, transactions | Medium–Hard | Required for grade 10 |
| 2 | **Car Service Intake System** | Car repairs, diagnostics, invoices | Medium–Hard | Required for grade 10 |
| 3 | **University Course Management** | Students, courses, instructors, grades | Medium–Hard | Required for grade 10 |
| 4 | **Warehouse Management (Offline)** | Products, suppliers, stock movements | **Easy** | Optional bonus only |

Each variant includes:
- `data.json` — realistic, nested JSON input  
- `README.md` — exam description, objectives, and grading  
- Example output or report file  

---

## 📂 Repository Structure

```
/
├── variant_x_webshop/
│   ├── data_.json
│   ├── README.md
└── README.md   # This overview file
```

---

## 🎯 Learning Objectives

Students must demonstrate the following Java 6 OOP competencies:

- **Class Design** with encapsulation and proper access modifiers  
- **Inheritance and Abstraction** using `abstract` classes  
- **Interfaces** and implementation  
- **Overriding** (`toString`, `businessKey`)  
- **Overloading** (constructors and methods)  
- **Static Members** (counters, utilities)  
- **ArrayLists** for data structures  
- **File I/O** (read/write JSON and reports)  
- **Exception Handling** (`try–catch`, validation errors)  
- **GUI** -> **Swing / FX / Android GUI** (for variants 1–3 to get to grade 10)

---

## ⚙️ Evaluation Method

1. The instructor will open each student’s code in NetBeans.  
2. The program must **compile and run** without additional configuration.  
3. During review, students will answer questions about:
   - Their class design and OOP structure  
   - Error handling  
   - How inheritance and interfaces were used  
4. Grading will follow the official rubric in each variant README.

---

## 📘 Notes for Students

- Work independently. Collaboration or copied code leads to disqualification.  
- Keep your repository organized: commit regularly, use meaningful messages.  
- Follow Java naming conventions (PascalCase for classes, camelCase for methods).  
- Code will be checked for OOP consistency, not line count.

---

## 🏆 Variant 4 (Offline) — for students without internet access

- Fully local JSON file provided  
- Manual parsing allowed (no JSON library required)  
- No GUI mandatory  
- Simpler, smaller dataset but still requires OOP design  
- Graded up to 10 points

---

_Repository maintained for educational use at the University of Medicine, Pharmacy, Science and Technology “George Emil Palade” Târgu Mureș (Informatics, Year 2)._
