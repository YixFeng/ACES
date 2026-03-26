# ACES: Adaptive Cognitive Evaluation System for Student Assessment

[![GitHub Pages](https://img.shields.io/github/actions/workflow/status/wjrforcyber/ACES/deploy.yml?branch=main&label=GitHub%20Pages&style=flat-square)](https://wjrforcyber.github.io/ACES/)
[![Deployment](https://img.shields.io/github/deployments/wjrforcyber/ACES/github-pages?label=Deploy&style=flat-square)](https://github.com/wjrforcyber/ACES/deployments)

A bilingual (Chinese + English) prototype website for teacher-completed initial assessment of students, based on the ACES proposal.

## Overview

This project is a pure frontend implementation (`HTML/CSS/JavaScript`) for classroom pilot use.

- No backend server
- No login/auth
- Local storage only (`localStorage`)
- JSON export for record sharing/archive
- Not for medical diagnosis

## Features

- Bilingual UI (Chinese and English shown together)
- 4 assessment modules, 16 questions, 5-point Likert scale
- Required-field validation
- Progress indicator
- Automatic track recommendation:
  - Employment Readiness Track
  - Independent Living Skills Track
  - Basic Behavioral Management Track
- Reassessment warning when top-two track score gap `< 8`
- Draft save/recover from local storage
- Local history list (load/delete/export)

## Tech Stack

- `index.html`
- `styles.css`
- `app.js`

No package manager or build step is required.

## Run Locally

From project root:

```bash
python3 -m http.server 4173
```

Then open:

- `http://127.0.0.1:4173`

## Scoring Logic

Each question is scored `1-5`, module score is normalized to `0-100`.

Track fit scores:

```text
employment_fit  = 0.35*cog + 0.35*comm + 0.20*life + 0.10*sensory
independent_fit = 0.20*cog + 0.20*comm + 0.45*life + 0.15*sensory
basic_fit       = 0.40*(100-cog) + 0.30*(100-comm) + 0.20*(100-life) + 0.10*(100-sensory)
```

The highest fit score becomes the final recommended track.

## Local Storage Keys

- `aces_assessment_draft`
- `aces_assessment_records`

## Exported JSON (core fields)

- `meta`
- `answers`
- `moduleScores`
- `trackScores`
- `finalTrack`
- `timestamp`

Includes bilingual fields like:

- `questionText.zh` / `questionText.en`
- `moduleName.zh` / `moduleName.en`

## Notes

- This prototype is intended for course/session demonstration and pilot testing.
- For production use, add backend persistence, authentication, and data governance controls.
