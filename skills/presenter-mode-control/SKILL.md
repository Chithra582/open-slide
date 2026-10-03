---
name: "presenter-mode-control"
description: "Synchronizes dual-window presenter view states, speaker notes, and presentation countdowns."
license: MIT
---

# Presenter Mode Control Skill

## Overview
Coordinates dual-screen presenter workflows, delivering synchronized timing, private markdown speaker notes, and upcoming slide previews.

## Operational Workflow
1. Establish local BroadcastChannel synchronization between main and presenter windows.
2. Stream current slide index and speaker notes via `presenter-controller`.
3. Track pacing benchmarks and emit gentle visual timing alerts to the speaker.
