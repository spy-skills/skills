---
date: 2026-03-26
type: task-worklog
task: sao-fj0
title: "Deep Dive: webapp-testing"
status: open
detailed_at: 2026-03-26
detail_score: ready-for-dev
tags: [deep-dive, webapp-testing, research]
---

# Deep Dive: webapp-testing — Detailed Design

## 1. Objective
Nghiên cứu skill `webapp-testing` (SKILL.md: 95 lines). Phân tích core logic, đánh giá chất lượng, viết analysis theo format chuẩn.

## 2. Scope
**In-scope:**
- Đọc SKILL.md + bundled resources
- Phân tích patterns, architecture, design decisions
- Đánh giá 4 tiêu chí (Completeness, Usability, Modularity, Safety) thang 1-10
- Viết analysis.md theo format chuẩn

**Out-of-scope:**
- Chạy thử skill
- So sánh cross-repo
- Sửa code skill

## 3. Input / Output
**Input:**
- `skills/webapp-testing/SKILL.md` (95 lines)
- Extra files: scripts/with_server.py (105L), examples/ (105L)

**Output:**
- `self-explores/learn/webapp-testing/analysis.md` (>= 40 lines)

## 4. Dependencies
- Không (ready ngay)

## 5. Flow xử lý

### Step 1: Đọc SKILL.md đầy đủ (~7 phút)
Dùng Read tool: `skills/webapp-testing/SKILL.md`
Ghi notes: structure, key patterns, design decisions
**Verify:** Có notes về mục đích, trigger conditions, core workflow

### Step 2: Đọc bundled resources (~7 phút)
scripts/with_server.py (105L), examples/ (105L)
Focus: patterns bổ sung cho SKILL.md chính
**Verify:** Hiểu resource nào critical vs optional

### Step 3: Phân tích theo 4 góc nhìn (~10 phút)
Focus areas: Playwright automation patterns, screenshot capture, browser console logging, server lifecycle management (with_server.py), static vs dynamic webapp testing
Chấm 4 tiêu chí: Completeness, Usability, Modularity, Safety (1-10 mỗi cái)
**Verify:** 4 scores với rationale

### Step 4: Viết analysis.md (~7 phút)
Format chuẩn:
```
# webapp-testing
## Đánh giá (Score X/10) — trung bình 4 tiêu chí
## Ưu & Nhược điểm (>= 3 ưu, >= 2 nhược)
## Khả năng tích hợp vào hệ thống hiện tại
## Ghi chú kỹ thuật (Technical Decisions)
```
**Verify:** File >= 40 lines, đúng format

## 6. Edge Cases
| Case | Trigger | Expected | Recovery |
|------|---------|----------|----------|
| File quá lớn | Extra files > 1000L | Đọc lướt, focus key sections | Ghi "partial read" |
| Skill quá đơn giản | < 50 lines, no extras | Shorter analysis OK | Min 20 lines |

## 7. Acceptance Criteria
- **Happy 1:** Given skill files, When analysis complete, Then analysis.md >= 40 lines, đúng format 4 sections
- **Happy 2:** Given 4 criteria, When scoring, Then each has score 1-10 + rationale 1 sentence
- **Negative:** Given missing file, Then log warning, continue with available files

## 8. Technical Notes
- Skill type: P2 priority
- SKILL.md: 95 lines
- Extra resources: scripts/with_server.py (105L), examples/ (105L)
- Focus: Playwright automation patterns, screenshot capture, browser console logging, server lifecycle management (with_server.py), static vs dynamic webapp testing

## 9. Risks
- Đọc superficial vì ép thời gian → mitigation: focus vào SKILL.md + key references only
- Subjective scoring → mitigation: rubric từ sao-9b3

## Worklog
*(Chưa bắt đầu)*
