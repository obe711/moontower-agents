# Example Conversions

## Example 1: Skill Package (ai-video-gen)

### Source: OpenClaw Skill Package

Directory: `ai-video-gen/`

**ai-video-gen.md** (manifest):
```yaml
---
name: ai-video-gen
description: End-to-end AI video generation - create videos from text prompts using image generation, video synthesis, voice-over, and editing.
---
```

Body sections: Capabilities, Quick Start, Setup (API Keys, Dependencies, FFmpeg),
Usage Examples, Workflow Options, Scripts Reference, API Cost Estimates.

Scripts: `generate_video.py`, `images_to_video.py`, `add_voiceover.py`

Other files: `requirements.txt`, `README(1).md`, `QUICK_START.md`

### Output: Paperclip SKILL.md

Directory: `skills/ai-video-gen/`

```
skills/ai-video-gen/
  SKILL.md
  scripts/
    generate_video.py
    images_to_video.py
    add_voiceover.py
    requirements.txt
  references/
    README.md
    QUICK_START.md
```

**skills/ai-video-gen/SKILL.md**:

```markdown
---
name: ai-video-gen
description: >
  End-to-end AI video generation - create videos from text prompts using
  image generation, video synthesis, voice-over, and editing. Supports
  OpenAI DALL-E, Replicate models, LumaAI, Runway, and FFmpeg editing.
---

# AI Video Generation Skill

Generate complete videos from text descriptions using AI image generation,
video synthesis, voice-over, and FFmpeg editing.

## When to Use

Use this skill when you need to:
- Generate images from text prompts (DALL-E 3, Stable Diffusion, Flux)
- Convert images to video (LumaAI, Runway, Replicate)
- Add voice-over narration (OpenAI TTS, ElevenLabs)
- Assemble and edit video with FFmpeg

## Preconditions

### API Keys

At least one image generation and one video generation key required:

| Service | Env Var | Purpose |
|---|---|---|
| OpenAI | `OPENAI_API_KEY` | DALL-E 3 images + TTS voice |
| Replicate | `REPLICATE_API_TOKEN` | Stable Diffusion, Flux images |
| LumaAI | `LUMAAI_API_KEY` | Image-to-video conversion |
| Runway | `RUNWAY_API_KEY` | Video generation |
| ElevenLabs | `ELEVENLABS_API_KEY` | Premium voice-over |

### Dependencies

```bash
pip install -r skills/ai-video-gen/scripts/requirements.txt
```

FFmpeg must be installed and available on PATH.

## Process

### 1. Full Video Pipeline

Generate an image, convert to video, and optionally add narration:

```bash
python skills/ai-video-gen/scripts/generate_video.py \
  --prompt "A futuristic city at night with flying cars" \
  --voiceover "Welcome to the future" \
  --output future_city.mp4
```

Options:
- `--image-model dalle|replicate` (default: dalle)
- `--video-model luma|runway` (default: luma)
- `--voice alloy|echo|fable|onyx|nova|shimmer` (default: alloy)

### 2. Image Sequence to Video

Convert a set of images into a video:

```bash
python skills/ai-video-gen/scripts/images_to_video.py \
  --images frame1.png frame2.png frame3.png \
  --fps 24 \
  --quality high \
  --output animation.mp4
```

### 3. Add Voice-Over

Add narration to an existing video:

```bash
python skills/ai-video-gen/scripts/add_voiceover.py \
  --video input.mp4 \
  --text "Your narration text here" \
  --output final.mp4
```

Use `--mix` to blend with existing audio instead of replacing.

## Scripts Reference

| Script | Description |
|---|---|
| `generate_video.py` | End-to-end pipeline: prompt → image → video → audio |
| `images_to_video.py` | Convert image sequence to video with FFmpeg |
| `add_voiceover.py` | Generate and attach voice-over to existing video |

## Configuration

### Budget Mode (Free)

- Image: Stable Diffusion via Replicate free tier or local
- Video: Open source models
- Voice: OpenAI TTS (~$0.015/1K chars)
- Editing: FFmpeg

### Quality Mode (Paid)

- Image: DALL-E 3 (~$0.04-0.08/image)
- Video: LumaAI ($0-0.50/5sec) or Runway (~$0.05/sec)
- Voice: ElevenLabs (~$0.30/1K chars)
- Editing: FFmpeg
```

