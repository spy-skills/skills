# Phân tích Tổng quan 16 Skills Anthropic Official

## Summary Table

| # | Skill | Domain | Lines | Files | Comp | Usab | Modul | Safe | AVG | Notes |
|---|-------|--------|-------|-------|------|------|-------|------|-----|-------|
| 1 | skill-creator | Dev | 357 | 7 | 9 | 9 | 9 | 9 | **9.0** | Meta-skill, teaches skill creation |
| 2 | pdf | Doc | 314 | 12 | 9 | 8 | 8 | 7 | **8.0** | 3 libs (pypdf/pdfplumber/reportlab), OCR, forms |
| 3 | mcp-builder | Dev | 236 | 10 | 9 | 8 | 8 | 8 | **8.3** | Python FastMCP + Node MCP SDK, 4 ref docs |
| 4 | docx | Doc | 481 | 61 | 9 | 7 | 8 | 8 | **8.0** | XML-based, tracked changes, 23K+ lines scripts |
| 5 | doc-coauthoring | Dev | 375 | 1 | 8 | 9 | 7 | 8 | **8.0** | 3-stage workflow, pure methodology |
| 6 | pptx | Doc | 232 | 59 | 8 | 8 | 8 | 7 | **7.8** | python-pptx + pptxgenjs, template editing |
| 7 | algorithmic-art | Design | 404 | 4 | 8 | 7 | 7 | 8 | **7.5** | p5.js generative art, seeded randomness |
| 8 | frontend-design | Design | 42 | 2 | 7 | 8 | 9 | 8 | **8.0** | Anti-AI-slop manifesto, universal |
| 9 | xlsx | Doc | 291 | 54 | 8 | 7 | 7 | 8 | **7.5** | Financial model standards, color coding |
| 10 | slack-gif-creator | Spec | 254 | 7 | 8 | 8 | 7 | 7 | **7.5** | GIFBuilder + validators + easing |
| 11 | webapp-testing | Dev | 95 | 6 | 6 | 8 | 7 | 7 | **7.0** | Playwright, decision tree, with_server.py |
| 12 | canvas-design | Design | 129 | 83 | 7 | 7 | 6 | 8 | **7.0** | Philosophy → visual expression, fonts |
| 13 | web-artifacts-builder | Spec | 73 | 5 | 7 | 8 | 6 | 7 | **7.0** | React+shadcn for Claude.ai artifacts |
| 14 | theme-factory | Design | 59 | 13 | 7 | 9 | 8 | 7 | **7.8** | 10 pre-set themes, plug-and-play |
| 15 | brand-guidelines | Design | 73 | 2 | 6 | 9 | 7 | 8 | **7.5** | Anthropic brand colors + typography |
| 16 | internal-comms | Doc | 32 | 6 | 4 | 7 | 6 | 7 | **6.0** | Thin dispatcher to example templates |

**Rubric:** Completeness (edge cases bao quát) | Usability (dễ dùng cho người mới) | Modularity (tách rời/tái sử dụng) | Safety (Anthropic prompt eng guidelines) — Scale 1-10

---

## Phân nhóm theo Domain

### 1. Document & Enterprise (5 skills)
**docx** | **pdf** | **pptx** | **xlsx** | **internal-comms**

Nhóm này chiếm nhiều code nhất (61+12+59+54+6 = 192 files). Đặc điểm chung:
- Xử lý file formats phức tạp (XML-based Office docs, PDF binary)
- Bundled scripts mạnh: validators, converters, Office XML schemas
- Production-grade: đây là skills được dùng thực tế trong Claude production
- **docx/pptx/xlsx** share cùng Office XML infrastructure (`scripts/office/`)

**Điểm mạnh:** Comprehensive, battle-tested, bundled tools
**Điểm yếu:** Nặng context (docx 481L + 23K scripts), learning curve cao

### 2. Development & Technical (4 skills)
**skill-creator** | **mcp-builder** | **webapp-testing** | **doc-coauthoring**

