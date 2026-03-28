# webapp-testing

## Đánh giá (Score 7.0/10)

| Tiêu chí | Score | Rationale |
|-----------|-------|-----------|
| Completeness | 6 | Covers Playwright basics, decision tree, server management. Missing: assertion patterns, CI integration. |
| Usability | 8 | Decision tree at top immediately routes user to correct approach. "Run --help first" philosophy. |
| Modularity | 7 | with_server.py reusable for any web testing. Playwright patterns transferable. |
| Safety | 7 | "DO NOT read source until absolutely necessary" — prevents context window pollution from large scripts. |

**Trung bình: 7.0/10**

## Ưu điểm

1. **Decision tree routing** — Static HTML? → read selectors → Playwright. Dynamic + no server? → with_server.py. Dynamic + server running? → Recon-then-action. Instant routing eliminates guesswork.

2. **"Run --help first, don't read source"** — Black-box script philosophy: scripts exist to be CALLED, not INGESTED. Prevents 100+ line scripts from polluting context window.

3. **Multi-server support** — with_server.py handles multiple servers (backend + frontend) with port specification. Covers real-world dev setups.

## Nhược điểm

1. **No assertion patterns** — Shows navigation and screenshot but no expect/assert patterns. Missing: how to verify element text, check visibility, validate state changes.

2. **Typo: "abslutely"** — Line 14 has "abslutely necessary" — minor but shows less polish than other skills.

## Khả năng tích hợp
- Playwright patterns directly applicable to QA workflows in any web project
- with_server.py pattern reusable for integration testing

## Ghi chú kỹ thuật
- 95L SKILL.md, 6 files total
- Playwright native Python scripts (not pytest-playwright)
- with_server.py manages server lifecycle including graceful shutdown
