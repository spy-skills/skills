# doc-coauthoring

## Đánh giá (Score 8.0/10)

| Tiêu chí | Score | Rationale |
|-----------|-------|-----------|
| Completeness | 8 | Full 3-stage workflow with clear exit conditions per stage. Handles both artifact-capable and no-artifact environments. |
| Usability | 9 | Conversational style, shorthand-friendly ("1: yes, 2: see #channel"). Progressive questioning adapts to user's communication style. |
| Modularity | 7 | Single file (375L), no bundled resources. Workflow is linear — hard to use only Stage 2 without Stage 1. |
| Safety | 8 | Reader Testing stage (Stage 3) explicitly catches blind spots. "Fresh Claude with no context" verification. |

**Trung bình: 8.0/10**

## Ưu điểm

1. **3-stage workflow addresses root cause of bad docs** — Stage 1 (Context Gathering) closes the knowledge gap FIRST, before writing anything. Most doc failures happen because writer skips context gathering. This forces "dump everything, organize later."

2. **Brainstorm → Curate → Draft per section** — Stage 2 generates 5-20 options per section, user curates, then Claude drafts. This prevents both blank page syndrome AND one-shot drafts that miss angles. Pattern: diverge → converge → refine.

3. **Reader Testing with "fresh Claude"** — Stage 3 tells user to open new Claude session, paste doc, ask questions. If fresh Claude (no context) gets confused, readers will too. Brilliant self-check that catches context leakage and jargon.

4. **Integration-aware** — Detects Slack/Teams/Google Drive connectors. If available, reads channels and docs directly. If not, suggests enabling connectors or pasting content. Adapts to environment.

5. **Shorthand-friendly interaction** — "1: yes, 2: see #channel, 3: no because backwards compat." Reduces friction for busy users. Respects user's time.

## Nhược điểm

1. **No template library** — Single workflow for all doc types (PRD, decision doc, spec, proposal). No type-specific guidance on what sections are typical. Stage 2 "suggest 3-5 sections" is generic.

2. **Linear-only workflow** — Must go Stage 1→2→3 in order. No support for partially-written docs, collaborative editing, or resuming mid-stage. If session breaks, loses all Stage 1 context.

## Khả năng tích hợp vào hệ thống hiện tại

- **Workflow pattern reusable** — The Context Gathering → Refinement → Testing 3-stage can be adapted for ANY writing task (blog posts, emails, code reviews). Not limited to docs.
- **Integrates with /viec ghi** — Stage 1 context gathering outputs can feed into self-explores/context/ for future reference.
- **Reader Testing principle** — Apply to any output: "Would a fresh Claude understand this?" as quality bar.

## Ghi chú kỹ thuật (Technical Decisions)

### Architecture: Pure Methodology Skill
- **No scripts, no references, no assets** — Entire skill is conversation workflow guidance
- **375 lines of procedural knowledge** — Every line is actionable instruction
- **Degrees of freedom: HIGH** — Skill guides the process, not the content. Claude adapts to any doc type.

### Key Patterns
- **Section-by-section workflow**: Clarifying Questions → Brainstorming (5-20 options) → Curation (user picks) → Draft → Surgical Edits
- **Exit conditions per stage**: Stage 1 exits when "edge cases and trade-offs can be asked about without needing basics explained"
- **Artifact detection**: Checks for create_file capability, falls back to markdown file
- **Image alt-text awareness**: Checks for images without alt-text in existing docs (important for AI readability)
