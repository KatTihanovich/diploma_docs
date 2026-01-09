# Criterion: Autonomous Agents

## Architecture Decision Record

### Status
**Status:** Accepted  
**Date:** 2026-01-06

### Context
Current enemy AI uses mostly monolithic scripts, making maintenance and extension difficult. Multiple enemy types with unique states exist, and boss agents require hierarchical behavior. A scalable, reusable, and maintainable system is needed in Unity, with shared data via a **Blackboard**.

### Decision
- **FSM** for regular enemies:
  - Shared base structure (`IState`, `StateRunner`, `Transition`)  
  - Each enemy customizes its own states  
  - Reusable and maintainable  
- **HFSM** for boss:
  - Separate files per state  
  - Supports complex, multi-layered behavior  
- **Blackboard** stores shared data accessible to all agents  
- Structure improves modularity and extensibility

### Alternatives Considered

| Alternative | Pros | Cons | Why Not Chosen |
|-------------|------|------|----------------|
| Monolithic scripts | Simple for one enemy | Hard to maintain, extend, duplicate logic | Becomes unmanageable as enemies increase |
| Event-driven behavior | Decoupled and flexible | Harder to reason about sequences | FSM/HFSM provides clearer, reusable structure |
| FSM only for all agents | Single framework | Cannot represent hierarchical/nested behavior | Boss needs HFSM for complex behavior |

---

### Consequences

**Positive**
- Easier maintenance and extension  
- Reusable base classes  
- Clear separation of concerns  
- Blackboard allows shared data  

**Negative**
- Slightly more initial setup  
- Requires understanding FSM/HFSM patterns  

**Neutral**
- State count varies per enemy; handled individually

---

## Implementation Details

### Project Structure

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

### Key Implementation Decisions

| Decision | Rationale |
|----------|-----------|
| FSM for regular enemies | Reusable, maintainable, clear behavior structure |
| HFSM for boss | Supports hierarchical, multi-step behaviors |
| Blackboard system | Shared dictionary for agent data access |
| Separate files per state | Improves modularity, simplifies debugging |

---

## Requirements Checklist

| # | Requirement | Status | Notes |
|---|-------------|--------|-------|
| 1 | ≥2 agents with multiple states | ✅ | Three regular enemies implemented with multiple states |
| 2 | Each agent has a unique state | ✅ | Each enemy has custom state classes |
| 3 | Behavior configured in code | ✅ | States and transitions set programmatically |
| 4 | Blackboard for shared data | ✅ | `Blackboard.cs` used by all agents |
| 5 | 4 agents with different behavior (optional) | ✅ | 3 regular + 1 boss; scalable for more |
| 6 | Config via files/node editor (optional) | ❌ | Currently hardcoded |
| 7 | Debug visualization (optional) | ❌ | Not implemented yet |

---

## Known Limitations

| Limitation | Impact | Potential Solution |
|------------|--------|-------------------|
| Variable enemy state count | Custom setup needed per enemy | Use factory or configuration patterns to automate states |
