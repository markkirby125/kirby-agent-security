# Module 1: MCP Connector Pre-Install Verification — Paper.design MCP & Higgsfield API

*Source: kirby-ai-design-system toolstack doctrine (Brad Bonanno, "My Entire AI Design System"). Extends dispatcher §5 (MCP Server Security Standards) with connector-specific verification specs. Consumed by `../../kirby-ai-design-system/SKILL.md` Module 5.*

### **1.1 Scope**
The AI Design System toolstack admits two third-party connectors into the agent environment: the **Paper.design MCP server** (DOM-native canvas control over JSON-RPC from within the design tool's desktop app) and the **Higgsfield API** (multi-model generative image/video engine). Both are treated as hostile until verified under the Zero-Trust standard. Verification is per-version: a reviewed version pin is invalidated by any update.

### **1.2 Paper MCP Server — Verification Pass**
1.  **Transport & exposure:** Confirm the MCP server binds only to the loopback interface of the Paper desktop app (local JSON-RPC endpoint). Reject any build that listens on a non-loopback interface or phones home canvas content without an explicit, documented sync feature the user enabled.
2.  **Tool-surface enumeration:** Enumerate the exposed tool list. The sanctioned surface is layout operations: inspect layers, read/set CSS properties, update text strings, create/position/swap asset layers, reflow frames. Flag and challenge any tool that reads files outside declared asset directories, executes shell commands, or fetches URLs not owned by the design system.
3.  **Permission mapping:** Every enumerated tool maps to a documented capability in the Paper docs; unmapped tools are removed from the allowlist before connection.
4.  **Injection scan:** Run the standard Skill Spectre scan + §4 behavioral phases against the server package — canvas documents are untrusted input (they may contain text from any source), so prompt-injection resistance is in scope, not optional.
5.  **Mutation audit:** Confirm destructive operations (delete layer, clear canvas) require explicit agent invocation — no batch/"clean up" tools that act beyond their named scope.

### **1.3 Higgsfield API Connector — Verification Pass**
1.  **Credential handling:** API key stored in the agent environment's secret store only — never in prompt-transmitted config, markdown files, or canvas documents. Confirm the connector redacts the key from all logs.
2.  **Egress allowlist:** The connector may call only the documented Higgsfield generation endpoints. Reject generic HTTP-proxy tooling ("fetch any URL") wrapped around the API.
3.  **Ingress path:** Generated assets land in a designated, sandboxed asset directory (the canvas slot target). The connector must not execute or parse returned binaries beyond image/video decoding.
4.  **Data-minimization default:** Prompts sent to the generation engine contain creative content only. No environment variables, file contents, or prior conversation context are attached by default; any "context enrichment" feature is disabled at verification time unless explicitly required.

### **1.4 Registration Gate**
Record for each connector: version pin, verified tool/endpoint surface, secret-handling attestation, scan artifacts, and reviewer sign-off. Register in agent configuration only after both gates pass. Re-verify on every version bump or scope change — an auto-updating connector is an unverified connector.
