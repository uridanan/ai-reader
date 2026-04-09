# General Engineering Principles: Object-Oriented Programming (OOP)

When participating in the design, typing, or implementation phases of the TDD workflow, the agent MUST strictly adhere to the following Object-Oriented Programming principles:

1. **Encapsulation:** Group related data and the methods that operate on them together within classes or encapsulated modules. Use access modifiers (`private`, `protected`, `public` in TypeScript) to restrict unauthorized access and hide internal state variations. Do not leak internal implementation details.
2. **Abstraction:** Expose only the necessary high-level interfaces to the outside world. 
3. **Inheritance & Composition:** Favor composition over inheritance to avoid deep, brittle hierarchies. However, use inheritance appropriately when there is a clear strict "is-a" structural relationship.
4. **Polymorphism:** Design interfaces and base classes that can be implemented seamlessly in multiple forms. 
5. **SOLID Principles:**
    - **Single Responsibility (SRP):** A class/module should have one, and only one, reason to change.
    - **Open/Closed (OCP):** Modules should be open for extension (e.g., via dependency injection or plugins) but closed for core modification.
    - **Liskov Substitution (LSP):** Derived implementations must be substitutable for their base interfaces without breaking the system.
    - **Interface Segregation (ISP):** Prefer many small, client-specific interfaces over one bulky, general-purpose "God" interface.
    - **Dependency Inversion (DIP):** Depend on abstractions (interfaces), not concrete implementations. Inject dependencies wherever possible to make unit testing easier.

**Role-Specific Enforcement Directions:**
* **Architect:** Your high-level plans must conceptualize the solution in terms of independent objects, modules, and their interactions, rather than pure procedural data pipelines.
* **API Designer:** You MUST define clean TypeScript `interface` and `abstract class` structures. Force the Developer to rely on dependency injection where applicable via constructor arguments or context.
* **Developer:** Your implementations must be encapsulated within the boundaries outlined by the API Designer. Avoid floating global variables or massive utility files full of loose functional spaghetti unless strictly mandated by a specific frontend framework paradigm.
