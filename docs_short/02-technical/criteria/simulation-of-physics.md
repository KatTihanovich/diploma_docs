# Criterion: Simulation of Cloth and Liquid

## Architecture Decision Record

### Status
**Status:** Accepted  
**Date:** 2026-01-06

### Context
The project requires **interactive rope simulation** in Unity for gameplay mechanics:  
- Player climbing  
- Interacting with objects (e.g., buttons)  
- Dynamic environmental challenges  

Ropes must respond to gravity, support player interaction, and simulate swinging/damping.  
Liquid/water simulation was considered but **not implemented** due to high computational cost and decorative purpose.

### Decision
- **Rope simulation** via Unity **Line Renderer** + custom physics  
- Two rope types:  
  1. Conditional-weight rope for triggering objects  
  2. Climbable rope with collision response for realistic swinging/sliding  
- Rope physics handle collisions and damping  
- **Liquid simulation omitted** for performance reasons

---

### Alternatives Considered

| Alternative | Pros | Cons | Why Not Chosen |
|-------------|------|------|----------------|
| Unity built-in colliders & physics | Easy implementation | Less control, weaker climbing/swinging | Custom physics provides better gameplay |
| Full fluid simulation (particles/SPH) | Realistic interactive water | High CPU/GPU cost | Not needed for decoration |
| Monolithic rope script without Line Renderer | Simpler code | Harder to visualize & reuse | Line Renderer improves clarity & modularity |

---

### Consequences

**Positive:**  
- Realistic rope behavior for gameplay  
- Player can climb and interact with objects  
- Lightweight computation suitable for 2D gameplay  

**Negative:**  
- No water simulation  
- Rope physics simplified; may fail in extreme scenarios  

**Neutral:**  
- Visual quality depends on Line Renderer resolution  

---

## Implementation Details

### Path to scripts

```
Honey&Bunny/Assets/scripts/Diploma/Physics/LevelLogic/
```

### Key Implementation Decisions

| Decision | Rationale |
|----------|-----------|
| Line Renderer for ropes | Clear visualization, lightweight physics |
| Custom rope physics | Enables climbing and interaction beyond Unity colliders |
| Two rope types | Separates climbing and object interaction mechanics |
| Water simulation omitted | Avoids high computational cost; not needed for gameplay |

---

## Requirements Checklist

| # | Requirement | Status | Notes |
|---|-------------|--------|-------|
| 1 | Rope simulation under gravity | ✅ | Responds to gravity & player interaction |
| 2 | Player can grab/interact | ✅ | Climbing and object-triggering supported |
| 3 | Rope oscillates & damps | ✅ | Swinging/damping simulated |
| 4 | Liquid simulation (optional) | ❌ | Not implemented due to complexity |

---

## Known Limitations

| Limitation | Impact | Potential Solution |
|------------|--------|------------------|
| No water simulation | Decorative liquid effects missing | Use particle/shader-based 2D fluids or simpler visual effects |
| Rope interaction animations missing | Character appears static while climbing | Integrate rope-specific animations from animation team |
