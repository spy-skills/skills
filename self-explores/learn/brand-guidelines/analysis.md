# brand-guidelines

## Đánh giá (Score 7.5/10)

| Tiêu chí | Score | Rationale |
|-----------|-------|-----------|
| Completeness | 6 | Colors + typography + application rules. Missing: spacing, iconography, voice/tone, logo usage. |
| Usability | 9 | Plug-and-play: hex codes ready, font fallbacks specified, application rules clear. |
| Modularity | 7 | Anthropic-specific but color/font application PATTERN reusable for any brand. |
| Safety | 8 | Official brand identity. Auto-fallback to Arial/Georgia if custom fonts unavailable. |

**Trung bình: 7.5/10**

## Ưu điểm

1. **Instant brand application** — 7 hex codes + 2 font families = complete visual identity. Copy-paste ready: Dark #141413, Light #faf9f5, Orange #d97757, Blue #6a9bcc, Green #788c5d.

2. **Smart font fallback** — Poppins (headings) → Arial fallback. Lora (body) → Georgia fallback. Works on any system without font installation.

3. **Accent color cycling** — Non-text shapes cycle through orange → blue → green. Maintains visual interest automatically.

## Nhược điểm

1. **Incomplete brand guide** — No logo usage rules, no spacing/padding guidelines, no voice/tone, no iconography. Only covers colors + fonts.

2. **Anthropic-only** — Hardcoded to Anthropic brand. Pattern is reusable but content is not.

## Khả năng tích hợp
- Brand application pattern reusable: hex codes + font stack + fallback + accent cycling
- Directly usable when creating Anthropic-branded content

## Ghi chú kỹ thuật
- 73L SKILL.md, no extra files
- Colors: 4 main (dark, light, mid-gray, light-gray) + 3 accents (orange, blue, green)
- Fonts: Poppins (headings 24pt+), Lora (body text)
- Applied via python-pptx RGBColor class
