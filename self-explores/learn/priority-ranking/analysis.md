# Xếp hạng Ưu tiên & Lộ trình học

**Persona:** AI/ML developer dùng Claude Code + OMC hàng ngày, xây skill/MCP servers.

## Weighted Scoring Matrix

**Tiêu chí + Trọng số:**
- Tích hợp OMC/Claude Code (30%)
- Tần suất dùng thực tế (30%)
- Độ sâu kiến thức (20%)
- Đòn bẩy scale/automate (20%)

| # | Skill | Tích hợp (30%) | Tần suất (30%) | Kiến thức (20%) | Đòn bẩy (20%) | **Weighted** | **Priority** | Rationale |
|---|-------|:-:|:-:|:-:|:-:|:-:|:-:|-----------|
| 1 | skill-creator | 5 | 4 | 5 | 5 | **4.7** | **5** | Foundational — hiểu skill anatomy = tạo mọi skill khác |
| 2 | mcp-builder | 5 | 4 | 5 | 5 | **4.7** | **5** | MCP servers là core extension point cho Claude Code |
| 3 | frontend-design | 4 | 5 | 4 | 4 | **4.3** | **5** | Anti-AI-slop principles áp dụng mọi UI output |
| 4 | pdf | 4 | 5 | 3 | 3 | **3.9** | **4** | Document processing phổ biến nhất |
| 5 | doc-coauthoring | 4 | 4 | 4 | 4 | **4.0** | **4** | 3-stage workflow áp dụng cho mọi documentation |
| 6 | docx | 3 | 4 | 4 | 3 | **3.5** | **4** | Word docs common, XML patterns reusable |
| 7 | pptx | 3 | 3 | 4 | 3 | **3.2** | **3** | Presentations less frequent but valuable |
| 8 | xlsx | 3 | 3 | 4 | 3 | **3.2** | **3** | Financial model patterns = niche but deep |
| 9 | webapp-testing | 5 | 3 | 3 | 4 | **3.8** | **4** | Playwright testing integrates with dev workflow |
| 10 | web-artifacts-builder | 4 | 3 | 3 | 3 | **3.3** | **3** | Claude.ai artifacts useful but narrow |
| 11 | algorithmic-art | 2 | 2 | 4 | 3 | **2.6** | **2** | Creative skill, less daily utility |
| 12 | canvas-design | 2 | 2 | 3 | 2 | **2.2** | **2** | Poster/art creation, niche |
| 13 | theme-factory | 3 | 3 | 2 | 3 | **2.8** | **3** | Quick theming, complementary to pptx/frontend |
| 14 | brand-guidelines | 2 | 2 | 2 | 2 | **2.0** | **2** | Anthropic-specific, narrow applicability |
| 15 | slack-gif-creator | 2 | 2 | 3 | 2 | **2.2** | **2** | Fun but low daily utility |
| 16 | internal-comms | 2 | 2 | 1 | 2 | **1.8** | **1** | Too thin, better to write custom templates |

---

## Learning Path — 3 Phases

### Phase 1: Foundation (Week 1-2) — 5 skills
**Mục tiêu:** Hiểu skill ecosystem + core development patterns

| Order | Skill | Why First | ~Time |
|-------|-------|-----------|-------|
| 1 | **skill-creator** | Meta-skill: hiểu anatomy = hiểu tất cả | 50 min |
| 2 | **frontend-design** | Anti-AI-slop principles, apply everywhere | 30 min |
| 3 | **mcp-builder** | Core extension point, Python+Node patterns | 55 min |
| 4 | **doc-coauthoring** | Methodology transferable to any writing | 35 min |
| 5 | **webapp-testing** | Playwright testing for dev workflow | 30 min |

**Kết quả Phase 1:** Có khả năng tạo skills mới, build MCP servers, viết docs structured, test web apps.

### Phase 2: Core (Week 3-4) — 5 skills
**Mục tiêu:** Master document processing + specialized output

| Order | Skill | Why Now | ~Time |
|-------|-------|---------|-------|
| 6 | **pdf** | Most common document format | 50 min |
| 7 | **docx** | Word docs, XML patterns deep | 55 min |
| 8 | **pptx** | Presentations, template handling | 45 min |
| 9 | **xlsx** | Financial models, data cleaning | 40 min |
| 10 | **web-artifacts-builder** | Claude.ai artifact creation | 35 min |

**Kết quả Phase 2:** Full document processing capability (PDF, Word, PowerPoint, Excel) + Claude.ai artifacts.

### Phase 3: Advanced (Week 5+) — 6 skills
**Mục tiêu:** Creative skills + specialized tools

| Order | Skill | Why Later | ~Time |
|-------|-------|-----------|-------|
| 11 | **theme-factory** | Complements pptx/frontend, plug-and-play | 25 min |
| 12 | **algorithmic-art** | Creative p5.js patterns, generative art | 35 min |
| 13 | **canvas-design** | Static visual art creation | 30 min |
| 14 | **slack-gif-creator** | Fun niche tool | 35 min |
| 15 | **brand-guidelines** | Anthropic-specific styling | 20 min |
| 16 | **internal-comms** | Template-based, least depth | 20 min |

**Kết quả Phase 3:** Full creative toolkit, brand awareness, communication templates.

---

## Key Recommendations

1. **Start with skill-creator** — nó dạy cách ĐỌC skills, không chỉ cách TẠO skills
2. **frontend-design principles > cụ thể** — 42 lines nhưng áp dụng được cho mọi UI work
3. **mcp-builder là highest ROI** cho developer — build 1 MCP server = extend Claude forever
4. **Document skills (pdf/docx/pptx/xlsx)** share infrastructure — learn 1, apply patterns to all
5. **Skip internal-comms** nếu thiếu thời gian — quá thin, tự viết template tốt hơn
