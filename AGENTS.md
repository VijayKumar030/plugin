# AWS AI-DLC Selective Routing Rules (`tcs-security-plugin1`)

Follow these rules in order for every user message:

1. **General Prompts (Direct Execution):**
   - For ordinary questions, quick explanations, or small standalone tasks, answer directly without starting the AI-DLC workflow or loading unrelated stage/skill files.

2. **Architecture-Only Prompts (Scoped Files Only):**
   - When the user asks for architecture design, microservice structure, DDD patterns, cloud architecture guidance, or an ADR (without `/tcs security`), use ONLY `./agents/aidlc-architect-agent.md` and `./knowledge/architect/*` (plus `./knowledge/aws/*` if AWS guidance is needed).
   - Do NOT trigger the full multi-phase AI-DLC workflow or run Terraform scans for pure architecture prompts.

3. **Terraform Security Prompts (Scoped IaC Skill Only):**
   - When the user asks to scan or validate Terraform files for security issues, use `./skills/tcs-iac-v1-2/SKILL.md` and `./agents/aidlc-devsecops-agent.md`.
   - Always execute real `checkov` and `tfsec` scans against actual `.tf` files in the workspace—never use mock, simulated, or placeholder findings.

4. **Full AI-DLC Workflow (`/tcs security` or End-to-End Lifecycle):**
   - Trigger `./skills/aidlc/SKILL.md` only when the user explicitly enters `/tcs security` or clearly requests a full end-to-end development or security lifecycle.
   - Keep all five phases (`initialization`, `ideation`, `inception`, `construction`, `operation`) inside this single plugin and load only the active stage on demand.