---
name: tcs-security
description: Execute the consolidated 5-phase (33-stage) AWS AI-DLC workflow with lazy stage loading when explicitly invoked via /tcs security or when an end-to-end development or security lifecycle is requested.
---

# AWS AI-DLC Workflow Skill (`tcs-security-plugin1`)

## Activation Guard
- Run this skill **only** when the user explicitly enters `/tcs security` or clearly requests an end-to-end software/infrastructure development or security lifecycle.
- Do **not** run this skill for general Q&A, quick edits, standalone architecture requests, or isolated Terraform scan prompts.

## Consolidated Phases & Lazy Loading
All five AI-DLC phases live inside `./stages/` within this single plugin:
1. `./stages/initialization/`
2. `./stages/ideation/`
3. `./stages/inception/`
4. `./stages/construction/`
5. `./stages/operation/`

### Rules for Execution
- **Lazy Stage Loading:** Read and load **only** the currently active phase and stage file needed for the current step. Never preload all 33 stages into context at once.
- **State Isolation:** Store per-project workflow state in `./.aidlc/` inside the target project workspace (never inside `tcs-security-plugin1`), and ensure `./.aidlc/` is ignored in Git.
- **Real Security Validation:** When reaching infrastructure/IaC or security validation stages, delegate to `tcs-iac-v1-2` / `aidlc-devsecops` to run real `checkov` and `tfsec` scans against actual `.tf` files—never use mock or placeholder findings.