---

## Example 2: Agent Workspace

### Source: OpenClaw Agent Workspace

Directory: `frontend-developer/`

**IDENTITY.md**:
```markdown
# Frontend Developer
Expert React and TypeScript developer focused on building responsive,
accessible user interfaces.
```

**SOUL.md**:
```markdown
## Identity
You are a senior frontend developer with deep expertise in React 19,
TypeScript, and modern CSS. You write clean, maintainable components
and prioritize accessibility.

## Communication Style
- Be direct and technical. Skip pleasantries.
- Show code, not prose. Prefer diffs and snippets.
- When reviewing, cite specific line numbers.

## Critical Rules
- Never ship without running `pnpm typecheck`.
- Always use semantic HTML elements.
- Never use `any` type — find or create the correct type.
- Test every component with at least one happy-path test.
```

**AGENTS.md**:
```markdown
## Core Mission
Build and maintain frontend components, pages, and features. Review
pull requests from other developers for UI quality and accessibility.

## Workflow
1. Read the issue description and acceptance criteria.
2. Check existing components in `ui/src/components/` for reuse.
3. Implement the feature with proper TypeScript types.
4. Write tests using Vitest and Testing Library.
5. Run `pnpm typecheck && pnpm test:run` before marking done.
6. Post a summary comment with the files changed.

## Deliverables
- Working React components with TypeScript
- Unit tests for new components
- Updated Storybook stories if applicable
```

### Output: Paperclip AGENTS.md

Directory: `agents/frontend-developer/`

**agents/frontend-developer/AGENTS.md**:

```markdown
---
name: Frontend Developer
title: Frontend Developer
reportsTo: null
skills:
  - paperclip
---

Expert React and TypeScript developer focused on building responsive,
accessible user interfaces. Deep expertise in React 19, TypeScript, and
modern CSS. Writes clean, maintainable components and prioritizes accessibility.

## Guidelines

- Be direct and technical. Skip pleasantries.
- Show code, not prose. Prefer diffs and snippets.
- When reviewing, cite specific line numbers.

## Critical Rules

- Never ship without running `pnpm typecheck`.
- Always use semantic HTML elements.
- Never use `any` type — find or create the correct type.
- Test every component with at least one happy-path test.

## Heartbeat Procedure

### 1. Identity & Context
If not cached, `GET /api/agents/me` for your id, companyId, role, budget.
Store companyId for subsequent calls.

### 2. Approval Follow-Up
If `PAPERCLIP_APPROVAL_ID` is set:
- `GET /api/approvals/{approvalId}` to read the decision.
- If approved: proceed with approved implementation.
- If rejected: revise approach per board feedback.

### 3. Check Assignments
`GET /api/agents/me/inbox-lite` to see assigned tasks.

### 4. Pick Work
Pick `in_progress` tasks first (resume), then `todo` (start new).
Skip `blocked` unless you have new information to unblock.

### 5. Checkout
`POST /api/issues/{issueId}/checkout` before starting any work.
If 409 Conflict: skip — another agent owns this task.

### 6. Core Work
1. Read the issue description and acceptance criteria.
2. Check existing components in `ui/src/components/` for reuse.
3. Implement the feature with proper TypeScript types.
4. Write tests using Vitest and Testing Library.
5. Run `pnpm typecheck && pnpm test:run` before marking done.
6. Post a summary comment with the files changed.

**Deliverables:**
- Working React components with TypeScript
- Unit tests for new components
- Updated Storybook stories if applicable

### 7. Update Status
- Comment on the issue with progress summary and files changed.
- `PATCH /api/issues/{issueId}` with updated status.
- Include `X-Paperclip-Run-Id: $PAPERCLIP_RUN_ID` header.

### 8. Exit
Always comment on in_progress work before exiting.
If blocked, set status to `blocked` with a clear reason.
```

**.paperclip.yaml** entry:

```yaml
schema: paperclip/v1

agents:
  frontend-developer:
    adapter:
      type: claude_local
      config:
        dangerouslySkipPermissions: true

routines:
  frontend-developer-heartbeat:
    triggers:
      - kind: schedule
        cronExpression: "*/5 * * * *"
        timezone: UTC
```
