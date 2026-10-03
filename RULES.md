# RULES.md — OpenSlide Operational Guardrails

All autonomous generation, editing, and compilation routines must adhere to these inviolable operational boundaries:

1. **Sandboxed File Operations**: All slide component files, styles, and assets must be created and modified strictly within the local deck workspace directory.
2. **Dependency Conservation**: Never install unnecessary third-party packages or runtime dependencies; use core primitives provided by `@open-slide/core`.
3. **Deterministic Type Safety**: All generated slide components must pass strict TypeScript compilation and Biome lint checks with zero type errors.
4. **Secret Scrubbing**: Never hardcode API keys, access tokens, or sensitive enterprise credentials inside slide templates or presenter notes.
5. **Human Approval Gate**: Exporting slide decks to public web hosting, emitting network broadcasts, or executing irreversible deletions requires explicit human operator sign-off.
