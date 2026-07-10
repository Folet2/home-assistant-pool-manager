# 🏗️ PoolBot Architecture

> Simple systems are easier to understand, maintain and trust.

---

## Overview

PoolBot is designed as a collection of independent modules.

Each module has a single responsibility and can evolve independently.

```text
Water Temperature
        │
        ▼
Runtime Calculator
        │
        ▼
Filtration Planner
        │
        ▼
Scheduler
        │
        ▼
Pump Controller
        │
        ▼
ESPHome / Relay
```

---

## Core Principles

### Single Responsibility

Each module answers one question only.

| Module | Responsibility |
|----------|----------------|
| Runtime Calculator | How long should filtration run today? |
| Filtration Planner | How should runtime be distributed? |
| Scheduler | When should filtration run? |
| Pump Controller | Execute the schedule |

---

### Modular Design

Modules should be loosely coupled.

A change in one module should not require modifications in the others.

---

### Testability

Every module should be testable independently.

For example:

Input:

```text
Water temperature = 26°C
```

Output:

```text
Filtration runtime = 13 hours
```

No physical equipment should be required to validate the logic.

---

## Runtime Calculator

### Purpose

Determine the daily filtration duration.

### Inputs

- Water temperature
- User configuration
- Future extensions

### Output

```text
Daily runtime (hours)
```

Example:

```text
Temperature = 28°C

Result = 14 h
```

---

## Filtration Planner

### Purpose

Split the daily runtime into multiple filtration cycles.

### Input

```text
14 h
```

### Output

```text
Cycle 1 = 5 h

Cycle 2 = 4 h

Cycle 3 = 5 h
```

---

## Scheduler

### Purpose

Convert filtration cycles into operating periods.

### Input

```text
5 h
4 h
5 h
```

### Output

```text
06:00 → 11:00

13:00 → 17:00

18:00 → 23:00
```

---

## Pump Controller

### Purpose

Control the physical filtration pump.

### Responsibilities

- Start pump
- Stop pump
- Monitor operating state
- Recover after Home Assistant restart

---

## Future Modules

The architecture is designed to support additional modules without modifying the existing core.

Potential future modules:

- Heat Pump Manager
- Freeze Protection Engine
- Water Chemistry Manager
- Energy Optimization Engine
- Solar Production Optimizer
- Notification Center

---

## Design Rule

Before creating a new module, ask:

1. Does it solve a real problem?
2. Can it remain independent?
3. Is it simple to understand?
4. Can it be tested separately?

If not, rethink the design.

---
> Keep the course.

Reliable automation is built from simple and well-defined components.
> Keep the course.

Reliable automation is built from simple and well-defined components.
