# Glossary

| Term | Definition |
|------|------------|
| Game API | Backend service that handles authentication, data persistence, and communication between the game client and the database |
| Client–Server Architecture | System design where the Unity game acts as a client and communicates with a remote backend server |
| Finite State Machine (FSM) | A behavior model based on a limited set of states and transitions between them |
| Hierarchical Finite State Machine (HFSM) | An extension of FSM where states can contain nested sub-states |
| Blackboard | A shared data storage used by multiple agents to exchange information |

## Acronyms

| Acronym | Full Form | Description |
|---------|-----------|-------------|
| API | Application Programming Interface | Interface used by the game client to communicate with the backend |
| UI | User Interface | Visual elements through which the player interacts with the game |
| FSM | Finite State Machine | State-based model for enemy behavior |
| HFSM | Hierarchical Finite State Machine | FSM variant used for complex agent behaviors such as bosses |
| CI/CD | Continuous Integration / Continuous Deployment | Automated process for building, testing, and deploying software |

## Domain-Specific Terms

### Game AI & Behavior

| Term | Definition |
|------|------------|
| State | A distinct behavior mode of an agent (e.g., idle, attack, patrol) |
| Transition | A rule that defines when an agent switches from one state to another |
| Agent | An autonomous game entity with its own behavior logic |

### Game Physics & Simulation

| Term | Definition |
|------|------------|
| Rope Simulation | Custom physics-based system that simulates rope behavior under gravity and interaction |
| Verlet Integration | Numerical method used for stable physics simulations, commonly applied to ropes and cloth |
| Line Renderer | Unity component used to visually represent rope geometry |
