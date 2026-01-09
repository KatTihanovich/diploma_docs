# Problem Statement & Goals (Simplified Version)

## Context

*Honey & Bunny* is a 2D platformer with elements of psychological drama. Players control Bunny, exploring the inner world of consciousness, solving puzzles, and interacting with manifestations of emotions. The project aims to create a fully interactive product integrating artistic, psychological, and technical components.

The diploma project focuses on developing key technical systems: autonomous agents (FSM/HFSM), physics simulations for objects, and a backend API with a database for saving player progress. These systems provide the foundation for further level design, story content, animations, and visual effects.

## Problem Statement

**Who:** Honey & Bunny developers and players.
**What:** Existing third-party solutions are limited, causing instability, complicating feature expansion, and restricting progress saving.
**Why:** Without scalable architecture, the team cannot efficiently add content, and players experience bugs and data loss. In-house solutions ensure stability, independence, and a high-quality user experience.

## Pain Points

* No centralized storage for progress across devices
* Unstable enemy and object behavior without modular autonomous agents
* Lack of automated build and testing (CI/CD) complicates maintenance
* Direct Unity-to-database connections pose security risks

## Business Goals

* Develop a stable cross-platform application (Windows/macOS) with progress saved via API
* Create autonomous agents with diverse behavior and synchronized via a blackboard system
* Implement physics simulations for objects and water with correct interactions
* Ensure reliable backend development and testing: automated builds, CI/CD, Docker

## Objectives & Metrics

* Full implementation of functionality: agents, physics, database integration
* Code coverage by automated tests ≥70%
* Stable builds through CI/CD
* Smooth gameplay with multiple agents
* API ensures proper saving and loading of progress

## Success Criteria

**Must Have:**

* Implementation of key functionality (agents, physics, database)
* Test coverage ≥70%
* Stable CI/CD builds
* Cross-platform operation without critical errors
* Correct integration of all modules
* Stable agent behavior and physics

**Nice to Have:**

* Exceed minimum test coverage
* High performance (FPS)
* Full integration of visual and audio content

## Non-Goals

* Development of graphics, animations, and character models
* Creation of main storyline or quests
* Online features, multiplayer, shops, microtransactions
* Creation of a custom game engine
* Analytics and marketing reports
* Additional levels beyond the demo