Nhóm này dạy CÁCH LÀM hơn là làm trực tiếp. Đặc điểm:
- **skill-creator** là meta-skill quan trọng nhất — hiểu nó = hiểu tất cả skills
- **mcp-builder** có 4 reference docs comprehensive (Python + Node + best practices + evaluation)
- **doc-coauthoring** là pure methodology — 3-stage workflow không cần code
- **webapp-testing** nhỏ nhưng effective với decision tree approach

**Điểm mạnh:** High leverage — knowledge transferable across projects
**Điểm yếu:** webapp-testing khá thin (95L)

### 3. Design & Creative (5 skills)
**frontend-design** | **canvas-design** | **algorithmic-art** | **theme-factory** | **brand-guidelines**

Nhóm này focus vào visual output quality. Pattern chung:
- **Anti-AI-slop philosophy** xuyên suốt: tránh generic aesthetics, bold choices
- **Philosophy → Expression** 2-step workflow (canvas-design, algorithmic-art)
- **frontend-design** ngắn nhất (42L) nhưng dense — mỗi câu đều actionable
- **theme-factory** plug-and-play: 10 themes sẵn, chỉ cần chọn

**Điểm mạnh:** Design quality principles applicable everywhere
**Điểm yếu:** canvas-design phụ thuộc font assets (83 files)

### 4. Specialized (2 skills)
**slack-gif-creator** | **web-artifacts-builder**

Hai skills cho use cases cụ thể:
- **slack-gif-creator**: GIFBuilder API clear, constraints well-defined (128x128, 10-30 FPS)
- **web-artifacts-builder**: React + shadcn/ui → single HTML artifact for Claude.ai

**Điểm mạnh:** Niche nhưng well-engineered cho mục đích cụ thể
**Điểm yếu:** Hẹp scope, khó reuse ngoài context ban đầu

---

## Patterns chung quan sát được

### 1. Progressive Disclosure Loading
Tất cả skills follow 3-tier loading:
- **Tier 1:** Frontmatter name + description (~100 words) — always loaded
- **Tier 2:** SKILL.md body — when skill triggers
- **Tier 3:** Bundled resources (scripts, references) — on demand

Skill-creator dạy pattern này explicitly. Đây là core principle.

### 2. "Context Window is a Public Good"
Skill-creator nói rõ: mỗi token trong SKILL.md phải justify giá trị. Skills tốt nhất (frontend-design 42L, brand-guidelines 73L) cực kỳ dense — mỗi câu đều actionable.

### 3. Degrees of Freedom
- **High freedom:** frontend-design, canvas-design, algorithmic-art — give principles, not recipes
- **Medium freedom:** doc-coauthoring, mcp-builder — structured workflow, room for adaptation
- **Low freedom:** docx, pdf, xlsx — specific scripts, exact commands, validation required

### 4. Anti-AI-Slop as Core Value
frontend-design, web-artifacts-builder, pptx all explicitly call out "AI slop" patterns to avoid:
- No Inter/Roboto/Arial fonts
- No purple gradients on white
- No centered cookie-cutter layouts
- Emphasize BOLD, INTENTIONAL, DISTINCTIVE design

### 5. Bundled Scripts vs Pure Knowledge
- **Script-heavy:** docx (61 files), pptx (59), xlsx (54) — complex file format manipulation
- **Knowledge-heavy:** frontend-design (42L, no scripts), doc-coauthoring (375L, no scripts)
- **Balanced:** mcp-builder (236L + 4 reference docs), slack-gif-creator (254L + 4 core modules)

---

## Top 5 Skills by Quality Score

1. **skill-creator** (9.0/10) — Foundational meta-skill, learn this first
2. **mcp-builder** (8.3/10) — Comprehensive MCP server development guide
3. **pdf** (8.0/10) — Best document skill, clean library coverage
4. **docx** (8.0/10) — Most comprehensive, heaviest bundled resources
5. **frontend-design** (8.0/10) — Shortest but most impactful design skill

## Bottom 3 by Quality Score

16. **internal-comms** (6.0/10) — Too thin, just a dispatcher
15. **webapp-testing** (7.0/10) — Useful but limited scope
14. **canvas-design** (7.0/10) — Font dependency, narrow use case
