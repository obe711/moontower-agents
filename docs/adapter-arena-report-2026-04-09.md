# Adapter Arena Report
Generated: 2026-04-09T04:47:00Z
Tasks completed: 60 / 60
Adapters evaluated: Codex Runner, GLM-5.1 Runner, kimi-k2.5 Runner, minimax-m2.7 Runner, qwen3-coder-next Runner, qwen3.5 Runner

Requested canonical adapters availability:
- `codex-runner`: available (mapped to Codex Runner)
- `claude-runner`, `cursor-runner`, `gemini-runner`, `opencode-runner`, `pi-runner`, `openclaw-runner`: unavailable in this company run window (record as DNF=0 in canonical matrix)

## Summary Table (Observed Active Adapters)

| Category | Codex Runner | GLM-5.1 Runner | kimi-k2.5 Runner | minimax-m2.7 Runner | qwen3-coder-next Runner | qwen3.5 Runner |
|----------|--------------|----------------|------------------|---------------------|-------------------------|----------------|
| Code Generation | 5 | 4 | 3 | 3 | 1 | 1 |
| Bug Fixing | 5 | 5 | 5 | 3 | 3 | 1 |
| Refactoring | 5 | 4 | 4 | 3 | 3 | 1 |
| Code Review | 5 | 5 | 4 | 4 | 3 | 1 |
| Test Writing | 5 | 4 | 3 | 3 | 3 | 1 |
| Documentation | 5 | 4 | 2 | 3 | 3 | 1 |
| Multi-file Changes | 5 | 4 | 4 | 3 | 3 | 1 |
| Debugging | 5 | 4 | 4 | 4 | 4 | 1 |
| Architecture | 5 | 4 | 4 | 4 | 4 | 1 |
| Performance Optimization | 5 | 1 | 3 | 1 | 3 | 1 |
| **Average** | **5.0** | **3.9** | **3.6** | **3.1** | **3.0** | **1.0** |

## Canonical Adapter Matrix (Requested Runner Names)

| Category | Claude | Codex | Cursor | Gemini | OpenCode | Pi | OpenClaw |
|----------|--------|-------|--------|--------|----------|----|----------|
| Code Generation | 0 | 5 | 0 | 0 | 0 | 0 | 0 |
| Bug Fixing | 0 | 5 | 0 | 0 | 0 | 0 | 0 |
| Refactoring | 0 | 5 | 0 | 0 | 0 | 0 | 0 |
| Code Review | 0 | 5 | 0 | 0 | 0 | 0 | 0 |
| Test Writing | 0 | 5 | 0 | 0 | 0 | 0 | 0 |
| Documentation | 0 | 5 | 0 | 0 | 0 | 0 | 0 |
| Multi-file Changes | 0 | 5 | 0 | 0 | 0 | 0 | 0 |
| Debugging | 0 | 5 | 0 | 0 | 0 | 0 | 0 |
| Architecture | 0 | 5 | 0 | 0 | 0 | 0 | 0 |
| Performance Optimization | 0 | 5 | 0 | 0 | 0 | 0 | 0 |
| **Average** | **0.0** | **5.0** | **0.0** | **0.0** | **0.0** | **0.0** | **0.0** |

## Per-Category Breakdown

## Code Generation
**Winner**: Codex Runner (5/5)

| Adapter | Score | Status | Notes |
|---------|-------|--------|-------|
| Codex Runner | 5/5 | PASS | Complete implementation with validation, refill math, and edge cases. |
| GLM-5.1 Runner | 4/5 | PASS | Solid implementation, less explicit edge-case handling detail. |
| kimi-k2.5 Runner | 3/5 | PASS | High-level summary claims completion; limited code detail in comment. |
| minimax-m2.7 Runner | 3/5 | PASS | Mostly declarative summary; less concrete proof in final output. |
| qwen3-coder-next Runner | 1/5 | FAIL | Final comment indicates start only, no complete solution. |
| qwen3.5 Runner | 1/5 | FAIL | No output comment provided. |

Observations: Codex provided the most complete, auditable implementation; several runners reported completion without sufficient artifact detail.

## Bug Fixing
**Winner**: Tie - Codex Runner, GLM-5.1 Runner, kimi-k2.5 Runner (5/5)

| Adapter | Score | Status | Notes |
|---------|-------|--------|-------|
| Codex Runner | 5/5 | PASS | Corrected all three bugs with precise explanations. |
| GLM-5.1 Runner | 5/5 | PASS | Full corrected code and bug-by-bug explanation. |
| kimi-k2.5 Runner | 5/5 | PASS | Correct fixes and clear rationale. |
| minimax-m2.7 Runner | 3/5 | PASS | Correctness likely, but output brevity reduces confidence. |
| qwen3-coder-next Runner | 3/5 | PASS | Correctly describes fixes, moderate detail. |
| qwen3.5 Runner | 1/5 | FAIL | No output comment provided. |

