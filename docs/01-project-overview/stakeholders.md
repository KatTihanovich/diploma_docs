# Stakeholders & Users

## Target Audience

| Persona | Description | Key Needs |
|---------|-------------|-----------|
| Developer | Current team developers and future contributors working on the Unity-based game project, including client-side logic and backend integration | Clear project structure, modular and reusable components, documented API, ease of integration between Unity client and backend services, and reference implementations of common gameplay patterns (e.g., FSM-based enemy behavior) to support further extension and maintenance |
| Game user | End users playing the cross-platform board game through a graphical Unity-based interface, without requiring technical knowledge, in a casual or testing environment | Stable and responsive gameplay, intuitive user interface, consistent game logic, and reliable interaction with game features |

## User Personas

### Persona 1: Developer

| Attribute | Details |
|-----------|---------|
| **Role** | Student game developer / Unity developer |
| **Age** | 16+ |
| **Tech Savviness** | High |
| **Goals** | Implement and extend game mechanics, AI behaviors, and backend integration; maintain and scale the project efficiently |
| **Frustrations** | Tightly coupled enemy behavior scripts that are difficult to reuse or extend, and missing or incomplete integration with backend services. |
| **Scenario** | Works on adding new enemy types or gameplay features in the Unity project, using existing modules and FSM-based behavior implementations as a reference, integrates changes with the backend API, and plans to utilize persisted user data for analytics and balancing purposes in future iterations. |

### Persona 2: Game User

| Attribute | Details |
|-----------|---------|
| **Role** | End user / Player |
| **Age** | 10+ |
| **Tech Savviness** | Low–Medium |
| **Goals** | Enjoy stable and engaging gameplay without technical issues and with the option to save your progress if the user wants to. |
| **Frustrations** | Errors in mob behaviour, lack of achievements, progress is only saved locally and will be lost if app is deleted. |
| **Scenario** | Launches a cross-platform desktop game, interacts with the graphical interface, and plays game sessions without requiring any technical knowledge, with the ability to save progress, earn achievements, and track statistics. |

## Stakeholder Map

### High Influence / High Interest
- **Developer / Student**: Directly developing the project; responsible for implementing, testing, and documenting all technical components, ensuring correct operation of modules, integration with the database, physics, and agent behavior.

### High Influence / Low Interest
- **Experts / Commission**: Assessing compliance with project requirements and evaluating the quality of documentation and technical implementation. They have high authority but only periodic engagement with the project.

### Low Influence / High Interest
- **Game development team (designers, animators, sound, narrative)**: Interested in reliable integration of technical components and correct operation of visual, animation, and audio elements; need a stable system to create content without conflicts.

### Low Influence / Low Interest
- **Scientific Supervisor**: Provides guidance and consultation, ensuring academic standards and diploma requirements are met. Their engagement is regular but their direct influence on daily project tasks is moderate.
- **Potential users (players)**: Interested in stable gameplay, interactivity, progress saving, and high-quality gaming experience; they have low influence over technical decisions.
