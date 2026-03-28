---
date: 2026-03-26
type: task-worklog
task: sao-e6v
title: "Review & Notion — Tổng hợp kết quả"
status: open
detailed_at: 2026-03-26
detail_score: ready-for-dev
tags: [review, notion, summary, tracking]
---

# Review & Notion — Tổng hợp kết quả — Detailed Design

## 1. Objective
Tổng hợp 16 analysis.md files thành comparison matrix + summary. Đẩy kết quả lên Notion (Experiments > Skills). Fallback: local-only nếu MCP fail.

## 2. Scope
**In-scope:**
- Đọc 16 analysis files từ self-explores/learn/*/analysis.md
- Tạo comparison matrix (Skill | Score | Ưu | Nhược | Tích hợp | Priority)
- Tạo summary analysis.md
- Push to Notion (1 overview page + 16 skill pages)
- Push to Trello tracking cards

**Out-of-scope:**
- Re-analyze skills
- Modify existing analysis files

## 3. Input / Output
**Input:**
- 16 files: `self-explores/learn/*/analysis.md`
- 1 file: `self-explores/learn/priority-ranking/analysis.md`

**Output:**
- `self-explores/learn/summary/analysis.md` (>= 100 lines)
- Notion pages under Experiments > Skills > 01_skills-anthropic-official
- Trello tracking cards on active board

## 4. Dependencies
- ALL 16 deep dive tasks (sao-4pl, sao-758, ..., sao-h3m)
- sao-dcm (Xếp hạng Ưu tiên)

## 5. Flow xử lý

### Step 1: Thu thập kết quả (~10 phút)
Đọc tất cả 16 analysis.md files. Extract: score, ưu, nhược, tích hợp notes.
**Verify:** Data cho 16 skills collected

### Step 2: Tạo comparison matrix (~5 phút)
Bảng 16 rows, columns: Skill | Domain | Score | Priority | Top Ưu | Top Nhược | Tích hợp
Sort by Priority descending, then Score descending.
**Verify:** 16 rows, no nulls

### Step 3: Viết summary analysis.md (~10 phút)
Sections: Executive Summary, Comparison Matrix, Top 5 Recommended, Learning Path, Patterns Observed
**Verify:** >= 100 lines, matrix included

### Step 4: Push to Notion (~15 phút)
4a. Search for parent page: `mcp__notion__notion-search` with "Experiments" or "Skills"
4b. If found → create child pages. If not → create new page at root.
4c. Overview page: comparison matrix + summary
4d. Per-skill pages: full analysis.md content
**Verify:** Pages created or error logged

### Step 5: Push to Trello (~5 phút)
5a. Find/create "Tracking" list on active board
5b. Create 1 card per completed deep dive task
**Verify:** Cards created or error logged

### Step 6: FALLBACK if MCP fails (~2 phút)
If Notion/Trello MCP unavailable:
- Log warning: "Notion/Trello MCP unavailable — results saved locally only"
- Ensure summary/analysis.md is complete (local output)
- Create daily log entry with results

## 6. Edge Cases
| Case | Trigger | Expected | Recovery |
|------|---------|----------|----------|
| Missing analysis.md | Deep dive not done | Skip skill in matrix | Log "MISSING: {skill}" |
| Notion MCP fail | Auth/network error | Local-only output | summary/analysis.md sufficient |
| Trello MCP fail | Auth/board error | Skip Trello | Log warning, continue |
| Notion parent page not found | Search returns empty | Create at root level | Log "Created at root" |

## 7. Acceptance Criteria
- **Happy 1:** Given 16 analysis files, When summary written, Then summary/analysis.md >= 100 lines with comparison matrix
- **Happy 2:** Given Notion MCP available, When push complete, Then >= 1 overview page created
- **Negative:** Given MCP failure, Then local summary still written, error logged

## 8. Technical Notes
- Notion search: try keywords "Experiments", "Skills", "01_skills-anthropic-official"
- Trello: use active board, list name "Tracking"
- Each Notion page should include: beads task ID, absolute file path, summary

## 9. Risks
- MCP authentication expired → mitigation: fallback to local
- Notion page structure mismatch → mitigation: search first, create if not found
- Rate limiting on batch create → mitigation: sequential with 1s delay

## Worklog
*(Chưa bắt đầu)*
