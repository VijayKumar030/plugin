# Review & Execution Guardrails

1. Answer general prompts directly without starting the AI-DLC workflow.
2. Scope architecture-only prompts to `./agents/aidlc-architect-agent.md` and `./knowledge/*`.
3. Enforce real `checkov` and `tfsec` scans on real `.tf` files with zero mock data.
4. Keep `.aidlc/` state and temporary scan files (`checkov-report.json`, `tfsec-report.json`) out of Git commits.