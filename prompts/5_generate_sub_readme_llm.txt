You're an AI assistant tasked with generating a scoped `README.llm` file for a specific subdirectory (e.g., `./tf/`) within a larger monorepo.

This file should help LLMs understand the purpose, structure, and modification rules specific to the infra or tooling contained in this subdir—without leaking details from unrelated parts of the codebase.

### Context Sources:
1. Files within the target subdirectory (e.g., Terraform modules, deployment configs, helper scripts)
2. `gitingest` output scoped to that directory
3. The repo’s `package.json` if relevant to builds/deployments
4. The README_TEMPLATE.llm as a base for the `<rules>` block

---

### Output Format (in a single `xml` markdown block):

```xml
<rules>
  Use the `<rules>` section from `README_TEMPLATE.llm` as a base.
  Add any additional Terraform or deployment-specific rules inferred from this subdirectory.
</rules>

<structure>
  Summarize key files and modules within the subdirectory.
  Example:
    /tf/
      main.tf – Root Terraform config
      deployment_manifest.json – Custom deployment instruction set
      modules/ – Shared infra modules used across environments
</structure>

<description>
  Briefly describe the infra or workflow purpose of this directory (e.g., defines shared VPCs, pipelines, environments).
</description>

<context>
  List and describe key resources, modules, or input/output interfaces that might be referenced by automation or other modules.
</context>
```

---

### Guidelines:

- Focus **only** on what’s in the scope of the directory (e.g., `/tf`, `/k8s-tf`, `/src/services`).
- Do not repeat logic from unrelated parts of the repo (e.g., application code or unrelated configs).
- Keep the output concise and structured. Favor inference from real file content over assumptions.