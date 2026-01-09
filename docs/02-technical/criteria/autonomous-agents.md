# Criterion: Autonomous Agents

## Architecture Decision Record

### Status

**Status:** Accepted

**Date:** 2026-01-06

### Context

In the current implementation, agent behavior for enemies is implemented in a mostly **monolithic way**, with one or two scripts controlling the entire behavior. This approach is difficult to maintain, extend, and reuse across different enemy types.  

The project includes multiple enemy types, each with **unique states** and behaviors. Boss agents require more complex decision-making compared to regular enemies. The goal is to implement a scalable, reusable, and maintainable system for autonomous agent behavior within Unity (C#), while also allowing shared data through a **Blackboard**.

### Decision

- **Finite State Machine (FSM)** is implemented for regular enemies:
  - A shared base structure is used (e.g., `IState`, `StateRunner`, `Transition`)  
  - Each enemy type inherits and customizes its own states 
  - Enables reusability and simplifies maintenance  
- **Hierarchical Finite State Machine (HFSM)** is implemented for the boss:
  - Separate files for each state  
  - Allows complex, multi-layered behaviors  
- **Blackboard** system stores shared agent data accessible by all agents  
- This structure improves modularity and makes it easier to extend or modify agent behavior in the future

### Alternatives Considered

| Alternative | Pros | Cons | Why Not Chosen |
|-------------|------|------|----------------|
| Monolithic scripts for each enemy | Simple to implement for a single enemy | Hard to maintain, extend, or reuse; duplication of logic | Complexity grows quickly with more enemies; violates separation of concerns |
| Event-driven behavior (scriptable events) | Decouples actions from states; flexible | Harder to reason about sequences and transitions; less structured | FSM/HFSM provides clearer, reusable structure for complex behaviors |
| FSM only for all agents including boss | Single framework, consistent | Cannot easily represent hierarchical or nested behavior | Boss behavior is complex and benefits from HFSM |

### Consequences

**Positive:**
- Easier to maintain and extend enemy behaviors  
- Reusable base classes for different enemy types  
- Clear separation of concerns between agent logic and state management  
- Blackboard allows shared data between agents  

**Negative:**
- Slightly more initial setup compared to monolithic approach  
- Developers need to understand FSM/HFSM patterns  

**Neutral:**
- Number of states per enemy varies; this is managed individually without affecting overall structure  

## Implementation Details

### Project Structure
```
Honey&Bunny/Assets/Scripts/Enemy/FSM/
├── BurderEnemy/
|        ├── States/
|        └── BurderAI
|
├── NeckkerEnemy/
├── HFSMBoss/
├── PlantEnemy/
├── Blackboard.cs
├── BlackboardKeys.cs
├── EnemyStateMachineRunner.cs
├── IState.cs
├── StateMachine.cs
└── Transition.cs
```

### Key Implementation Decisions

| Decision | Rationale |
|----------|-----------|
| FSM for regular enemies | Provides reusable, maintainable, and clear behavior structure for multiple enemy types without complex behaviour |
| HFSM for boss | Supports complex hierarchical behaviors, allowing nested states for multi-step actions |
| Blackboard system | Shared state dictionary allows agents to access and update common data efficiently |
| Separation of states into files | Improves modularity and simplifies debugging and future expansion |

## Requirements Checklist

| # | Requirement | Status | Evidence/Notes |
|---|-------------|--------|----------------|
| 1 | At least 2 agents, each with multiple behavior states | ✅ | Three regular enemies implemented with FSM, each having multiple states |
| 2 | Each agent has at least one unique state | ✅ | Each enemy type has a custom state class unique to itself |
| 3 | Behavior configuration through code | ✅ | States and transitions configured programmatically via FSM and HFSM |
| 4 | Blackboard (shared data storage) | ✅ | `Blackboard.cs` provides a shared dictionary accessible to all agents |
| 5 | 4 agents with different behavior sets (optional) | ✅ | Currently 3 regular enemies and 1 boss implemented; more can be added easily |
| 6 | Behavior configuration via external files or node editor (optional) | ❌ | Configuration is currently hardcoded; external files or node editor not used |
| 7 | Debug mode: visualization of current state/branch in real-time (optional) | ❌ | Not implemented yet; would require editor/visualization tools |

## Known Limitations

| Limitation | Impact | Potential Solution |
|------------|--------|-------------------|
| Variability in enemy state count | Each enemy may require additional setup for custom states | Use factory or configuration patterns to automate state assignments |
