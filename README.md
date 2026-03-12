# Clean Architecture .NET Template

## Repository Description

This repository provides a structured **.NET solution template** inspired by the principles described in *Clean Architecture* by Robert C. Martin, combined with official Microsoft documentation and widely adopted industry practices.

The structure presented here is a **suggested architectural baseline**, not a rigid framework. Its goal is to demonstrate how to organize a .NET solution so that core business logic remains independent from infrastructure, delivery mechanisms, and external technologies.

---

## Architectural Principles

This template emphasizes:

- ✅ **The Dependency Rule** (dependencies point inward)
- ✅ Clear separation of:
  - Domain
  - Application
  - Infrastructure
  - Presentation
- ✅ **Ports and Adapters** (plugin-style architecture)
- ✅ Replaceable frameworks and external services
- ✅ Testable and maintainable business policies
- ✅ Explicit naming conventions and architectural guardrails

---

## Solution Structure Philosophy

Each project in the solution has a clearly defined responsibility and is supported by documentation explaining:

- Its purpose  
- Its architectural boundaries  
- Its design intent  

The repository also includes example projects to illustrate how to apply Clean Architecture concepts in real-world scenarios involving:

- HTTP APIs  
- Messaging  
- Persistence  
- External integrations  

---

## Intended Usage

This repository is designed to serve as:

- 📘 An onboarding reference for developers  
- 🎓 A teaching tool for Clean Architecture within the organization  
- 🏗️ A foundation for building production-ready .NET solutions aligned with architectural best practices  

---

## Goal

The structure aims to promote:

- Clarity  
- Consistency  
- Long-term maintainability  

…especially in systems that are expected to evolve over time.

---

> Architecture should make change easier, not harder.  
> This template exists to support that goal.

## High-Level Architecture

             ┌──────────────────────────────┐
             │        Presentation          │
             │  (API, UI, Controllers)      │
             └───────────────┬──────────────┘
                             │
                             ▼
             ┌──────────────────────────────┐
             │         Application          │
             │  (Use Cases, DTOs, Ports)    │
             └───────────────┬──────────────┘
                             │
                             ▼
             ┌──────────────────────────────┐
             │            Domain            │
             │ (Entities, Value Objects,    │
             │  Business Rules)             │
             └──────────────────────────────┘
                             ▲
                             │
             ┌───────────────┴──────────────┐
             │        Infrastructure        │
             │ (EF Core, External APIs,     │
             │  Messaging, File System)     │
             └──────────────────────────────┘
