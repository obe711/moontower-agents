---
name: arena-report
description: Generate a structured comparison report for Adapter Arena benchmark results. Use after all runner agents have completed their tasks and results need to be compiled into a comparative analysis.
version: 0.1.0
---

# Arena Report

Generate the Adapter Arena comparison report from collected benchmark results.

## When to Use

Use this skill after all runner agents have completed all benchmark tasks and posted their structured results as task comments.

## Report Format

### Header

```markdown
# Adapter Arena Report
Generated: <timestamp>
Tasks completed: <N> / <total>
Adapters evaluated: <list>
```

### Summary Table

```markdown
| Category | Claude | Codex | Cursor | Gemini | OpenCode | Pi | OpenClaw |
|----------|--------|-------|--------|--------|----------|----|----------|
| Code Generation | X | X | X | X | X | X | X |
| Bug Fixing | X | X | X | X | X | X | X |
| Refactoring | X | X | X | X | X | X | X |
| Code Review | X | X | X | X | X | X | X |
| Test Writing | X | X | X | X | X | X | X |
| Documentation | X | X | X | X | X | X | X |
| Multi-file Changes | X | X | X | X | X | X | X |
| Debugging | X | X | X | X | X | X | X |
| Architecture | X | X | X | X | X | X | X |
| Performance Optimization | X | X | X | X | X | X | X |
| **Average** | **X.X** | **X.X** | **X.X** | **X.X** | **X.X** | **X.X** | **X.X** |
```

### Per-Category Breakdown

For each of the 10 categories, include:

```markdown
## <Category Name>

**Winner**: <adapter name> (score: X/5)

### Results by adapter

| Adapter | Score | Status | Notes |
|---------|-------|--------|-------|
| Claude | X/5 | PASS | ... |
| Codex | X/5 | PASS | ... |
| Cursor | X/5 | PASS | ... |
| Gemini | X/5 | PASS | ... |
| OpenCode | X/5 | PASS | ... |
| Pi | X/5 | PASS | ... |
| OpenClaw | X/5 | PASS | ... |

### Observations
<qualitative comparison of approaches taken by different adapters>
```

### Overall Rankings

```markdown
## Overall Rankings

| Rank | Adapter | Average Score | Strengths | Weaknesses |
|------|---------|---------------|-----------|------------|
| 1 | ... | X.X | ... | ... |
| 2 | ... | X.X | ... | ... |
| 3 | ... | X.X | ... | ... |
| 4 | ... | X.X | ... | ... |
| 5 | ... | X.X | ... | ... |
| 6 | ... | X.X | ... | ... |
| 7 | ... | X.X | ... | ... |
```

## Scoring Rubric

Apply these criteria uniformly across all tasks and adapters:

- **5 - Excellent**: Correct, complete, well-structured, follows best practices, handles edge cases
- **4 - Good**: Correct and complete, minor style or structure issues
- **3 - Adequate**: Mostly correct, some gaps or minor issues
- **2 - Poor**: Partially correct, significant gaps or errors
- **1 - Failing**: Incorrect, incomplete, or fundamentally flawed approach
- **0 - DNF**: Agent failed to run, timed out, or did not produce output

## Evaluation Dimensions

For each task result, consider:

1. **Correctness** -- Does the output satisfy the task requirements?
2. **Completeness** -- Are all parts of the task addressed?
3. **Quality** -- Code style, structure, best practices
4. **Insight** -- Does the agent show understanding beyond the literal task?
5. **Efficiency** -- Is the solution practical and performant?

## Process

1. Collect all task results from runner agents' task comments
2. Parse the structured result format (Status, Output, Notes)
3. Score each result using the rubric and task-specific evaluation criteria
4. Generate the summary table
5. Write per-category breakdowns
6. Compute averages and produce rankings
7. Write the final report as a markdown document
