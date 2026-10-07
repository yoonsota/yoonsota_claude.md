## Development Workflow

The user explicitly starts each stage. Stay in the current stage until instructed otherwise.

Only the main/controller agent manages workflow stages. Dispatched subagents follow only their assigned task and relevant task-scoped skills.

1. **Research** — Run `deep-research`. If unavailable, use `mattpocock-skills:research` and identify the substitution.

   Research implementation options, technical constraints, relevant industry standards and established practices, and version compatibility. Prefer primary sources and save a cited report.

   **Complete when:** findings and unresolved questions are recorded.

2. **Requirements** — Run `mattpocock-skills:grill-with-docs`. Use the Research artifacts to interview the user and finalize requirements, decisions, and acceptance criteria.

   Use `mattpocock-skills:domain-modeling` when domain terminology, glossary, or ADR work is needed.

   **Complete when:** the user confirms shared understanding and the approved requirements have an identifiable source.

3. **Development** — Run `superpowers:using-superpowers` and follow the workflow it selects.

   Reuse Research and Requirements artifacts. Revisit only unresolved, changed, or contradictory points.

   Apply `andrej-karpathy-skills:karpathy-guidelines` throughout Development for implementation, refactoring, simplification, and review.

   **Complete when:** the selected Superpowers workflow completes its native process.

4. **Final Quality** — After Development is complete, perform one additional independent refinement pass using the approved requirements/spec, actual Git diff, and actual test results as the sources of truth.

   - Run `code-simplifier:code-simplifier`.
   - Run `mattpocock-skills:code-review` for Standards and Spec.
   - Resolve significant findings and re-run affected tests and verification.
   - Re-run affected reviews after material changes.

   **Complete when:** the final result matches the approved requirements/spec, required tests and verification pass, significant findings are resolved or dispositioned, and no confirmed blocker remains.

### Skill & Tool Routing

Reuse existing project evidence before additional external research.

- **Graphify:** Codebase exploration → follow the Graphify rules below.
- **Context7 MCP:** Library APIs and version-specific behavior.
- **GitHub MCP:** Upstream source, issues, releases, and history.
- **NVIDIA `nvidia-skill-finder`:** NVIDIA SDK, hardware, and platform-specific questions.
- **Matt `codebase-design`:** Architecture and module boundaries.
- **Matt `domain-modeling`:** Domain concepts and ADRs.
- **Matt `writing-for-agents`:** Agent-facing instructions.

## graphify

Rules:

- When the user types `/graphify`, invoke the installed `~/.claude/skills/graphify/SKILL.md` before other task work.
- For codebase exploration, first run `graphify query "<question>"` when `graphify-out/graph.json` exists. Use `graphify path "<A>" "<B>"` for relationships and `graphify explain "<concept>"` for focused concepts. Follow the installed skill's `references/query.md` for vocabulary expansion, traversal, provenance, and feedback.
- Use `graphify-out/wiki/index.md` for broad navigation when available.
- Read `graphify-out/GRAPH_REPORT.md` only for broad architecture review or when query/path/explain do not surface enough context.
- Treat graph results as navigation. Verify behavior, API contracts, and edit/review claims against the specific source, diff, or tests they identify. Reuse supplied evidence; do not repeat broad exploration just to validate a scoped claim. If graph evidence is stale or insufficient, inspect the relevant source directly.
- Dirty graph artifacts are expected after updates. PreToolUse guidance does not refresh the graph or prove its freshness.
- After modifying code in a graphed project, run `graphify update .` (AST-only, no API cost), or confirm a hook/watch already completed the equivalent update for those changes. Use the installed skill's `/graphify --update` workflow when semantic document/media content needs refreshing.
