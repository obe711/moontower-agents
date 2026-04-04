# Mapping Rules: OpenClaw → Paperclip

## Mode 1 — Skill Package Conversion

### Frontmatter Mapping

| OpenClaw Source Field | Paperclip SKILL.md Field | Transformation |
|---|---|---|
| `name` | `name` | Slugify: lowercase, hyphens, strip special chars |
| `description` | `description` | Wrap in YAML `>` multiline block |

### Body Section Mapping

| OpenClaw Section | Paperclip Section | Notes |
|---|---|---|
| `## Capabilities` | **When to Use** | Reframe as "use this skill when you need to..." |
| `## Quick Start` | **Process** (steps) | Convert examples into numbered workflow steps |
| `## Setup` / `### Required API Keys` | **Preconditions** | List env vars, dependencies, external tools |
| `## Setup` / `### Install Dependencies` | **Preconditions** | Include pip/npm install commands |
| `## Usage Examples` | **Process** (steps) | Merge into workflow steps with concrete commands |
| `## Workflow Options` | **Configuration** | Document budget vs quality modes |
| `## Scripts Reference` | **Scripts Reference** | Keep as table: script name, description |
| `## API Cost Estimates` | **Configuration** | Include in Configuration section |

### Script Path Rewriting

OpenClaw skills reference scripts relative to a `skills/` prefix:
```
python skills/ai-video-gen/generate_video.py --prompt "..."
```

After conversion, rewrite to Paperclip skill location:
```
python skills/<slug>/scripts/generate_video.py --prompt "..."
```

### File Placement

| Source File | Target Location |
|---|---|
| Manifest `.md` | Consumed → becomes `SKILL.md` content |
| `*.py`, `*.sh`, `*.js` scripts | `skills/<slug>/scripts/` |
| `requirements.txt` | `skills/<slug>/scripts/requirements.txt` |
| `README.md` | `skills/<slug>/references/README.md` |
| `QUICK_START.md` | `skills/<slug>/references/QUICK_START.md` |
| Other docs | `skills/<slug>/references/` |

---

## Mode 2 — Agent Workspace Conversion

### Source File Roles

| OpenClaw File | Content | Role |
|---|---|---|
| `IDENTITY.md` | `# emoji Name` + vibe/description | Agent identity — provides name and title |
| `SOUL.md` | Identity, communication style, critical rules | Persona — provides guidelines and rules |
| `AGENTS.md` | Mission, workflow, deliverables | Operations — provides core work procedure |

### Frontmatter Mapping

| Source | Paperclip AGENTS.md Field | Transformation |
|---|---|---|
| IDENTITY.md `# heading` | `name` | Strip emoji prefix, use the name text |
| IDENTITY.md `# heading` | `title` | Derive title (e.g., "Frontend Developer" → "Frontend Developer"). Ask user if ambiguous. |
| — | `reportsTo` | Default `null`. User sets to manager agent ID. |
| — | `skills` | Default `[paperclip]`. Add domain skills as needed. |

### Body Section Mapping

| Source Section | Target Section | Notes |
|---|---|---|
| IDENTITY.md body | **Role preamble** | 1-2 sentence summary at top of body |
| SOUL.md `## Identity` | **Role preamble** | Merge with IDENTITY.md content |
| SOUL.md `## Communication` / `## Style` | **Guidelines** | Behavioral and communication rules |
| SOUL.md `## Critical Rules` / `## Rules You Must Follow` | **Critical Rules** | Preserve verbatim |
| AGENTS.md `## Mission` / `## Core Mission` | Heartbeat **Step 6: Core Work** | Primary responsibility |
| AGENTS.md `## Workflow` | Heartbeat **Step 6: Core Work** | Step-by-step procedure |
| AGENTS.md `## Deliverables` | Heartbeat **Step 6: Core Work** | Expected outputs |
| All other AGENTS.md sections | Heartbeat **Step 6: Core Work** | Append in order |

### Heartbeat Procedure Template

All Paperclip agents must follow the heartbeat model. Wrap the converted workflow
content in this template:

```markdown
## Heartbeat Procedure

### 1. Identity & Context
If not cached, `GET /api/agents/me` for your id, companyId, role, budget.
Store companyId for subsequent calls.

### 2. Approval Follow-Up
If `PAPERCLIP_APPROVAL_ID` is set:
- `GET /api/approvals/{approvalId}` to read the decision
- If approved: proceed with approved work
- If rejected: adjust approach per feedback

### 3. Check Assignments
`GET /api/agents/me/inbox-lite` to see assigned tasks.

### 4. Pick Work
- Pick `in_progress` tasks first (resume), then `todo` (start new).
- Skip `blocked` tasks unless you have new information to unblock.
- If `PAPERCLIP_WAKE_COMMENT_ID` is set, read that comment first.

### 5. Checkout
`POST /api/issues/{issueId}/checkout` — must do before starting any work.
If 409 Conflict: another agent owns this task. Move to next task.

### 6. Core Work
<< CONVERTED WORKFLOW CONTENT GOES HERE >>

### 7. Update Status
- Comment on the issue with progress summary.
- `PATCH /api/issues/{issueId}` with updated status.
- Include `X-Paperclip-Run-Id: $PAPERCLIP_RUN_ID` header on all mutations.

### 8. Exit
Always comment on in_progress work before exiting.
If blocked, set status to `blocked` with a clear reason.
```

### .paperclip.yaml Template

```yaml
schema: paperclip/v1

agents:
  <agent-slug>:
    adapter:
      type: claude_local
      config:
        dangerouslySkipPermissions: true

routines:
  <agent-slug>-heartbeat:
    triggers:
      - kind: schedule
        cronExpression: "*/5 * * * *"
        timezone: UTC
```

---

## Slugification Rules

Convert names to directory-safe slugs:

1. Lowercase the entire string
2. Replace spaces and non-alphanumeric characters with hyphens
3. Collapse consecutive hyphens into one
4. Strip leading and trailing hyphens

Examples:
- `AI Video Gen` → `ai-video-gen`
- `Frontend Developer` → `frontend-developer`
- `CEO` → `ceo`
- `UX/UI Designer` → `ux-ui-designer`
