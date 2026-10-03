# EXPLAINABILITY.md

This document explains the internal mechanisms, data lineage, operational boundaries, and governance framework of **OpenSlide** (`open-slide`) in accordance with the **OpenGAP v0.1.0** specification for the **HiDevs GitAgent Passport** clearance pipeline.

> **Agent Name:** OpenSlide (`open-slide`)  
> **Specification:** OpenGAP v0.1.0  
> **Category / Domain:** Developer Tools / Slide Engineering, Interactive Presentations & AI Deck Generation  
> **Compliance Standard:** OpenGAP Checkpoint 2 (Explainability & Decision Governance), OWASP LLM Top 10, MITRE ATLAS  

---

## How the Agent Decides

OpenSlide operates an intelligent, component-driven presentation compilation and layout routing architecture designed to transform technical specifications into interactive web slides. The agent manages narrative outlines, component typography, asset optimization, and live presenter telemetry through a deterministic five-stage operational pipeline.

### 1. Decision Architecture

The runtime intake, state classification, evaluation, and execution tracking operate across a deterministic, five-stage pipeline:

```
[ User Presentation Brief / Markdown Deck Outline ]
                       │
                       ▼
[Stage 1: Intent Ingestion & Theme Resolution Gate]
  - Parses outline headers, slide counts, and target audience tier
  - Evaluates color palette tokens and aspect ratio specifications (16:9 / 4:3)
  - Dispatches layout constraints to component scaffolding engine
                       ▼
[Stage 2: Semantic Layout & Component Binding Gate]
  - Maps content blocks to interactive React component templates
  - Evaluates code syntax highlighting requirements and diagrams
  - Computes typography scale and whitespace distribution metrics
                       ▼
[Stage 3: Design Rule & Accessibility Verification Gate]
  - Evaluates contrast ratio C_contrast against WCAG AA standards
  - Enforces text overflow boundaries and maximum line length rules
  - Computes composite slide visual balance score S_slide
                       ▼
[Stage 4: Vite HMR Compilation & Render Pass-Through Gate]
  - Triggers incremental module compilation via Vite dev server
  - Mounts slide components inside isolated DOM container
  - Captures rendering telemetry, layout shifts, and asset load times
                       ▼
[Stage 5: Presenter Mode Synchronization & Export Sealing Gate]
  - Synchronizes speaker notes across dual-window BroadcastChannels
  - Compiles final presentation into immutable static SPA bundle
  - Seals build artifact and records execution audit metadata
                       ▼
[ Final Verified OpenSlide Presentation Deck Ready ]
```

### 2. Decision Logic & Routing Formulations

When synthesizing slide component layouts and structuring presentation pacing, OpenSlide evaluates two deterministic mathematical formulations:

1. **Composite Slide Visual Balance Score ($S_{	ext{slide}}$)**:
   $$S_{	ext{slide}} = w_c \cdot C_{	ext{contrast}} + w_d \cdot (1 - D_{	ext{overflow}}) + w_r \cdot R_{	ext{ratio}} + w_p \cdot P_{	ext{pacing}}$$
   Where:
   - $C_{	ext{contrast}} \in [0, 1]$: Normalized text-to-background contrast score relative to WCAG AA ($4.5:1$ threshold).
   - $D_{	ext{overflow}} \in [0, 1]$: Geometric bounding box overflow penalty across viewport boundaries.
   - $R_{	ext{ratio}} \in [0, 1]$: Aspect ratio fidelity score enforcing strict $16:9$ viewport scaling.
   - $P_{	ext{pacing}} \in [0, 1]$: Slide narrative density metric evaluating word count versus recommended speaking duration ($120$ words/slide maximum).
   - Standard weightings: $w_c = 0.35$, $w_d = 0.30$, $w_r = 0.20$, $w_p = 0.15$ ($\sum w_i = 1.0$).
   - Layout approval threshold: A slide layout is cleared for compilation only if $S_{	ext{slide}} \ge 	au_{	ext{balance}} = 0.70$.

