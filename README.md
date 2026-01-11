# Aaron Davis

Backend engineer focused on constraint-driven systems, state management, and algorithmic problem-solving. Building data-intensive applications with emphasis on architectural clarity and correctness guarantees.

## Current Focus

Systems where design constraints force careful architectural decisions: allocation algorithms, workflow orchestration, transactional consistency, and data integrity under complex business rules.

## Selected Projects

### [Project Storage](https://github.com/AaronDDavis/project_storage) — P2P Storage Marketplace with Admin Verification

A Django-based platform connecting people with unused storage space to those needing temporary storage. The technical challenge centered on modeling physical space hierarchically (Space → Rack → Shelf) while maintaining referential integrity across a two-phase verification workflow.

**Key engineering decisions:**

- **Service-layer architecture**: Extracted all business logic from Django views/models into framework-agnostic service classes for testability and reuse.
- **Best-fit allocation algorithm**: Implemented rack selection algorithm to minimize fragmentation by selecting racks with smallest available capacity, using ORM annotations for efficient filtering.
- **Explicit State machine**: Request lifecycle (Pending → Approved → Completed) enforced through dedicated state service, with gaurded transitions.
- **Domain-driven error handling**: Custom exception hierarchy (e.g. `SpaceStateException`, `BookingStatusException`) decouples business constraints from infrastructure errors.

The system handles concurrent bookings across 6-dimensional space state (3D physical dimensions + location + time + verification state), with price calculation, availability checking, and allocation logic centralized in testable service modules.

### [BTO Management System](https://github.com/AaronDDavis/bto-management-system) — Housing Application Workflow with Two-Pass Hydration

Console-based simulation of Singapore's Build-To-Order housing application process, modeling applicants, officers, and managers under real-world policy constraints. The core challenge was reconstructing an in-memory object graph from CSV files storing only IDs, while maintaining role-based visibility and state machine integrity.

**Key engineering decisions:**

- **Two-phase reference resolution**: Phase 1 hydrates all entities with primitives only; Phase 2 resolves relationships via O(1) lookup maps, eliminating forward-reference issues.
- **Entity-Control-Boundary layering**: Strict architectural separation where domain entities have zero dependencies on control/boundary layers, enforced through package-level import constraints.
- **Multi-actor state machines**: Different transition rules per application type (BTO, ProjectRegistration, Withdrawal), with guards preventing invalid states (e.g., applicant cannot have both `appliedProject != null` and `canApply == true`).
- **Role-based data filtering**: Database managers apply eligibility constraints specific to the particular user at query time.

Demonstrates file-based persistence with relational semantics, role-driven workflows, and constraint propagation across interconnected entities.

### [Team Allocation Simulator](https://github.com/AaronDDavis/team-allocation-simulator) — Constraint Satisfaction for 6000+ Students

Algorithm that partitions students across tutorial groups into balanced teams of 4–10 members, satisfying competing statistical constraints on gender ratio, CGPA distribution, and institutional diversity.

**Key engineering decisions:**

- **Adaptive constraint relaxation**: Monotonic loosening of thresholds (CGPA tolerance, minimum school diversity) triggered by iteration counters, guaranteeing convergence without manual tuning.
- **Proportional sampling strategy**: Random selection weighted by target gender distributions computed from tutorial-wide ratios, maintaining equity while exploring solution space stochastically.
- **Hierarchical constraint priority**: Gender ratios enforced strictly (institutional requirement), CGPA tolerance widens first, diversity requirements relax last—reflects real-world constraint rigidity.
- **Violation detection and retry logic**: Teams validated against all constraints post-generation; rejected teams return students to pool rather than attempting local repairs.

Handles combinatorially large solution spaces (10^15+ configurations for 50-student tutorials) without exhaustive enumeration, converging to tightest feasible thresholds for each group's composition.

## Technical Skills

**Languages:** Python, Java, JavaScript  
**Backend & Frameworks:** Django, ORM design  
**Data & Persistence:** PostgreSQL, SQLite, CSV-based systems  
**Architecture & Patterns:** Service-layer architecture, State machines (FSM), Strategy pattern, Entity-Control-Boundary (ECB), Composite pattern  
**Algorithms:** Constraint satisfaction, Best-fit allocation, Graph construction, Two-pass hydration  
**Tools & Infrastructure:** Git, Gunicorn, WhiteNoise, Render (PaaS), Environment-based configuration  
**Development Practices:** SOLID principles, Domain-driven error handling, Type annotations

## Contact

Email: [aaronddavis001@gmail.com](mailto:aaronddavis001@gmail.com)

LinkedIn: [https://linkedin.com/in/aaron-daniel-davis]
