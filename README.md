# PodSphere: Podcast Learning & Creator Services Platform

| Course | Project | Team | Team size | Database | Submission period |
| --- | --- | --- | ---: | --- | --- |
| Database Management Systems | PodSphere | T0093 | 4 | PostgreSQL | November 2026 |

## Project Overview

PodSphere is a podcast-focused platform for creators, learners, instructors, equipment providers, recording studios, and creative-service providers. Its current logical model brings these workflows together:

- Podcast creation and episode management
- Courses, lessons, learner enrollments, and lesson progress
- Equipment listings and rental requests
- Studio listings and time-slot bookings
- Creator services and service orders
- Payments, transaction events, and provider payouts
- Reviews of users and marketplace offerings
- Creator planning and task tracking

The CP1/CP2 database scope contains **23 relational tables**. Sponsorship agreements, subscriptions, premium-content entitlements, and affiliate commissions are outside the current schema. Add them only after their requirements and business rules are defined.

## Team

| Role | Name | Enrollment No. | GitHub |
| --- | --- | --- | --- |
| Group Lead | Aniket Kumar | 2501010635 | [NopePlague](https://github.com/NopePlague) |
| Member 2 | Aditya Kumar Gupta | 2501010565 | [AdityaGupta-2006](https://github.com/AdityaGupta-2006) |
| Member 3 | Anik Kumar Deo | 2501010056 | [Source-sucker](https://github.com/Source-sucker) |
| Member 4 | Muskan Praveen | 251010602 | [mukku2549](https://github.com/mukku2549) |

The DE repository's root-level `team.json` is maintained separately for course-tracker commit attribution. This AP repository README documents the PodSphere project and its deliverables.

## Repository Structure

```text
PodSphere_AP_2026/
├── README.md
├── dbms/
│   ├── 01_normalization.md       # CP1: UNF-to-3NF analysis and functional dependencies
│   ├── 02_er_diagram.md          # CP2: logical ER model, notation, and constraints
│   ├── 03_schema.sql             # CP2: PostgreSQL DDL, keys, checks, indexes, and triggers
│   ├── 04_queries.sql            # CP3: planned SQL query workload
│   ├── 05_query_timings.md       # CP4: planned query timing analysis
│   └── plans/                    # CP4: planned EXPLAIN/query-plan evidence
└── diagrams/
    ├── er_diagram.png            # Visual ERD for reports and review
    ├── er_diagram.svg            # Scalable vector export
    └── er_diagram.drawio         # Editable diagrams.net source
```

The CP3 and CP4 paths show the planned deliverable layout; they are not complete until the corresponding files and evidence are added and committed.

## Database Design

| Domain | Tables | Purpose |
| --- | --- | --- |
| Identity and profiles | `users`, `roles`, `user_roles`, `profiles` | Accounts, role membership, and user profiles |
| Podcasts | `podcasts`, `episodes` | Creator-owned podcasts and episodes |
| Learning | `courses`, `lessons`, `enrollments`, `lesson_progress` | Course content, enrollment, and learner progress |
| Equipment | `equipment_categories`, `equipment`, `rentals` | Equipment catalogue, providers, and rental records |
| Studios | `studios`, `studio_bookings` | Studio listings and bookings |
| Creator services | `services`, `service_orders` | Provider services and customer orders |
| Finance | `payments`, `transactions`, `payouts` | Payment records, transaction history, and payouts |
| Feedback | `reviews` | Reviews for one supported target per review |
| Creator planning | `creator_plans`, `plan_tasks` | Creator plans and task lists |

### Integrity Rules

- Each review targets exactly one supported type: user, equipment, studio, service, or course.
- A reviewer cannot submit duplicate reviews for the same target; five target-specific partial unique indexes enforce this.
- Confirmed studio bookings cannot overlap for the same studio.
- Confirmed and active equipment rentals must respect available inventory over overlapping date ranges.
- Lesson progress requires enrollment in the course containing the lesson.
- Composite uniqueness is scoped to its parent, such as episode number within a podcast or lesson order within a course.

The detailed keys, predicates, exclusion constraint, and trigger behavior are documented in `dbms/02_er_diagram.md` and `dbms/03_schema.sql`.

## Checkpoint Plan

| Checkpoint | Target date | Workstream | Deliverables |
| --- | --- | --- | --- |
| CP1 | 16 Nov 2026 | Relational analysis and normalization | `dbms/01_normalization.md` |
| CP2 | 17 Nov 2026 | ER modelling and PostgreSQL schema | `dbms/02_er_diagram.md`, `dbms/03_schema.sql`, `diagrams/` exports |
| CP3 | 19 Nov 2026 | SQL query implementation and validation | `dbms/04_queries.sql` |
| CP4 | 23 Nov 2026 | Query performance, execution plans, and analysis | `dbms/05_query_timings.md`, `dbms/plans/` |

These are checkpoint target dates. Completion should be evidenced by the required committed files, not by a status label alone.

## Working and Validation

1. Keep the logical model, Mermaid ER description, visual ERD, and SQL DDL synchronized.
2. Treat PostgreSQL DDL as the source for implemented keys, nullability, checks, and database-enforced rules.
3. Recheck foreign keys, composite keys, partial unique indexes, and cardinalities when changing the diagram.
4. Run the schema against a clean PostgreSQL database before claiming execution validation.
5. Preserve tested SQL, environment details, and raw execution-plan evidence for query-performance work.
6. Commit work under each contributor's own GitHub identity for attributable team history.

## Project Handoff

The current AP handoff is the CP1 normalization report and CP2 ER/schema package. The next planned work is CP3 query implementation, followed by CP4 timing and query-plan evidence.

Before final submission, verify that the schema executes cleanly, the ERD and DDL agree, special constraints are tested, timing claims are backed by saved plans, and the required files are present on the submission branch.

**AP repository:** [PodSphere_AP_2026](https://github.com/AdityaGupta-2006/PodSphere_AP_2026) · **Team:** T0093
