# Module 14 — LLD Interview Playbook

> **Prerequisites**: Modules [01–13](./00_README.md)
> **Next**: [Module 15 → BONUS: Anti-Patterns](./15_Anti_Patterns.md)

---

## Why Does This Module Exist?

You know SOLID, you know the Design Patterns, and you know how to solve standard problems like Parking Lot and Ride-sharing. But knowing the theory is different from executing it under pressure in a 45-minute interview.

This module provides a battle-tested framework for tackling **any** LLD (Low-Level Design / Machine Coding) interview, structuring your time, and knowing exactly what the interviewer is evaluating.

---

## Table of Contents

1. [What Interviewers Actually Look For](#1-what-interviewers-actually-look-for)
2. [The 45-Minute Interview Timeline](#2-the-45-minute-interview-timeline)
3. [The 5-Step Execution Framework](#3-the-5-step-execution-framework)
4. [Design Pattern Cheat Sheet (When to use what)](#4-design-pattern-cheat-sheet)
5. [Handling Curveballs](#5-handling-curveballs)
6. [The "Extra Mile" (Getting Strong Hire)](#6-the-extra-mile)

---

## 1. What Interviewers Actually Look For

Many candidates think LLD is just about writing code that compiles and passes test cases. **It's not.** If you write a massive `main` method with 10 `if-else` blocks that works perfectly, you will likely fail.

The interviewer evaluates you on:
1. **Extensibility**: Can I add a new feature without rewriting everything? (Open/Closed Principle).
2. **Modularity**: Are responsibilities separated? (Single Responsibility Principle).
3. **Readability**: Is the code clean? Are naming conventions clear?
4. **Design Patterns**: Did you recognize standard problems and apply standard solutions?
5. **Handling Ambiguity**: Did you ask the right questions before you started typing?

---

## 2. The 45-Minute Interview Timeline

A typical LLD or Machine Coding interview lasts 45 to 60 minutes. Time management is your biggest risk.

### Timeline Breakdown
* **00:00 - 05:00 (Clarification)**: Read the prompt, ask questions, define scope.
* **05:00 - 15:00 (Design & Modeling)**: Identify classes, relationships, and APIs. Draw a quick UML or write class signatures. **Get buy-in from the interviewer.**
* **15:00 - 35:00 (Implementation)**: Code the core logic. Do not get stuck on boilerplate (like getters/setters) unless required.
* **35:00 - 45:00 (Review & Extend)**: Dry run, discuss edge cases, concurrency, and answer follow-up questions.

> **Pro Tip**: Talk out loud while you think. If you go silent for 5 minutes and then write the wrong code, there's no time to recover.

---

## 3. The 5-Step Execution Framework

Use this structured approach for any LLD problem.

### Step 1: Clarify Requirements & Scope
- **Identify Actors**: Who interacts with the system? (e.g., User, Admin, System).
- **Identify Use Cases**: What can they do? (e.g., Book ticket, Cancel ticket, View status).
- **Out of Scope**: Explicitly state what you will *not* cover (e.g., "I will assume payment processing is handled by an external gateway").

### Step 2: Identify Core Entities (The Nouns)
Extract nouns from the requirements.
*Example (Movie Ticket Booking)*:
- Movie, Theater, Screen, Show, Seat, Ticket, User, Payment.

### Step 3: Define Relationships & APIs (The Verbs)
How do the entities connect?
- A `Theater` *has-a* list of `Screen`s (Composition).
- A `Show` *has-a* `Movie` and a `Screen` (Aggregation).
- Define interfaces for the core actions: `bookTicket()`, `searchMovies()`.

### Step 4: Apply Design Patterns
Look for specific triggers in the requirements (see cheat sheet below). Don't force patterns, but apply them where they solve a problem.

### Step 5: Implement the Core
Start with interfaces, then core entities, then the business logic (Services/Managers).

---

## 4. Design Pattern Cheat Sheet

When you hear a specific requirement, your brain should immediately associate it with a pattern.

| When the interviewer says... | Think... | Example |
|------------------------------|----------|---------|
| "We have different algorithms for..." | **Strategy** | Pricing (Surge vs Normal), Navigation (Shortest vs Fastest) |
| "Notify users when..." | **Observer** | Send SMS/Email when order status changes |
| "The object behaves differently based on its status..." | **State** | Vending Machine, Order lifecycle (Pending -> Shipped) |
| "We need to create different types of..." | **Factory** | Creating TwoWheeler vs FourWheeler parking spots |
| "We need a single orchestrator..." | **Singleton** | System-wide Configuration Manager, DB Connection Pool |
| "We need to add temporary features to..." | **Decorator** | Adding toppings to a Pizza, adding features to a Car |

---

## 5. Handling Curveballs

### "How would you handle concurrency?"
- *If they ask this*: They are checking for race conditions.
- *Your move*: Identify the shared resource (e.g., a specific seat in a theater, a parking spot). Mention `synchronized` blocks, `ReentrantLock`, or `ConcurrentHashMap`. (See [Module 13](./13_Concurrency_in_LLD.md)).

### "How would this scale to multiple servers?"
- *If they ask this*: They are bridging LLD with HLD.
- *Your move*: Mention that in-memory data structures (like a `HashMap` of active sessions) would need to move to a distributed cache like Redis. Local locks (`synchronized`) become Distributed Locks (Redis/Zookeeper).

### "I want to add a new requirement..." (Mid-interview)
- *If they ask this*: They are testing the Open/Closed Principle.
- *Your move*: If your design is solid, you should only need to add a new class (e.g., a new `Strategy` implementation) rather than modifying existing classes.

---

## 6. The "Extra Mile" (Getting Strong Hire)

To move from "Hire" to "Strong Hire":
1. **Custom Exceptions**: Don't just throw `Exception`. Create and use domain-specific exceptions like `SeatAlreadyBookedException` or `InvalidPaymentException`.
2. **Enums for States**: Use Enums for predefined states (e.g., `OrderStatus.DELIVERED`, `SeatType.PREMIUM`) instead of Strings or Integers.
3. **Immutability**: Make fields `final` where possible. It shows you care about thread safety and robust state management.
4. **Separation of Concerns**: Don't put business logic in your data models. Use Services/Managers (e.g., `OrderService` operates on the `Order` model).

---

> ✅ **Module 14 Complete**  
> **Next**: [Module 15 → BONUS: Anti-Patterns](./15_Anti_Patterns.md)
