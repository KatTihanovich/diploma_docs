# 1. Project Overview

This section covers the business context, goals, and requirements for the project.

## Contents

- [Problem Statement & Goals](problem-and-goals.md)
- [Stakeholders & Users](stakeholders.md)
- [Scope](scope.md)
- [Features](features.md)

## Executive Summary

This diploma project focuses on the design and implementation of the core technical architecture for the cross-platform desktop platformer game Honey & Bunny, developed using Unity. I was responsible for architecting and implementing a scalable and maintainable infrastructure that ensures reliable interaction between internal game systems and external services, including persistent progress storage and communication with a remote database via a REST API. To address these challenges, a modular and extensible architecture was designed. This included the development of a custom server-side API with CI/CD integration and automated testing, as well as the full integration of the Unity client with the backend database. A significant part of the work involved the development of autonomous in-game agents, implemented using finite state machines (FSM/HFSM) combined with a Blackboard pattern, enabling predictable and extensible AI behavior. In addition, custom physical simulations were implemented for interactive elements such as ropes, requiring synchronization between physics logic and gameplay mechanics. The project also addressed cross-platform deployment, resulting in stable builds for Windows and macOS, and ensured correct game state persistence across sessions. As a result, the project delivers a fully functional technical foundation for the game, including a production-ready server API with automated testing and CI/CD, stable AI agent behavior, cross-platform support, and progress saving. The developed solution can be reused and extended in future game development projects and serves as a practical example of applied software engineering in game development.

## Key Highlights

| Aspect | Description |
|--------|-------------|
| **Problem** | Difficulty in creating a stable, scalable, and maintainable technical infrastructure for a cross-platform Unity game, including backend integration and persistent game state. |
| **Solution** | Modular and extensible architecture integrating Unity client, custom server API, and PostgreSQL database, with autonomous agents and physics simulation. |
| **Target Users** | Team Developers |
| **Key Features** | Autonomous enemy agents with FSM/HFSM and Blackboard, physics simulation, saving game progress and server integration, custom server API with persistent game state, CI/CD pipeline, and automated testing for quality assurance. |
| **Tech Stack** | Unity, C#, Java, Spring Boot , PostgreSQL, REST API, GitHub Actions (CI/CD), Docker. |
