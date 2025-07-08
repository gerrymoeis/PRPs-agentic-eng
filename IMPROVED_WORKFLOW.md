# The Production-Grade Agentic Workflow

This document outlines the complete, end-to-end workflow for developing large-scale, production-quality applications using an AI agent. It integrates structured planning, formal design, and rigorous validation into a cohesive process.

---

## Phase 0: Project Kickstart & Onboarding

**Goal:** To align the AI agent with the project's existing structure, standards, and history.

1.  **Initiation:** The user starts the project using the `KICKSTART_PROMPT_TEMPLATE.md`.
2.  **Codebase Analysis:** The agent recursively scans the entire project to understand its structure.
3.  **Context Synthesis:** The agent reads all configuration (`package.json`, etc.), documentation (`README.md`, `CLAUDE.md`), and existing guides to build a deep understanding of the project's rules and patterns.

## Phase 1: Collaborative Planning & Design

**Goal:** To move from a high-level idea to a detailed, reviewed, and approved technical design.

1.  **Interactive Requirements Gathering:** The agent initiates a structured Q&A session to define the feature's goals, scope, and constraints (scalability, security, etc.).
2.  **Architectural Design Document (ADD) Creation:**
    - The agent uses the `TEMPLATES/ARCHITECTURAL_DESIGN_DOCUMENT.md` to draft a formal design document.
    - This ADD details the proposed architecture, data models, API contracts, and testing strategies.
3.  **Human Review & Approval:** The user (and other stakeholders) reviews the ADD. This is a critical checkpoint to ensure the technical plan is sound before implementation begins. The ADD is updated until it is formally 'Approved'.

## Phase 2: Implementation & Validation

**Goal:** To translate the approved design into high-quality, well-tested code.

1.  **Production PRP Generation:**
    - Using the approved ADD, the agent fills out the `TEMPLATES/PRODUCTION_PRP_TEMPLATE.md`.
    - This creates a detailed, step-by-step implementation plan that includes specific unit, integration, and E2E tests.
2.  **Git Workflow Adherence:** The agent follows the `GUIDES/GIT_WORKFLOW.md`, creating a `feature/*` branch from `develop`.
3.  **Test-Driven Implementation:** The agent executes the PRP, writing tests as defined in the 'Validation Loop' section *before or alongside* the feature code.
4.  **Automated & Manual Validation:** The agent runs all automated tests. The user performs manual QA checks as specified in the PRP. This iterative process continues until all validation criteria are met.

## Phase 3: Deployment & Documentation

**Goal:** To safely deploy the feature to production and document the work for future reference.

1.  **Pull Request & CI/CD:** The agent opens a Pull Request from the feature branch to `develop`. This triggers a CI/CD pipeline that runs all tests automatically.
2.  **Release Management:** Following the Git workflow, the feature is promoted to `main` via a `release/*` branch.
3.  **Deployment & Rollback:** The agent follows the deployment and rollback plans outlined in the PRP.
4.  **Documentation Update:** The agent updates the project's `decisions_and_changes_log.md` and `STATE_OF_THE_PROJECT.md` with a summary of the changes, linking to the ADD and PRP for full context. This ensures the project's knowledge base stays current.

---

## Phase 4: State Management & Recovery

**Goal:** To ensure the development process is resilient to AI context drift and can recover from catastrophic context loss.

This phase runs concurrently with all others and is governed by the principle that **the project's state lives in version control, not the chat history.**

1.  **Continuous State Tracking:**
    - The agent is responsible for keeping the `STATE_OF_THE_PROJECT.md` file meticulously up-to-date after every significant action.

2.  **Course-Correction Protocol:**
    - If the agent deviates from the plan, the user can issue the command **"Cascade, re-synchronize."**
    - This instructs the agent to re-read the `STATE_OF_THE_PROJECT.md` and the active PRP to get back on track.

3.  **Disaster Recovery Protocol:**
    - In the event of a new chat session, the user will initiate the process using the `TEMPLATES/RESUME_PROJECT_PROMPT_TEMPLATE.md`.
    - This allows a new agent instance to quickly onboard itself using the state file and resume work exactly where the previous session left off.

*For full details on these protocols, see `GUIDES/RECOVERY_AND_CORRECTION.md`.*
