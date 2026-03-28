---
date: 2026-03-26
type: task-worklog
task: sao-cul
title: "Deep Dive: theme-factory"
status: open
detailed_at: 2026-03-26
detail_score: ready-for-dev
tags: [deep-dive, theme-factory, research]
---

# Deep Dive: theme-factory — Detailed Design

## 1. Objective
Nghiên cứu skill `theme-factory` (SKILL.md: 59 lines). Phân tích core logic, đánh giá chất lượng, viết analysis theo format chuẩn.

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
- `skills/theme-factory/SKILL.md` (59 lines)
- Extra files: themes/ (10 theme files x 19L each), theme-showcase.pdf

**Output:**
- `self-explores/learn/theme-factory/analysis.md` (>= 30 lines)

## 4. Dependencies
- Không (ready ngay)

## 5. Flow xử lý

### Step 1: Đọc SKILL.md đầy đủ (~6 phút)
Dùng Read tool: `skills/theme-factory/SKILL.md`
Ghi notes: structure, key patterns, design decisions
**Verify:** Có notes về mục đích, trigger conditions, core workflow

### Step 2: Đọc bundled resources (~6 phút)
themes/ (10 theme files x 19L each), theme-showcase.pdf
Focus: patterns bổ sung cho SKILL.md chính
**Verify:** Hiểu resource nào critical vs optional

### Step 3: Phân tích theo 4 góc nhìn (~8 phút)
Focus areas: 10 pre-set themes catalog, color/font specs per theme, on-the-fly theme generation, theme application to different artifact types
Chấm 4 tiêu chí: Completeness, Usability, Modularity, Safety (1-10 mỗi cái)
**Verify:** 4 scores với rationale

### Step 4: Viết analysis.md (~6 phút)
Format chuẩn:
```
# theme-factory
## Đánh giá (Score X/10) — trung bình 4 tiêu chí
## Ưu & Nhược điểm (>= 3 ưu, >= 2 nhược)
## Khả năng tích hợp vào hệ thống hiện tại
## Ghi chú kỹ thuật (Technical Decisions)
```
**Verify:** File >= 30 lines, đúng format

## 6. Edge Cases
| Case | Trigger | Expected | Recovery |
|------|---------|----------|----------|
| File quá lớn | Extra files > 1000L | Đọc lướt, focus key sections | Ghi "partial read" |
| Skill quá đơn giản | < 50 lines, no extras | Shorter analysis OK | Min 20 lines |

## 7. Acceptance Criteria
- **Happy 1:** Given skill files, When analysis complete, Then analysis.md >= 30 lines, đúng format 4 sections
- **Happy 2:** Given 4 criteria, When scoring, Then each has score 1-10 + rationale 1 sentence
- **Negative:** Given missing file, Then log warning, continue with available files

## 8. Technical Notes
- Skill type: P3 priority
- SKILL.md: 59 lines
- Extra resources: themes/ (10 theme files x 19L each), theme-showcase.pdf
- Focus: 10 pre-set themes catalog, color/font specs per theme, on-the-fly theme generation, theme application to different artifact types

## 9. Risks
- Đọc superficial vì ép thời gian → mitigation: focus vào SKILL.md + key references only
- Subjective scoring → mitigation: rubric từ sao-9b3

## Worklog
*(Chưa bắt đầu)*
