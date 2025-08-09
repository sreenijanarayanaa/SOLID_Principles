# 🧱 SOLID Principles in Object-Oriented Design
- SOLID is an acronym for five fundamental principles of ObjectOriented Programming (OOP) and design.
- These principles help developers create maintainable, scalable, and flexible software.
-  Introduced by Robert C. Martin (Uncle Bob), these principles are now standard guidelines for writing clean and efficient code.

## 1. Single Responsibility Principle (SRP)
Definition:A class should have only one reason to change, meaning it should handle only one responsibility.

Explanation:If a class has multiple jobs, changes in one part can affect unrelated functionality. Separating responsibilities improves maintainability and testability.

❌ Violation:

In an online store, if a OrderService class is responsible for placing orders, processing payments, and sending confirmation emails, it’s doing too much.
```java
class OrderService {
    void placeOrder() { /* order logic */ }
    void processPayment() { /* payment logic */ }
    void sendConfirmationEmail() { /* email logic */ }
}
```
✅ Solution:Split responsibilities
```java
class OrderService { void placeOrder() { } }
class PaymentService { void processPayment() { } }
class EmailService { void sendEmail() { } }
```
🎯 Each service now has one job, making them easier to maintain and test.

## 2. 🔓 Open/Closed Principle (OCP)
✅ Definition:Software entities should be open for extension but closed for modification.

📝 Explanation:You should be able to add new behavior without changing existing code. Use inheritance or interfaces.

❌ Violation:
```java
class PaymentProcessor {
    double pay(String gateway, double amount) {
        if (gateway.equals("Stripe")) return amount * 0.98;
        else if (gateway.equals("PayPal")) return amount * 0.95;
        return amount;
    }
}
```
Adding a new discount type requires modifying this class.

✅ Solution:
```java
interface PaymentGateway {
    double processPayment(double amount);
}

class StripeGateway implements PaymentGateway {
    public double processPayment(double amount) { return amount * 0.98; }
}

class PayPalGateway implements PaymentGateway {
    public double processPayment(double amount) { return amount * 0.95; }
}
```
Now, you can add new discount types without modifying existing classes.

## 3. 🧬 Liskov Substitution Principle (LSP)
✅ Definition:Subclasses should be substitutable for their parent classes without breaking functionality.

📝 Explanation:You should be able to use a subclass anywhere a parent class is expected, and it should behave properly.

Example: Document Generation System
In a reporting tool, you generate multiple formats: PDF, Word, Excel. All documents should follow a common interface.

❌ Violation:
```java
class Document {
    void print() { System.out.println("Printing..."); }
}

class SecurePDF extends Document {
    @Override
    void print() {
        throw new UnsupportedOperationException("Secure PDFs can't be printed");
    }
}
```
✅ Solution:
```java
class Document { /* common functionality */ }

class PrintableDocument extends Document {
    void print() { System.out.println("Printing..."); }
}

class SecurePDF extends Document {
    // No print() method here
}
```
🎯 Substituting subclasses won’t break behavior expected by the system.

## 4. 🧩 Interface Segregation Principle (ISP)
✅ Definition:Clients should not be forced to depend on methods they do not use.

📝 Explanation:Use smaller, more specific interfaces instead of one large interface.

Example: Banking Software — Different User Roles
A BankUser interface shouldn't force all users (e.g., tellers, customers, auditors) to implement all actions.

❌ Violation:
```java
interface BankUser {
    void withdrawCash();
    void approveLoan();
    void viewAuditLogs();
}
```
A teller might not approve loans, and an auditor doesn’t need to withdraw cash.

✅ Solution:
```java
interface CashHandler {
    void withdrawCash();
}

interface LoanManager {
    void approveLoan();
}

interface Auditor {
    void viewAuditLogs();
}
```
🎯 Each role implements only what it needs.

## 5. 🔌 Dependency Inversion Principle (DIP)
✅ Definition:

Highlevel modules should not depend on lowlevel modules. Both should depend on abstractions.

📝 Explanation:Use interfaces or abstract classes to reduce tight coupling.

Example: Notification System in Enterprise Applications
An app needs to send notifications via SMS, email, or push notifications.

❌ Violation:
```java
class NotificationService {
    EmailSender sender = new EmailSender();
    void notifyUser() { sender.sendEmail(); }
}
```
✅ Solution:
```java
interface Notifier {
    void notifyUser(String message);
}

class EmailSender implements Notifier {
    public void notifyUser(String message) { /* send email */ }
}

class SMSender implements Notifier {
    public void notifyUser(String message) { /* send SMS */ }
}

class NotificationService {
    private Notifier notifier;
    public NotificationService(Notifier notifier) {
        this.notifier = notifier;
    }

    void send(String message) {
        notifier.notifyUser(message);
    }
}
```
🎯 This design allows switching between notification types easily and is easier to test with mocks.

🏁 Conclusion
SOLID principles help create better software architecture.

Here’s a quick recap:

✅ SRP: One class = one responsibility

✅ OCP: Extend behavior without changing existing code

✅ LSP: Subtypes must be replaceable without errors

✅ ISP: Avoid forcing classes to use methods they don’t need

✅ DIP: Depend on abstractions, not concrete classes

➡️ Applying these principles makes code easier to understand, reuse, test, and maintain.
