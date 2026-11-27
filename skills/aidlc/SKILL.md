---
name: tcs-security
description: Execute the consolidated AWS AI-DLC workflow with lazy stage loading when explicitly invoked via /tcs security or when an end-to-end development or security lifecycle is requested.
---

# AWS AI-DLC Workflow Skill (`tcs-security-plugin1`)

## Activation Rules
- Run this skill **only** when the user explicitly enters `/tcs security` or requests an end-to-end development or security lifecycle.
- Do **not** run this skill for general questions, standalone architecture requests, or isolated Terraform scan prompts.

## Lazy Stage Loading
- Load **only** the currently active stage from `./stages/` (`initialization`, `ideation`, `inception`, `construction`, `operation`) rather than loading all stages at once.
- Keep per-workspace `.aidlc/` state isolated per project workspace and out of Git commits.
- For Terraform security validation, delegate to `tcs-iac-v1-2` / `aidlc-devsecops` to run real `checkov` and `tfsec` scans against real `.tf` files—never use mock data.