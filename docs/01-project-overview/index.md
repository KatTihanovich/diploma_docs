# 1. Project Overview

This section covers the business context, goals, and requirements for the project.

## Contents

- [Problem Statement & Goals](problem-and-goals.md)
- [Stakeholders & Users](stakeholders.md)
- [Scope](scope.md)
- [Features](features.md)

## Executive Summary

The project involves the development and integration of key technical components for the cross-platform desktop platform game Honey & Bunny on Unity. It solves the problem of creating a stable, scalable, and manageable technical infrastructure that ensures the correct interaction of game systems with external resources, including saving progress and working with a remote database via REST API. The main beneficiaries of the project are student developers, the game development team, and end users. The problem is solved through a modular and extensible architecture: creation of a server API with CI/CD support and automated testing, integration of the client part on Unity with the database, implementation of autonomous game agents using FSM/HFSM and Blackboard, simulation of physical processes (vines, dynamic water) and cross-platform build for Windows and macOS. Key results include: a supported server API with automated testing and CI/CD; stable operation of autonomous game agents; cross-platform build and correct progress saving through database integration.

## Key Highlights

| Aspect | Description |
|--------|-------------|
| **Problem** | Difficulty in creating a stable, scalable, and maintainable technical infrastructure for a cross-platform Unity game, including backend integration and persistent game state. |
| **Solution** | Modular and extensible architecture integrating Unity client, custom server API, and PostgreSQL database, with autonomous agents and physics simulation. |
| **Target Users** | Team Developers |
| **Key Features** | Autonomous enemy agents with FSM/HFSM and Blackboard, physics simulation, saving game progress and server integration, custom server API with persistent game state, CI/CD pipeline, and automated testing for quality assurance. |
| **Tech Stack** | Unity, C#, Java, Spring Boot , PostgreSQL, REST API, GitHub Actions (CI/CD), Docker. |
