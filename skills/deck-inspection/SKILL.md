---
name: "deck-inspection"
description: "Inspects slide decks for visual overflow, contrast compliance, and performance bottlenecks."
license: MIT
---

# Deck Inspection Skill

## Overview
Performs automated automated quality checks on compiled slide decks, identifying typography overflows, broken image links, and accessibility contrast issues.

## Operational Workflow
1. Initialize inspection session using `inspector-telemetry`.
2. Measure element bounding boxes and text contrast ratios.
3. Emit structural diagnostic reports highlighting remediation recommendations.
