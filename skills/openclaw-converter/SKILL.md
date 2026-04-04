---
name: openclaw-converter
description: >
  Convert OpenClaw skills and agent workspaces into Paperclip-compatible
  Claude Code agents. Use when you need to import an OpenClaw skill package
  (manifest .md + scripts) into a Paperclip skills/ directory, or convert an
  OpenClaw agent workspace (SOUL.md + AGENTS.md + IDENTITY.md) into a Paperclip
  AGENTS.md with heartbeat procedure. Triggers: "convert openclaw skill",
  "import openclaw agent", "convert this skill to paperclip", or when given a
  path to an OpenClaw workspace or skill package.
---

# OpenClaw-to-Paperclip Converter

Convert OpenClaw skills and agents into Claude Code formatted agents and skills
that work with Paperclip's control plane.

## Two Modes

**Mode 1 — Skill Package Conversion**
Source: An OpenClaw skill directory containing a manifest `.md` (YAML frontmatter
with `name` and `description`) alongside scripts, requirements, and documentation.
Target: A Paperclip `skills/<name>/SKILL.md` with optional `references/` directory.

**Mode 2 — Agent Workspace Conversion**
Source: An OpenClaw agent workspace with `SOUL.md`, `AGENTS.md`, and `IDENTITY.md`.
Target: A Paperclip `agents/<role>/AGENTS.md` with heartbeat procedure, plus a
`.paperclip.yaml` adapter entry.

## Workflow

### Step 1 — Detect Source Format

Read the source directory and classify:

- **Skill package**: Directory contains a `.md` file with YAML frontmatter (`name`,
  `description`) alongside executable scripts (`.py`, `.sh`, `.js`), plus optional
  `requirements.txt`, `README.md`, `QUICK_START.md`.
- **Agent workspace**: Directory contains `SOUL.md` + `AGENTS.md` + `IDENTITY.md`
  (the three-file OpenClaw format).
- **Canonical agent-shop agent**: Single `.md` with frontmatter containing `color`,
  `emoji`, `vibe` fields. This is NOT an OpenClaw format — advise using
  `agent-shop/scripts/convert.sh --tool paperclip` instead.

### Step 2 — Read Source Content

**Mode 1 (Skill Package):**
1. Read the manifest `.md` file — extract `name`, `description` from frontmatter
   and the full markdown body.
2. List all executable scripts in the directory.
3. Read `requirements.txt` if present (dependency list).
4. Read `README.md` / `QUICK_START.md` if present (supplementary docs).

**Mode 2 (Agent Workspace):**
1. Read `IDENTITY.md` — extract agent name (first `#` heading) and description.
2. Read `SOUL.md` — extract identity, communication style, and critical rules sections.
3. Read `AGENTS.md` — extract mission, workflow, deliverables sections.

### Step 3 — Map to Paperclip Format

Apply the mapping rules from `references/mapping-rules.md`.

**Mode 1 — Skill Package → SKILL.md:**

Write `skills/<slug>/SKILL.md` with this structure:

```yaml
---
name: <slugified-name>
description: >
  <original description>
---
```

Body structure:
1. **Title** — `# <Name> Skill`
2. **When to Use** — derived from the source description and capabilities list
3. **Preconditions** — API keys, dependencies, tools (from Setup/requirements.txt)
4. **Process** — numbered workflow steps derived from the source Usage/Quick Start
   sections. Rewrite script paths to use the Paperclip skill location:
   `skills/<slug>/scripts/<filename>`
5. **Scripts Reference** — table of scripts with descriptions
6. **Configuration** — environment variables and API keys (from Setup section)

Copy scripts into `skills/<slug>/scripts/`.
Move README/QUICK_START into `skills/<slug>/references/`.

**Mode 2 — Agent Workspace → AGENTS.md:**

Write `agents/<slug>/AGENTS.md` with this structure:

```yaml
---
name: <Name from IDENTITY.md>
title: <Inferred title or ask user>
reportsTo: null
skills:
  - paperclip
---
```

Body structure:
1. **Role preamble** — 1-2 sentence summary from IDENTITY.md description
2. **Guidelines** — communication style and behavioral rules from SOUL.md
3. **Critical Rules** — rules sections from SOUL.md
4. **Heartbeat Procedure** — wrap the AGENTS.md mission/workflow content in the
   standard Paperclip heartbeat structure:

```markdown
## Heartbeat Procedure

### 1. Identity & Context
If not cached, `GET /api/agents/me` for your id, companyId, role, budget.

### 2. Approval Follow-Up
If `PAPERCLIP_APPROVAL_ID` is set, read the approval and act on decision.

### 3. Check Assignments
`GET /api/agents/me/inbox-lite` for assigned tasks.

### 4. Pick Work
Pick `in_progress` tasks first, then `todo`. Skip `blocked` unless unblocked.

### 5. Checkout
`POST /api/issues/{issueId}/checkout` before starting any work.

### 6. Core Work
<< INSERT converted workflow/mission content from source AGENTS.md here >>

### 7. Update Status
Comment on the issue with progress. Update status via PATCH.

### 8. Exit
Always comment on in_progress work before exiting.
```

### Step 4 — Generate .paperclip.yaml Entry

For agent conversions (Mode 2), output a `.paperclip.yaml` snippet:

```yaml
schema: paperclip/v1

agents:
  <agent-slug>:
    adapter:
      type: claude_local
      config:
        dangerouslySkipPermissions: true
```

If the source agent was designed for OpenClaw, also note the `openclaw_gateway`
adapter alternative:

```yaml
  <agent-slug>:
    adapter:
      type: openclaw_gateway
      config:
        url: wss://gateway.example.com
        authToken: <token>
```

### Step 5 — Write Output

Create the target directory structure and write all files:

- Mode 1: `skills/<slug>/SKILL.md`, `skills/<slug>/scripts/`, `skills/<slug>/references/`
- Mode 2: `agents/<slug>/AGENTS.md`, `.paperclip.yaml` entry

### Step 6 — Summarize

Report:
- Source format detected (skill package or agent workspace)
- Files created with paths
- Manual follow-up needed:
  - For agents: set `reportsTo` to the correct manager agent ID
  - For agents: add domain-specific skills to the `skills` list
  - For agents: adjust heartbeat interval in `.paperclip.yaml` routines
  - For skills: install into company library via `POST /api/companies/{id}/skills/import`

## Critical Rules

- **Never discard scripts** during conversion. Always copy them into the output.
- **Slugify names** for directory and file naming: lowercase, hyphens, no special chars.
- **Always add `paperclip`** to the skills list for converted agents.
- **Heartbeat procedure is mandatory** for Paperclip agents — never skip it.
- **Never hardcode secrets.** Document required env vars but use placeholder values.
- **Preserve script functionality.** Update paths in documentation but do not modify
  script source code.
- **One skill = one directory.** Each converted skill gets its own directory under
  `skills/`.

For detailed field mappings and worked examples, see:
- `skills/openclaw-converter/references/mapping-rules.md`
- `skills/openclaw-converter/references/example-conversion.md`
