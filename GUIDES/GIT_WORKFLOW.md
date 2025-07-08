# Production-Grade Git Workflow Guide

This document outlines the standardized Git workflow for this project. Adhering to this process is crucial for maintaining a clean, scalable, and manageable codebase.

## Branching Strategy: GitFlow

We will use a simplified GitFlow model. This model is designed to manage features, releases, and hotfixes in a structured way.

### Core Branches

1.  **`main`**
    -   **Purpose:** This branch represents the official, production-ready release history.
    -   **Rules:**
        -   Code on `main` must always be stable and deployable.
        -   Direct commits to `main` are strictly forbidden.
        -   Code gets onto `main` only by merging from a `release/*` or `hotfix/*` branch.
        -   Each merge to `main` must be tagged with a version number (e.g., `v1.0.0`).

2.  **`develop`**
    -   **Purpose:** This is the primary development branch, representing the latest delivered development changes for the next release.
    -   **Rules:**
        -   This branch is the integration point for all completed features.
        -   Direct commits to `develop` are forbidden.
        -   Code gets onto `develop` only by merging a `feature/*` branch.

### Supporting Branches

These branches have a limited lifetime and are used to manage specific tasks.

1.  **Feature Branches (`feature/*`)**
    -   **Purpose:** To develop new features.
    -   **Naming Convention:** `feature/[ticket-id]-[short-description]` (e.g., `feature/PROJ-123-user-authentication`)
    -   **Workflow:**
        1.  Branch off from `develop`.
        2.  Work on the feature, making regular commits.
        3.  When complete, open a Pull Request (PR) to merge back into `develop`.
        4.  Once the PR is reviewed, approved, and passes all automated checks, it can be merged.
        5.  The feature branch is deleted after the merge.

2.  **Release Branches (`release/*`)**
    -   **Purpose:** To prepare for a new production release. This branch is for final bug fixes, documentation generation, and other release-oriented tasks.
    -   **Naming Convention:** `release/v[version-number]` (e.g., `release/v1.2.0`)
    -   **Workflow:**
        1.  Branch off from `develop` when it is feature-complete for the next release.
        2.  Perform final testing and fix any bugs directly on this branch.
        3.  Once stable, merge into `main` and tag the commit with the version number.
        4.  Merge any changes made in the release branch back into `develop` to ensure `develop` also has the bug fixes.
        5.  The release branch is deleted after the merges.

3.  **Hotfix Branches (`hotfix/*`)**
    -   **Purpose:** To quickly patch a critical bug in production.
    -   **Naming Convention:** `hotfix/[short-description]` (e.g., `hotfix/fix-login-bug`)
    -   **Workflow:**
        1.  Branch off from `main`.
        2.  Fix the bug and bump the version number.
        3.  Merge back into `main` and tag the new version.
        4.  Merge back into `develop` to ensure the fix is included in future releases.
        5.  The hotfix branch is deleted.

## Commit Message Convention

We will follow the **Conventional Commits** specification. This creates an explicit commit history, which makes it easier to track features, fixes, and breaking changes.

**Format:** `<type>[optional scope]: <description>`

-   **`feat`**: A new feature.
-   **`fix`**: A bug fix.
-   **`docs`**: Documentation only changes.
-   **`style`**: Changes that do not affect the meaning of the code (white-space, formatting, etc).
-   **`refactor`**: A code change that neither fixes a bug nor adds a feature.
-   **`perf`**: A code change that improves performance.
-   **`test`**: Adding missing tests or correcting existing tests.
-   **`chore`**: Changes to the build process or auxiliary tools and libraries.

**Example:** `feat(api): add user registration endpoint`
