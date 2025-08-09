# 🧱 SOLID Principles in Object-Oriented Design

- Writing clean, maintainable code is just as important as writing code that works. 

- The SOLID principles, introduced by Robert C. Martin (Uncle Bob), provide a blueprint for building software that is easy to adjust, extend, and maintain over time.

- This repository explores each of the five SOLID principles with real-world examples and code snippets.

---

## 📚 Table of Contents

- [S: Single Responsibility Principle (SRP)](#s-single-responsibility-principle-srp)
- [O: Open/Closed Principle (OCP)](#o-openclosed-principle-ocp)
- [L: Liskov Substitution Principle (LSP)](#l-liskov-substitution-principle-lsp)
- [I: Interface Segregation Principle (ISP)](#i-interface-segregation-principle-isp)
- [D: Dependency Inversion Principle (DIP)](#d-dependency-inversion-principle-dip)

---

## S: Single Responsibility Principle (SRP)

> A class should have one, and only one, reason to change.

### ❌ Violation Example
```python
class UserManager:
    def authenticate_user(self): ...
    def update_profile(self): ...
    def send_email_notification(self): ...
