# frontend-design

## Đánh giá (Score 8.5/10)

| Tiêu chi | Score | Rationale |
|-----------|-------|-----------|
| Completeness | 7 | Covers design thinking + aesthetics guidelines in 42 lines. No reference files, no code examples, no framework-specific patterns. Relies entirely on Claude's latent knowledge for implementation. Intentionally minimal -- the brevity IS the design. |
| Usability | 9 | Immediately actionable. Every sentence is a directive, not filler. Two clear sections (Design Thinking + Aesthetics Guidelines) create a simple mental model: think first, then execute with these rules. Zero onboarding friction. |
| Modularity | 8 | Self-contained single file, no external dependencies. Works with any frontend framework (HTML/CSS/JS, React, Vue). No reference files means no loading complexity. Downside: cannot swap or extend aesthetic rulesets without editing the core file. |
| Safety | 10 | The entire skill IS a safety mechanism -- it guards against the #1 risk in AI-generated frontends: generic, soulless output. The anti-AI-slop rules (banned fonts, banned color schemes, banned layout patterns) are explicit safety rails for design quality. |

**Trung binh: 8.5/10**

## Uu diem

1. **Anti-AI-slop blacklist is precise and actionable** -- Lines 36-38 explicitly ban Inter, Roboto, Arial, system fonts; purple gradients on white; cookie-cutter layouts. This is not vague "be creative" advice. It is a concrete exclusion list that forces Claude away from the statistical mode of AI-generated design. Most skills tell you what TO do; this one also tells you what NEVER to do, which is far more effective at preventing mediocrity.

2. **Extreme density: 42 lines encode a complete design philosophy** -- Compare with mcp-builder (~2500 lines across 4 reference files) or skill-creator (~1800 lines). This skill achieves comparable behavioral impact in 2% of the token budget. Every line carries weight. The "Design Thinking" section (lines 11-18) is a full creative brief framework. The "Aesthetics Guidelines" section (lines 27-35) covers typography, color, motion, spatial composition, and backgrounds -- five pillars in five bullet points. This is masterclass-level prompt engineering: maximum behavioral shift per token.

3. **Tone diversity enforcement prevents convergence** -- Line 15 lists 12+ aesthetic directions (brutally minimal, maximalist chaos, retro-futuristic, organic/natural, luxury/refined, playful/toy-like, editorial/magazine, brutalist/raw, art deco/geometric, soft/pastel, industrial/utilitarian). Line 38 explicitly warns against converging on popular choices ("Space Grotesk, for example"). This addresses the fundamental LLM failure mode: regression to the mean across generations.

4. **"Match implementation complexity to aesthetic vision" (line 40)** -- This single sentence prevents two common failures: (a) over-engineering minimalist designs with unnecessary animations, and (b) under-delivering on maximalist visions with sparse code. It links code volume to creative intent, which is a nuance most design guidelines miss entirely.

5. **The closing line is functional, not motivational** -- "Claude is capable of extraordinary creative work" (line 42) is not cheerleading. In the context of a system prompt, this sentence recalibrates the model's self-imposed constraints. LLMs tend to play it safe by default; this explicit permission to push boundaries has measurable impact on output quality.

## Nhuoc diem

1. **No reference files or code examples** -- Unlike pdf (4 reference files), mcp-builder (4 reference files), or skill-creator (3 reference files), frontend-design ships zero supplementary material. This means Claude must generate all CSS patterns, animation code, font pairing logic, and color theory from its training data. For common frameworks (React + Tailwind), this works well. For edge cases (complex SVG animations, WebGL backgrounds, CSS Houdini), the lack of reference patterns may result in hallucinated or outdated API usage. A single reference file with 10-15 curated code snippets (noise textures, gradient meshes, staggered reveal animations, asymmetric grid layouts) would significantly boost output reliability.

2. **No accessibility guardrails** -- Line 16 mentions accessibility as a "constraint" to consider, but provides zero concrete guidance. Color contrast ratios, focus indicators, screen reader compatibility, reduced-motion preferences, semantic HTML -- none are addressed. This is a significant gap because the skill actively encourages bold color choices, unusual layouts, and heavy animations, all of which can create accessibility failures. A 3-line "Accessibility Minimum" section (WCAG AA contrast, prefers-reduced-motion, semantic landmarks) would cost almost nothing in token budget but prevent real harm.