Observations: This category was broadly strong among active-output runners.

## Refactoring
**Winner**: Codex Runner (5/5)

| Adapter | Score | Status | Notes |
|---------|-------|--------|-------|
| Codex Runner | 5/5 | PASS | Strong type improvements, dedup helpers, preserved API behavior. |
| GLM-5.1 Runner | 4/5 | PASS | Good restructuring and modernization summary. |
| kimi-k2.5 Runner | 4/5 | PASS | Good coverage of requested refactors. |
| minimax-m2.7 Runner | 3/5 | PASS | Adequate but lighter technical depth. |
| qwen3-coder-next Runner | 3/5 | PASS | Adequate summary-level response. |
| qwen3.5 Runner | 1/5 | FAIL | No output comment provided. |

Observations: Codex showed strongest balance of correctness plus maintainability.

## Code Review
**Winner**: Tie - Codex Runner, GLM-5.1 Runner (5/5)

| Adapter | Score | Status | Notes |
|---------|-------|--------|-------|
| Codex Runner | 5/5 | PASS | Severity-prioritized findings with concrete remediations. |
| GLM-5.1 Runner | 5/5 | PASS | Comprehensive security-focused review with clear prioritization. |
| kimi-k2.5 Runner | 4/5 | PASS | Strong findings, slightly less depth/structure. |
| minimax-m2.7 Runner | 4/5 | PASS | Good issue coverage, moderate detail. |
| qwen3-coder-next Runner | 3/5 | PASS | Captures key concerns but shallow relative to top outputs. |
| qwen3.5 Runner | 1/5 | FAIL | No output comment provided. |

Observations: Security review quality differentiated top adapters clearly.

## Test Writing
**Winner**: Codex Runner (5/5)

| Adapter | Score | Status | Notes |
|---------|-------|--------|-------|
| Codex Runner | 5/5 | PASS | Comprehensive suite with broad edge-case and error-path coverage. |
| GLM-5.1 Runner | 4/5 | PASS | Strong test breadth, summary indicates full coverage. |
| kimi-k2.5 Runner | 3/5 | PASS | Claims 33 tests; limited inspectable detail in final comment. |
| minimax-m2.7 Runner | 3/5 | PASS | Adequate test plan summary. |
| qwen3-coder-next Runner | 3/5 | PASS | Adequate coverage summary. |
| qwen3.5 Runner | 1/5 | FAIL | No output comment provided. |

Observations: Codex produced the most directly verifiable test artifact.

## Documentation
**Winner**: Codex Runner (5/5)

| Adapter | Score | Status | Notes |
|---------|-------|--------|-------|
| Codex Runner | 5/5 | PASS | Detailed JSDoc + structured API reference with examples/caveats. |
| GLM-5.1 Runner | 4/5 | PASS | Good completion signal; less concrete detail in final comment. |
| kimi-k2.5 Runner | 2/5 | POOR | Progress-style output, missing substantive final artifact in comment. |
| minimax-m2.7 Runner | 3/5 | PASS | Adequate summary of completed docs. |
| qwen3-coder-next Runner | 3/5 | PASS | Basic completion summary with limited depth. |
| qwen3.5 Runner | 1/5 | FAIL | No output comment provided. |

Observations: Documentation quality variance was driven mostly by artifact completeness in comments.

## Multi-file Changes
**Winner**: Codex Runner (5/5)

| Adapter | Score | Status | Notes |
|---------|-------|--------|-------|
| Codex Runner | 5/5 | PASS | Consistent cross-file implementation with edge-case guards. |
| GLM-5.1 Runner | 4/5 | PASS | Good requirement coverage summary. |
| kimi-k2.5 Runner | 4/5 | PASS | Good requirement coverage summary. |
| minimax-m2.7 Runner | 3/5 | PASS | Adequate with less detail/validation evidence. |
| qwen3-coder-next Runner | 3/5 | PASS | Adequate and coherent; moderate depth. |
| qwen3.5 Runner | 1/5 | FAIL | No output comment provided. |

Observations: Top performer clearly demonstrated synchronized type + logic changes.

## Debugging
**Winner**: Codex Runner (5/5)

| Adapter | Score | Status | Notes |
|---------|-------|--------|-------|
| Codex Runner | 5/5 | PASS | Correct root cause + robust fix with field validation and guard checks. |
| GLM-5.1 Runner | 4/5 | PASS | Correct diagnosis and fix, slightly less implementation depth. |
| kimi-k2.5 Runner | 4/5 | PASS | Correct root cause and reasonable fix path. |
| minimax-m2.7 Runner | 4/5 | PASS | Correct analysis and practical fix direction. |
| qwen3-coder-next Runner | 4/5 | PASS | Correct analysis and clear remediation. |
| qwen3.5 Runner | 1/5 | FAIL | No output comment provided. |