2. **Deck Layout Density Index ($I_{	ext{density}}$)**:
   $$I_{	ext{density}} = rac{1}{N} \sum_{i=1}^{N} \left( lpha \cdot rac{T_i}{T_{	ext{max}}} + eta \cdot rac{A_i}{A_{	ext{max}}} ight)$$
   Where:
   - $N$: Total number of slides in the active presentation deck.
   - $T_i$: Token and word count of slide $i$ relative to maximum readability ceiling $T_{	ext{max}} = 150$.
   - $A_i$: Number of visual components (charts, code blocks, images) on slide $i$ ($A_{	ext{max}} = 4$).
   - Coefficients: $lpha = 0.60$, $eta = 0.40$. Decks with $I_{	ext{density}} > 0.85$ trigger automatic layout pruning.

### 3. Thresholding & Refusal Decision Criteria

OpenSlide enforces strict operational boundaries and deterministic refusal thresholds:
- **Refusal on ERR_WCAG_CONTRAST_VIOLATION**: Slide text failing minimum contrast threshold ($C_{	ext{contrast}} < 4.5:1$) halts compilation with code `ERR_WCAG_CONTRAST_VIOLATION`.
- **Refusal on ERR_LAYOUT_OVERFLOW_DETECTED**: Component content exceeding viewport bounding boundaries halts compilation with code `ERR_LAYOUT_OVERFLOW_DETECTED`.
- **Refusal on ERR_UNAUTHORIZED_EXTERNAL_IMPORT**: Slide code importing unwhitelisted third-party external CDN scripts halts execution with code `ERR_UNAUTHORIZED_EXTERNAL_IMPORT`.
- **Refusal on ERR_BUILD_COMPILATION_FAILED**: TypeScript syntax or Vite build errors halting deck compilation terminate with code `ERR_BUILD_COMPILATION_FAILED`.
- **Refusal on ERR_TOKEN_BUDGET_EXCEEDED**: Deck specifications exceeding turn budget allocations ($T_{	ext{deck}} > 50,000$ tokens) halt with code `ERR_TOKEN_BUDGET_EXCEEDED`.

### 4. Fallback Decision Mechanism

Continuous operational stability is maintained through layered fault recovery:
- **Fallback Layout Degradation**: If complex grid or interactive canvas components fail to render within $200$ms, OpenSlide falls back to a clean semantic bullet layout.
- **Static Asset Bundling Fallback**: If external web fonts or CDN icons fail to resolve, local system typography stacks (`Inter`, `system-ui`) are seamlessly applied.
- **Model Fallback Cascade**: High-level reasoning and synthesis default to `gemini-2.0-flash` with automatic failover to `gpt-4o` and `claude-3-5-sonnet`.

### 5. Human-in-the-Loop Governance

Human operators retain sovereign authority over the multi-agent execution lifecycle:
- **Interactive Component Approval**: Deploying custom user-authored JavaScript widgets requires explicit operator confirmation before packaging.
- **Production Export Sign-Off**: Publishing compiled slide decks to public hosting domains or company CDNs mandates explicit administrator approval.
- **Presenter Timing Auditing**: Operators can inspect deck performance timelines, slide duration analytics, and contrast audit reports.

---

## The Data It Uses

OpenSlide operates under strict principles of data minimization, environment isolation, and privacy protection.

### 1. Ingested Input Data

The framework processes only operational data necessary to perform its functions:
- **Presentation Outline Briefs**: User prompt directives, markdown topic lists, and technical documentation extracts.
- **Component Code Snippets**: Sample code blocks, SQL queries, and syntax definitions for code presentation slides.
- **Visual Asset References**: Local SVG icons, PNG diagrams, and presentation theme configuration JSON files.

### 2. Configuration & Reference Data

- **Design System Manifests**: Theme color palettes, responsive font scales, and layout spacing tokens.
- **Component Registry**: Whitelisted `@open-slide/core` UI primitives, syntax highlighter definitions, and layout templates.
- **Presenter Metadata**: Speaker notes, countdown duration limits, and slide transition timing profiles.

