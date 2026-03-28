# internal-comms

## Đánh giá (Score 6.0/10)

| Tiêu chí | Score | Rationale |
|-----------|-------|-----------|
| Completeness | 4 | Only 32 lines — dispatches to 4 example files. No inline guidance, no formatting rules, no tone guidelines. |
| Usability | 7 | Simple: identify type → load example → follow instructions. Low barrier. |
| Modularity | 6 | Depends entirely on example files. SKILL.md alone is near-useless. |
| Safety | 7 | Template-based approach reduces tone/content errors. |

**Trung bình: 6.0/10**

## Ưu điểm

1. **Lowest barrier to entry** — 32 lines. Identify communication type → load appropriate example file → follow specific instructions. Anyone can use immediately.

2. **4 communication types covered** — 3P updates, company newsletters, FAQ answers, general comms. Covers most internal communication needs.

3. **Dispatcher pattern** — SKILL.md acts as router: match type → load file. Keeps each template independent and focused.

## Nhược điểm

1. **Thinnest skill in the repo** — 32 lines is barely a skill. No formatting guidance, no tone rules, no audience adaptation, no examples in SKILL.md itself. All substance lives in example files.

2. **No fallback for unknown types** — "If the communication type doesn't match any existing guideline, ask for clarification" — but doesn't help create new template types. Dead end.

3. **Company-specific templates** — Example files are for ONE company's format. Not generalizable without significant customization.

## Khả năng tích hợp
- Dispatcher pattern (route by type → load template) applicable to any template-based skill
- 3P update format potentially useful for team status reporting

## Ghi chú kỹ thuật
- 32L SKILL.md, 4 example files in examples/
- Types: 3p-updates.md, company-newsletter.md, faq-answers.md, general-comms.md
- Pure dispatcher: no logic in SKILL.md, all content in examples/
