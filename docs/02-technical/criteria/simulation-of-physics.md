# Criterion: Simulation of Cloth and Liquid

## Architecture Decision Record

### Status

**Status:** Accepted 

**Date:** 2026-01-06

### Context

The project requires simulation of interactive ropes (cloth-like physics) in Unity without relying on built-in colliders or cloth components.  

Ropes serve as a **gameplay tool**, allowing the creation of various mechanics such as:  
- player climbing,  
- interacting with objects (e.g., triggering buttons),  
- providing dynamic environmental challenges.  

The ropes must respond to gravity, allow player interaction, and simulate swinging and damping behavior.  

Simulation of liquid (water) was initially considered but **not implemented** due to high computational cost and its purely decorative purpose for this 2D game. Alternative simpler solutions exist for visual effects if needed.

### Decision

- Implemented **rope simulation** using Unity's **Line Renderer** combined with custom physics computations.  
- Two ropes exist:  
  1. Rope with a conditional weight, used to trigger button.  
  2. Rope that the player can grab and climb, with collision response allowing realistic swinging and sliding around a character's body.  
- Rope physics handle player collisions and damping.  
- Water/liquid simulation is **omitted** to avoid unnecessary CPU/GPU load.

### Alternatives Considered

| Alternative | Pros | Cons | Why Not Chosen |
|-------------|------|------|----------------|
| Unity built-in colliders and physics | Easy to implement | Less control over rope behavior, less realistic swinging | Custom physics gives more control and climbing behavior |
| Full 2D/3D fluid simulation (particles or SPH) | Realistic water physics, interactive waves | High CPU/GPU cost, complex | Not needed for decorative purposes; deferred for simplicity |
| Monolithic rope script without Line Renderer | Simpler structure | Harder to visualize, less reusable | Line Renderer improves visual clarity and modularity |

### Consequences

**Positive:**
- Realistic rope behavior for gameplay interactions  
- Player can climb, and grab ropes with objects
- Visualized clearly with Line Renderer  
- Lightweight computation suitable for 2D gameplay

**Negative:**
- Liquid/water simulation not implemented  
- Rope physics simplified; may not handle extreme scenarios realistically

**Neutral:**
- Visual quality of rope depends on Line Renderer resolution; no effect on gameplay mechanics

## Implementation Details

### Path to scripts

```
Honey&Bunny/Assets/scripts/Diploma/Physics/LevelLogic/
```

### Key Implementation Decisions

| Decision | Rationale |
|----------|-----------|
| Use of Line Renderer for rope | Provides visual clarity while keeping physics lightweight |
| Custom physics for rope | Enables player interaction and climbing mechanics not possible with default Unity colliders |
| Two separate rope types | Allows both interaction with objects and climbing without conflict |
| Exclusion of water simulation | Avoids high computational cost; decorative element deemed unnecessary |

## Requirements Checklist

| # | Requirement | Status | Evidence/Notes |
|---|-------------|--------|----------------|
| 1 | Rope simulation under gravity | ✅ | Rope responds to gravity and player interaction |
| 2 | Player can grab/interact with rope | ✅ | Rope allows climbing and object triggering |
| 3 | Rope oscillates and damps over time | ✅ | Custom physics simulates swinging and damping |
| 4 | Liquid simulation (optional) | ❌ | Not implemented due to complexity and decorative purpose |

## Known Limitations

| Limitation | Impact | Potential Solution |
|------------|--------|-------------------|
| No water simulation | Decorative liquid effects are not present | Implement particle-based or shader-based 2D fluid simulation if needed or use easer way to create 2D water effects |
