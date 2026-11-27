---
name: tcs-iac-v1-2
description: Scan Terraform configurations using real Checkov and TFSec CLI executions before deployment with zero mock data.
---

# Terraform IaC Security Scan Skill (`tcs-iac-v1-2`)

## Zero-Mock-Data Policy
- **NEVER** generate mock, simulated, hardcoded, or placeholder scan findings.
- Every finding, rule ID, severity, resource name, and file/line reference must come from live `checkov` and `tfsec` CLI runs against actual `.tf` files in the workspace.
- If no `.tf` files exist in the workspace, report clearly that no Terraform files were found instead of inventing sample findings.

## Execution Steps
1. Search the workspace for `.tf` files; if none exist, stop and report that clearly.
2. Verify `checkov` and `tfsec` are available in the environment (`which checkov tfsec`), attempting installation if missing and reporting if blocked.
3. Run real scans on the Terraform files:
   ```bash
   checkov -d . --framework terraform -o json > checkov-report.json
   tfsec . --format json > tfsec-report.json