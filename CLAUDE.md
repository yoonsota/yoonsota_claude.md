## Development Workflow

The user explicitly starts each of the four top-level stages: Research, Requirements, Development, and Final Quality. The main agent does not advance between these stages without user instruction.

Within the active stage, follow each skill's native workflow, including its internal transitions and approval requirements.

Only the main/controller agent manages workflow stages.

When dispatching subagents, explicitly provide the task scope, approved constraints, relevant artifact paths, and required skills. Do not assume the parent's activated skills or conversation context are inherited.

<SUBAGENT-STOP>
If you are a dispatched subagent, ignore workflow stages 1–4. Follow your assigned task and relevant task-scoped skills. The Skill & Tool Routing and Graphify rules still apply within your task scope.
</SUBAGENT-STOP>

### 1. Research

Run `deep-research`. If unavailable, use `mattpocock-skills:research` and identify the substitution.

Research implementation options, technical constraints, relevant industry standards and established practices, and version compatibility. Prefer primary sources and save a cited report.

**Complete when:** Findings, supporting sources, technical constraints, and unresolved questions are recorded in an identifiable Research artifact.

### 2. Requirements

Run `mattpocock-skills:grill-with-docs`. Use available Research artifacts to interview the user and finalize requirements, decisions, and acceptance criteria.

Use `mattpocock-skills:domain-modeling` when domain terminology, glossary, or ADR work is needed.

Persist the approved requirements, implementation decisions, scope, and testable acceptance criteria in an identifiable Spec document. Reuse existing approved specifications when sufficient.

**Complete when:** The user confirms shared understanding, an approved Spec is recorded, and no unresolved decisions block Development.

### 3. Development

Run `superpowers:using-superpowers` and follow its selected workflow (Spike, Bounded, or Architectural — SDD/Native).

Build on existing Research and Requirements artifacts, revisiting assumptions when new evidence warrants it.

Apply `andrej-karpathy-skills:karpathy-guidelines` throughout development, including implementation and code review. Keep changes simple, focused, and verifiable.

When delegating implementation or review tasks, the main agent must explicitly provide `andrej-karpathy-skills:karpathy-guidelines` to the relevant subagents.

Defer branch finalization until after Final Quality.

**Complete when:** The applicable Superpowers development, review, and verification steps are complete, with documented Spike findings or verified implementation results.

### 4. Final Quality

When the user explicitly starts Final Quality for implemented changes, perform one independent refinement pass using the approved requirements, actual Git diff, and actual test results as the sources of truth.

1. **Simplification** — Dispatch `code-simplifier:code-simplifier` to simplify the implemented changes while preserving approved behavior and contracts.
2. **Independent Review** — Run `mattpocock-skills:code-review` for Standards and Spec reviews. Use the approved Spec, repository standards, and full development diff. If no formal Spec exists, use the approved task requirements. Ensure uncommitted changes are also covered.
3. **Verification** — Resolve significant findings and re-run affected tests and verification. Repeat affected reviews only when material changes require it.

**Complete when:** The final result matches the approved requirements, affected tests and verification pass, significant findings are resolved or dispositioned, and no confirmed blocker remains.

After Final Quality passes, run `superpowers:finishing-a-development-branch`. Present the available integration options and execute only the user's selected action.

### Skill & Tool Routing

The following routing applies to both the main agent and subagents within their assigned tasks.

Use existing project evidence as a starting point, not unquestionable authority. When credible concerns arise, use relevant skills and tools to verify assumptions and investigate alternatives. Subagents report significant conflicts to the main agent; changes to approved requirements require user approval.

- **Graphify:** Codebase exploration and impact analysis → follow the Graphify rules below.
- **Context7 MCP:** Library APIs, usage patterns, and version-specific behavior.
- **GitHub MCP:** Upstream source, issues, releases, history, and implementation references.
- **NVIDIA `nvidia-skill-finder`:** NVIDIA SDK, hardware, and platform-specific questions.
- **Matt `codebase-design`:** Use as a supporting skill during Requirements or Superpowers brainstorming when module responsibilities, interface complexity, or architectural seams require deeper design analysis. Reuse approved design decisions and avoid unnecessary redesign.
- **Matt `domain-modeling`:** Domain concepts and ADRs.
- **Matt `writing-for-agents`:** Agent-facing instructions.

**Examples by Stage**

1. **Research**
   - Investigate JetPack/DeepStream compatibility → NVIDIA + Context7.
   - Compare upstream implementations, known issues, and releases → GitHub MCP.

2. **Requirements**
   - Clarify domain concepts, terminology, and architectural decisions → Matt `domain-modeling`.
   - Define module responsibilities, interfaces, and boundaries → Matt `codebase-design`.

3. **Development**
   - Trace code relationships and assess change impact → Graphify.
   - Resolve unexpected API behavior or implementation questions → Context7, GitHub MCP, or NVIDIA.
   - Create or refine agent-facing project instructions → Matt `writing-for-agents`.

4. **Final Quality**
   - Investigate suspicious dependencies or unintended impacts discovered during review → Graphify.
   - Verify questionable SDK usage, API contracts, or upstream behavior → Context7, GitHub MCP, or NVIDIA.
   - Examine architectural concerns raised by reviewers → Matt `codebase-design`.

These are examples, not mandatory tool calls. Select tools based on the task and available evidence.

Skill and tool usage supports the current stage or delegated task; it does not authorize workflow transitions.

## graphify

Rules:

- When the user types `/graphify`, invoke the installed `~/.claude/skills/graphify/SKILL.md` before other task work.
- For codebase exploration, first run `graphify query "<question>"` when `graphify-out/graph.json` exists. Use `graphify path "<A>" "<B>"` for relationships and `graphify explain "<concept>"` for focused concepts. Follow the installed skill's `references/query.md` for vocabulary expansion, traversal, provenance, and feedback.
- Use `graphify-out/wiki/index.md` for broad navigation when available.
- Read `graphify-out/GRAPH_REPORT.md` only for broad architecture review or when query/path/explain do not surface enough context.
- Treat graph results as navigation. Verify behavior, API contracts, and edit/review claims against the specific source, diff, or tests they identify. Reuse supplied evidence; do not repeat broad exploration just to validate a scoped claim. If graph evidence is stale or insufficient, inspect the relevant source directly.
- Dirty graph artifacts are expected after updates. PreToolUse guidance does not refresh the graph or prove its freshness.
- After modifying code in a graphed project, run `graphify update .` (AST-only, no API cost), or confirm a hook/watch already completed the equivalent update for those changes. Use the installed skill's `/graphify --update` workflow when semantic document/media content needs refreshing.