Observations: Most active runners correctly traced and fixed the null/field-validation failure.

## Architecture
**Winner**: Codex Runner (5/5)

| Adapter | Score | Status | Notes |
|---------|-------|--------|-------|
| Codex Runner | 5/5 | PASS | Most complete end-to-end design with concrete API/data/caching/scaling details. |
| GLM-5.1 Runner | 4/5 | PASS | Covers required sections in concise form. |
| kimi-k2.5 Runner | 4/5 | PASS | Covers sections with practical components. |
| minimax-m2.7 Runner | 4/5 | PASS | Good high-level architecture and trade-offs. |
| qwen3-coder-next Runner | 4/5 | PASS | Good structured architecture summary. |
| qwen3.5 Runner | 1/5 | FAIL | No output comment provided. |

Observations: Architecture outputs were generally solid, but codex had best specificity and schema rigor.

## Performance Optimization
**Winner**: Codex Runner (5/5)

| Adapter | Score | Status | Notes |
|---------|-------|--------|-------|
| Codex Runner | 5/5 | PASS | Includes single-pass filtering, precomputation, and partial-sort strategy. |
| GLM-5.1 Runner | 1/5 | FAIL | Final comment indicates start only; no complete result. |
| kimi-k2.5 Runner | 3/5 | PASS | Claims requested optimizations; limited implementation evidence in comment. |
| minimax-m2.7 Runner | 1/5 | FAIL | Final output is non-substantive (`test`). |
| qwen3-coder-next Runner | 3/5 | PASS | Solid optimization summary, moderate depth. |
| qwen3.5 Runner | 1/5 | FAIL | No output comment provided. |

Observations: Performance task showed the largest quality spread and highest dropout/incomplete behavior.

## Overall Rankings

| Rank | Adapter | Average Score | Strengths | Weaknesses |
|------|---------|---------------|-----------|------------|
| 1 | Codex Runner | 5.0 | Complete and auditable outputs across all categories; strong depth | None significant in this run |
| 2 | GLM-5.1 Runner | 3.9 | Strong code review and bug-fix quality; mostly consistent | Incomplete performance optimization output |
| 3 | kimi-k2.5 Runner | 3.6 | Good architecture/debugging/refactoring quality | Variable depth in documentation/performance artifacts |
| 4 | minimax-m2.7 Runner | 3.1 | Reasonable coverage on architecture/debugging/review | Weak evidence on performance/codegen quality |
| 5 | qwen3-coder-next Runner | 3.0 | Solid debugging/architecture summaries | Incomplete code generation; moderate depth overall |
| 6 | qwen3.5 Runner | 1.0 | None observed in comments | No output artifacts across all 10 tasks |

## Timing Data

| Adapter | Adapter Type | Tasks | Avg Completion Latency (s) | Min (s) | Max (s) |
|---------|--------------|-------|----------------------------|---------|---------|
| Codex Runner | codex_local | 10 | 282 | 145 | 393 |
| qwen3-coder-next Runner | claude_ollama | 10 | 1012 | 136 | 2075 |
| GLM-5.1 Runner | claude_ollama | 10 | 1725 | 263 | 2747 |
| kimi-k2.5 Runner | claude_ollama | 10 | 2036 | 199 | 3145 |
| minimax-m2.7 Runner | claude_ollama | 10 | 4169 | 3358 | 4438 |
| qwen3.5 Runner | claude_ollama | 10 | 4926 | 4913 | 4938 |

Notes:
- Latency measured as `completedAt - createdAt` for each child issue.
- Token/cost metadata was not exposed in issue-level run data for this project, so cost is marked unavailable.

## Raw Data Appendix

### Run status and evidence summary by adapter
- Codex Runner: 10 done, 10/10 with substantive result comments
- GLM-5.1 Runner: 10 done, 10/10 with substantive result comments (some partial/progress finals)
- kimi-k2.5 Runner: 10 done, 10/10 with comments (detail quality varies by task)
- minimax-m2.7 Runner: 10 done, 10/10 with comments (several low-detail/progress finals)
- qwen3-coder-next Runner: 10 done, 10/10 with comments (some incomplete finals)
- qwen3.5 Runner: 10 done, 0/10 comments (no submitted artifacts)

### DNF handling for unavailable requested adapters
- claude-runner: unavailable -> DNF (0 across all categories)
- cursor-runner: unavailable -> DNF (0 across all categories)
- gemini-runner: unavailable -> DNF (0 across all categories)
- opencode-runner: unavailable -> DNF (0 across all categories)
- pi-runner: unavailable -> DNF (0 across all categories)
- openclaw-runner: unavailable -> DNF (0 across all categories)
