# 4. Retrospective

This section reflects on the project development process, lessons learned, and future improvements.

## What Went Well ✅

### Technical Successes

- Successful separation of responsibilities between the Unity client and the backend API
- Stable integration between Unity and the REST API for game progress, achievements, and levels
- Backend API design proved convenient for consumption from Unity without additional adapters
- Automated testing and CI/CD for the API increased confidence in backend stability during Unity development
- Clear data contracts (DTOs) reduced integration issues between client and server

### Process Successes

- Minimal rework was required when connecting Unity to the backend API
- Parallel development of Unity client features and backend API endpoints was possible due to clear API contracts
- Backend changes could be validated quickly without blocking Unity development

### Personal Achievements

- Became more confident working with Unity and writing game on C# and Game API on Java
- Gained hands-on experience integrating a Unity client with a remote backend API
- Improved understanding of client–server architecture in game development
- Strengthened skills in designing APIs with real consumer requirements (Unity) in mind

## What Didn't Go As Planned ⚠️

| Planned | Actual Outcome | Cause | Impact |
|---------|---------------|-------|--------|
| Liquid (water) simulation | Water simulation was not implemented | Particle-based or fluid simulation would introduce unnecessary CPU/GPU overhead for a 2D platformer; the feature was purely decorative and later removed from the game design | Medium |
| CI/CD for Unity game build | CI/CD pipeline was applied only to the backend API | Game builds require manual testing and validation; backend API is continuously deployed and better suited for automated pipelines | Low |
| Automated testing for full game project | Automated tests were implemented only for the backend API | Unity project includes third-party and legacy code; gameplay behavior is more efficiently verified through manual testing | Low |


### Challenges Encountered

1. **First-time use of Finite State Machines (FSM) for enemy AI**
   - **Problem:** FSM-based behaviour was used for the first time, which required understanding how to structure states, transitions, and shared logic for enemies.
   - **Impact:** Initial enemy implementation took more time, and some behaviour logic had to be updated after early testing.
   - **Resolution:** The FSM design was simplified, states were clearly separated, and reusable patterns were established, making subsequent enemy development more predictable and efficient.

2. **Limited lifetime of the remote database environment**
   - **Problem:** The hosted remote database had a limited lifetime (30 days), requiring periodic recreation of the database instance.
   - **Impact:** Temporary interruptions in development and additional time spent on database reconfiguration and data reinitialization.
   - **Resolution:** Database migrations and seed scripts were used to quickly restore the schema and data, minimizing disruption to the development workflow.


## Technical Debt & Known Issues

| ID | Issue | Severity | Description | Potential Fix |
|----|-------|----------|-------------|---------------|
| TD-001 | Offline progress is not persisted | Medium | In offline (guest) mode, gameplay progress, achievements, and statistics are not saved or synchronized | Implement local storage and deferred synchronization with the backend once connectivity is restored |
| TD-002 | Limited automated testing for Unity client | Medium | Automated tests are applied only to the backend API; the Unity client relies mostly on manual testing | Introduce Unity Test Framework for critical gameplay logic and regression testing |
| TD-003 | Manual configuration of enemy FSM states | Low | Enemy behavior states are configured directly in code, which may require additional setup when adding new enemy types | Introduce configuration via nodes and graphs |

### Code Quality Issues

- Unity code is missing comments
- Unity code isn't covered by unit tests
- Unity consists code that was written by other developers  and isn't in scope of my project, so it has different quality

## Future Improvements (Backlog)

If there was more time, these features/improvements would be prioritized:

### High Priority

1. **Offline Authentication Support**
   - Description: Allow users to log in while offline using locally cached credentials
   - Value: Improves user experience and enables seamless gameplay without a network connection
   - Effort: Medium

2. **Offline Progress Synchronization**
   - Description: Store gameplay progress locally in offline mode and synchronize it with the backend once the connection is restored
   - Value: Preserves player progress and achievements while maintaining data consistency
   - Effort: High

### Medium Priority

3. **CI/CD Pipeline for Unity Game Builds**
   - Description: Set up automated build pipelines for the Unity project (build validation, artifact generation)
   - Value: Improves build stability and reduces manual errors during releases
   - Effort: Medium

### Nice to Have

5. Environmental puzzles using liquid mechanics (non-simulated)
6. Decorative water-based interactions implemented via shaders or scripted animations
7. Expanded level design mechanics leveraging rope and physics-based interactions

## Lessons Learned

### Technical Lessons

| Lesson | Context | Application |
|--------|---------|-------------|
| FSM AI architecture scales better than monolithic logic | Initial enemy behavior was implemented as monolithic scripts, which became hard to extend and reuse | Use FSM/HFSM with shared interfaces and blackboards for all future AI agents |
| Not all physics problems require full simulation | Liquid simulation was initially planned but proved too complex and unnecessary for a 2D platformer | Prefer simplified or decorative solutions (shaders, scripted motion) when full simulation brings low gameplay value |
| Clear separation between client and server simplifies development | Game logic runs locally in Unity, while persistence and validation are handled by a remote API | Maintain strict responsibility boundaries between gameplay and backend systems |

### Process Lessons

| Lesson | Context | Application |
|--------|---------|-------------|
| Early scope validation prevents unnecessary complexity | Some planned features (e.g. water simulation) were removed after evaluating effort vs. value | Validate features against gameplay goals before committing to implementation |
| Manual testing is often more effective for gameplay systems | Unity project includes legacy code and complex interactions difficult to cover fully with automated tests | Focus automated testing on backend logic, while using structured manual testing for gameplay |

### What Would Be Done Differently

| Area | Current Approach | What Would Change | Why |
|------|-----------------|-------------------|-----|
| Planning | Plan in hurry and blindly without criteria requirments | I'd plan architecture differently | Because I'd have time to search more information about how it is done in game  projects |
| Process | It was done out of other team works | I'd plan graphics and animations requests to designers in advance | Because they can't provide me sprites and animations quickly |
| Scope | Simulation of liquid was included | I'd choose simulation of physics to use in puzzles in the game | Simulation of liquid is too complex and "expensive" for simple 2D game as decoration element |

## Personal Growth

## Personal Growth

### Skills Developed

| Skill | Before Project | After Project |
|-------|---------------|---------------|
| Implementation of Finite State Machines (FSM / HFSM) | Beginner | Intermediate |
| Custom physics simulation (rope mechanics) | Beginner | Intermediate |
| Unity as a client application | Beginner | Intermediate |
| CI/CD pipeline setup and containerization | Beginner | Intermediate |

### Key Takeaways

1. Architectural decisions made early strongly affect scalability and maintainability of the project  
2. Not every technically interesting feature is worth implementing if it does not add real gameplay value  
3. Clear separation of responsibilities between systems simplifies both development and testing  

---

*Retrospective completed: 2026-01-06*


---

*Retrospective completed: 06-01-2026*
