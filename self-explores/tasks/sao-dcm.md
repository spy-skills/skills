---
date: 2026-03-26
type: task-worklog
task: sao-dcm
title: "Xếp hạng Ưu tiên & Lộ trình học"
status: open
detailed_at: 2026-03-26
detail_score: ready-for-dev
tags: [research, priority, roadmap, skills]
---

# Xếp hạng Ưu tiên & Lộ trình học — Detailed Design

## 1. Objective
Chấm ưu tiên 1-5 cho 16 skills bằng weighted scoring matrix. Persona: AI/ML developer dùng Claude Code hàng ngày. Tạo learning path 3 phases.

## 2. Scope
**In-scope:**
- Weighted scoring: 4 tiêu chí với trọng số
- Learning path 3 phases: Foundation → Core → Advanced
- Gợi ý timeline

**Out-of-scope:**
- Deep dive từng skill
- So sánh cross-repo

## 3. Input / Output
**Input:**
- `self-explores/learn/overview/analysis.md` (kết quả sao-9b3)

**Output:**
- `self-explores/learn/priority-ranking/analysis.md` (>= 80 lines)
- Bảng ranking 16 skills sortable by priority
- Learning path 3 phases

## 4. Dependencies
- sao-9b3 (Tổng quan) phải xong trước

## 5. Flow xử lý

### Step 1: Đọc overview analysis (~5 phút)
Đọc `self-explores/learn/overview/analysis.md`
**Verify:** Hiểu scores + notes của 16 skills

### Step 2: Chấm weighted priority (~15 phút)
Matrix 4 tiêu chí:
- **Tích hợp OMC/Claude Code** (30%): Skill dùng được ngay trong workflow hàng ngày?
- **Tần suất dùng thực tế** (30%): Bao lâu gặp use case 1 lần?
- **Độ sâu kiến thức** (20%): Học được bao nhiêu patterns reusable?
- **Đòn bẩy** (20%): Có thể scale/automate/delegate không?

Chấm mỗi tiêu chí 1-5, weighted sum → final priority 1-5
**Verify:** 16 rows filled, no ties (break by Tần suất)

### Step 3: Tạo learning path (~10 phút)
- **Foundation** (Week 1-2): Skills cần biết trước
- **Core** (Week 3-4): Skills dùng hàng ngày
- **Advanced** (Week 5+): Skills chuyên sâu
**Verify:** Mỗi phase có >= 3 skills, tổng = 16

## 6. Edge Cases
| Case | Trigger | Expected | Recovery |
|------|---------|----------|----------|
| Tie scores | 2+ skills cùng điểm | Break by Tần suất → Tích hợp | Ghi note "tied with X" |
| Overview chưa xong | sao-9b3 chưa done | Task blocked | Chờ, không làm |

## 7. Acceptance Criteria
- **Happy 1:** Given overview data, When ranking complete, Then bảng 16 rows sortable, mỗi skill có rationale
- **Happy 2:** Given 16 skills, When learning path created, Then 3 phases, total = 16 skills
- **Negative:** Given tie, Then break clearly documented

## 8. Technical Notes
- Persona: AI/ML developer, dùng Claude Code + OMC hàng ngày, xây skill/MCP servers
- Trọng số tham khảo, có thể adjust sau khi chấm nếu kết quả counter-intuitive

## 9. Risks
- Subjective → mitigation: weighted formula transparent, rationale mỗi skill

## Worklog
*(Chưa bắt đầu)*
