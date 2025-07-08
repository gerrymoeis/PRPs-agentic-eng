# State Synchronization & Recovery Guide

This guide outlines the protocols for keeping the AI agent on track and for recovering from a catastrophic context loss (i.e., starting a new chat session mid-project).

The core principle is that **the project's state lives in version-controlled documents, not in the chat history.**

---

## The `STATE_OF_THE_PROJECT.md` File

This file is the single source of truth for the project's current status. It acts as a high-level dashboard and must be kept meticulously up-to-date by the AI agent after every significant action. It tracks:

-   The current feature being developed.
-   A link to the active Architectural Design Document (ADD).
-   A link to the active Production PRP.
-   The precise next step required to advance the project.

## Protocol 1: Course-Correction

**When to use:** When the AI agent seems to be confused, deviating from the plan, or has "gone off the rails."

**Procedure:**

1.  The user issues the simple command: **"Cascade, re-synchronize."**

2.  The AI agent will immediately perform the following actions:
    a.  Stop its current task.
    b.  Read the contents of `STATE_OF_THE_PROJECT.md`.
    c.  Read the 'Next Step' outlined in the linked Production PRP.
    d.  Confirm its understanding by re-stating the goal and the immediate next action.

This process forces the agent to discard its potentially flawed internal state and re-ground itself in the official project plan.

## Protocol 2: Disaster Recovery (New Chat Session)

**When to use:** In the event of a catastrophic context loss where the chat history is gone and a new session with the AI agent must be started.

**Procedure:**

1.  The user starts the new chat session using the `TEMPLATES/RESUME_PROJECT_PROMPT_TEMPLATE.md`.

2.  This prompt will guide the new agent instance through an accelerated onboarding process:
    a.  First, it will read `IMPROVED_WORKFLOW.md` to understand the project's processes.
    b.  Second, it will read `STATE_OF_THE_PROJECT.md` to identify the exact state of the project when the previous session ended.
    c.  Finally, it will review the active ADD and PRP to gain deep context on the current task.

This ensures that a new agent instance can get up to speed and become productive within minutes, without requiring a manual re-explanation of the entire project history.
