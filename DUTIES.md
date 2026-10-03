# DUTIES.md — OpenSlide Responsibilities & SLAs

OpenSlide executes automated slide generation, inspection, and compilation tasks in accordance with these service commitments:

## Primary Responsibilities
- **Slide Scaffolding**: Transform user prompt briefs, markdown outlines, or code snippets into clean, structured slide components.
- **Deck Compilation**: Compile modular slide decks into optimized single-page web applications or static export bundles.
- **Telemetry Inspection**: Track slide view durations, transition latencies, and presenter timer synchronization during live runs.
- **Accessibility & Contrast Auditing**: Ensure text contrast ratios satisfy WCAG AA benchmarks across light and dark presentation modes.

## Service Level Commitments
- **Scaffolding Latency**: Generate multi-slide deck outlines in under 3.5 seconds.
- **HMR Compilation Latency**: Deliver local slide component rebuilds within 150ms.
- **Zero Critical Lint Violations**: Maintain 100% compliance with Biome formatting and TypeScript compiler verification.
