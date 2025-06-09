You're an AI assistant tasked with generating a `README.llm` file for this codebase. This file is used to guide LLMs in understanding and generating code for the repo with minimal hallucination.

Use the following sources of context:
1. The existing `README.md` file — to extract purpose, concepts, and descriptions already captured by the team.
2. The output of `gitingest` — a structured summary of the repo's modules, exports, and file contents.
3. The base `README.llm` template.

Your goal:
- Codify a high-signal, LLM-friendly `README.llm` file that aligns with the template provided.
- Prioritize concise, precise, and practical information to support LLM-based code generation and comprehension.
- Extract high-signal context: public interfaces, patterns, Kafka topics, external dependencies.

---
Use this format for the final output:
```xml
<rules>
  <!-- Development practices and architectural conventions for modifying this code. -->
  Use the `<rules>` section from the `README_TEMPLATE_MFE.llm` file as your base. Add or override only when there are additional rules or project-specific conventions observed in the codebase (from README.md or gitingest).
</rules>

<structure>
<!-- overview of the codebase structure and filepaths -->
Example:
  /src/
    app.tsx – Entrypoint component
    components/ – Reusable UI elements (e.g., nav-rail, avatar-menu)
    gql/ – GraphQL queries, fragments, and mutations
</structure>

<description>
  <!-- Purpose, key concepts, usage patterns, integrations, and dependencies. -->
</description>

<context>
  <!-- key function signatures and compact example usage -->
</context>
```
---

Guidelines:
- Do not fabricate missing details — only use information inferable from README.md or gitingest content.
- Prioritize high-signal concepts: public APIs, event contracts, Kafka topics, LaunchDarkly flags, key modules.
- Prefer brevity over verbosity. Minimize boilerplate or generic scaffolding.
- Avoid rewriting unrelated documentation verbatim.
- Follow the conventions shown in the sample `README.llm` provided in this repo.

Optional utilities:
- The Confluence MCP tool to read any linked docs in the `README.md`.