3. **No responsive design or performance guidance** -- The skill focuses entirely on visual aesthetics with no mention of mobile viewports, loading performance, or bundle size. A design that is "visually striking and memorable" on a 27" monitor may be unusable on a phone. Similarly, "elaborate code with extensive animations" (line 40) can destroy Core Web Vitals. Two sentences on responsive adaptation and performance budgets would close this gap.

## Kha nang tich hop vao he thong hien tai

**High integration value for OMC workflows:**

1. **Direct use in autopilot/ralph modes** -- When autopilot or ralph receives a frontend task, this skill provides the creative direction layer that prevents generic output. The Design Thinking framework (Purpose, Tone, Constraints, Differentiation) maps naturally to the explore -> plan -> execute pipeline.

2. **Complements theme-factory and web-artifacts-builder** -- theme-factory provides 10 pre-set themes; frontend-design provides the philosophy for creating NEW themes that break conventions. web-artifacts-builder handles React/Tailwind/shadcn infrastructure; frontend-design handles the aesthetic layer on top. These three skills form a complete frontend stack: infrastructure (web-artifacts-builder) + presets (theme-factory) + creative direction (frontend-design).

3. **Anti-convergence rules improve multi-generation workflows** -- In team or ultrawork modes where multiple agents generate frontend components in parallel, the anti-convergence rules (line 38: "No design should be the same. Vary between light and dark themes, different fonts, different aesthetics") prevent the common failure where parallel agents all produce suspiciously similar output.

4. **Lightweight token footprint** -- At 42 lines, this skill can be loaded into any agent context without meaningful token cost. It can ride along as ambient guidance in any workflow that might produce frontend output, unlike heavier skills that must be loaded selectively.

## Ghi chu ky thuat (Technical Decisions)

### Design Principle: Opinionated Exclusion Over Open Guidance

The skill's most powerful technique is the NEVER list (line 36). Rather than trying to enumerate all good design (impossible), it identifies the specific failure mode of AI-generated design (convergence on Inter/Roboto, purple gradients, centered layouts) and bans it explicitly. This is a form of negative prompting -- constraining the output space by removing the highest-probability but lowest-quality region. It exploits the fact that LLMs default to statistically common patterns, so banning those patterns forces exploration of the long tail where genuinely creative output lives.

### Anti-AI-Slop Patterns (The Core Innovation)

The skill identifies and addresses the "AI aesthetic" problem at multiple levels:

- **Font level**: Ban Inter, Roboto, Arial, system fonts. Force distinctive typography choices.
- **Color level**: Ban purple gradients on white. Force cohesive palettes with "dominant colors + sharp accents."
- **Layout level**: Ban "predictable layouts and component patterns." Encourage asymmetry, overlap, diagonal flow, grid-breaking.
- **Cross-generation level**: Ban convergence on popular alternatives ("Space Grotesk, for example"). Force variety between generations.
- **Meta level**: Ban "cookie-cutter design that lacks context-specific character." Every design must be unique to its context.

### Typography Strategy: Display + Body Pairing

Line 30 prescribes a specific typographic architecture: "Pair a distinctive display font with a refined body font." This two-tier system creates visual hierarchy while allowing creative expression in headlines without sacrificing readability in body text. The instruction to use "unexpected, characterful font choices" pushes toward Google Fonts long-tail (e.g., Playfair Display, Syne, Cabinet Grotesk, Instrument Serif) rather than the top-10 defaults.

### Motion Hierarchy: Orchestrated Entrances Over Scattered Micro-interactions

Line 32 makes a specific architectural choice: "one well-orchestrated page load with staggered reveals (animation-delay) creates more delight than scattered micro-interactions." This prioritizes choreographed entrance sequences over distributed hover effects. It also prescribes CSS-only solutions for HTML and Motion library for React, establishing a clear technology decision tree.

### Spatial Composition: Controlled Rule-Breaking

Line 33 lists specific spatial techniques: asymmetry, overlap, diagonal flow, grid-breaking elements. Then it adds the crucial qualifier: "Generous negative space OR controlled density." The OR is important -- it acknowledges that both sparse and dense layouts can be excellent, preventing a one-size-fits-all spatial rule. This maps to the overarching principle on line 19: "Bold maximalism and refined minimalism both work -- the key is intentionality, not intensity."

### The 42-Line Constraint as a Feature

The extreme brevity is itself a design decision. A longer skill with detailed code examples would anchor Claude to specific patterns, potentially creating a new form of convergence. By staying at the philosophy level, the skill leaves implementation space open for Claude's creative inference. The tradeoff: higher variance in output quality, but also higher ceiling for exceptional output. This is the right tradeoff for a design skill where uniqueness matters more than consistency.