### 3. Base Model & Inference Lineage

- **Compilation Core**: TypeScript 5.9+, React 19, and Vite 6 build engine operating deterministically on Node.js LTS.
- **Formatting Engines**: Biome 2.5+ AST linter and Tailwind CSS utility compiler ensuring zero styling regressions.
- **Foundation Model Adapters**: Standardized REST adapters connecting cloud reasoning models for slide content generation.

### 4. Data Privacy, Storage, and Retention

- **OWASP LLM & MITRE ATLAS Hardened**: Defended against indirect prompt injection, credential leakage, and unauthorized external API dispatch.
- **Local Environment Isolation**: Agent execution workspaces, intermediate scratchpads, and vector stores reside strictly within designated local project directories.
- **Automated Secret Scrubbing**: API keys, database credentials, and personal credentials are automatically redacted prior to embedding or logging.
- **Zero Commercial Monetization**: Prompts, intermediate reasoning trajectories, and task deliverables are never commercialized or shared with third parties.

---

## Limitations

Understanding the operational boundaries and technical constraints of OpenSlide is essential for effective deployment.

### 1. High-Concurrency Canvas Rendering Overhead
- **Limitation**: Embedding complex interactive 3D WebGL scenes across multiple slides can increase GPU memory utilization.
- **Mitigation**: Lazy-load heavy canvas components only when the active slide enters the immediate viewport buffer.

### 2. Custom Web Font Resolution Dependencies
- **Limitation**: Offline presentation environments without network connectivity cannot download remote Google Fonts.
- **Mitigation**: Automatically bundle local WOFF2 font subsets directly into the compiled standalone deck distribution.

### 3. Dual-Screen Synchronization Across Firewalled Networks
- **Limitation**: Running presenter mode across separate physical devices requires open WebSocket ports on the local network.
- **Mitigation**: Leverage local peer-to-peer WebRTC or fallback to single-screen split presenter mode.

### 4. Highly Nested Component Layout Bleed
- **Limitation**: Deeply nested custom flexbox components can cause unexpected margin collapse in narrow aspect ratios.
- **Mitigation**: Enforce strict parent viewport container clipping with automatic font size downscaling.

### 5. Multi-User Real-Time Collaboration Latency
- **Limitation**: Concurrent slide edits by multiple agents simultaneously can introduce merge collisions in git worktrees.
- **Mitigation**: Segment deck authoring into discrete slide component files with per-file lock arbitration.

---

## Summary & Compliance Checklist

| Checkpoint 2 Requirement | Corresponding Section | Status |
| :--- | :--- | :---: |
| **How the agent decides** | [How the Agent Decides](#how-the-agent-decides) | **Covered** |
| - Decision architecture & 5-stage pipeline | Section 1 | Verified |
| - Decision logic & routing formulations | Section 2 | Verified |
| - Thresholding & refusal decision criteria | Section 3 | Verified |
| - Fallback decision mechanism | Section 4 | Verified |
| - Human-in-the-loop governance & oversight | Section 5 | Verified |
| **The data it uses** | [The Data It Uses](#the-data-it-uses) | **Covered** |
| - Ingested input data & query streams | Section 1 | Verified |
| - Configuration & reference schemas | Section 2 | Verified |
| - Base model lineage & deterministic engines | Section 3 | Verified |
| - Data privacy, retention lifecycle & MITRE/OWASP | Section 4 | Verified |
| **Its limitations** | [Limitations](#limitations) | **Covered** |
| - High-Concurrency Canvas Rendering Overhead | Section 1 | Verified |
| - Custom Web Font Resolution Dependencies | Section 2 | Verified |
| - Dual-Screen Synchronization Across Firewalled Networks | Section 3 | Verified |
| - Highly Nested Component Layout Bleed | Section 4 | Verified |
| - Multi-User Real-Time Collaboration Latency | Section 5 | Verified |
