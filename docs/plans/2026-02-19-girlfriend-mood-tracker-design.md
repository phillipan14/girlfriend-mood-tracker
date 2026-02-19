# Girlfriend Mood Tracker — Design Doc

**Date:** 2026-02-19
**Status:** Approved
**Tone:** Tongue-in-cheek humor. Serious engineering, unserious premise.

## Overview

A single-file, zero-dependency web app that cross-references text response times, emoji usage, and calendar events to predict relationship "danger zones." Ships with hilarious mock data, dark military ops-center aesthetic. Designed to go viral on GitHub.

## Architecture

- **Format:** Single `index.html` file (~1000 lines). Clone → open in browser.
- **Styling:** Embedded CSS, dark theme (military/ops center vibe)
- **Data:** Embedded mock dataset + localStorage for user input
- **Charts:** Canvas API only (zero external dependencies)
- **"AI" Engine:** Weighted scoring algorithm — response time decay + emoji sentiment + calendar conflict detection

## Core Features

### 1. DEFCON Threat Meter
Big animated gauge, center of the dashboard. Scale 1-5:
- **DEFCON 5:** "All Clear" (green)
- **DEFCON 4:** "Slight Disturbance" (yellow-green)
- **DEFCON 3:** "Proceed With Caution" (yellow)
- **DEFCON 2:** "Danger Zone" (orange)
- **DEFCON 1:** "Sleep on the Couch" (red)

Animates on load and on data changes.

### 2. Signal Timeline
Scrolling feed of "intercepted signals":
- Response time anomalies (e.g., "Response time: 47min — baseline: 3min — ELEVATED")
- Emoji usage shifts (e.g., "Emoji usage dropped 80% — CRITICAL")
- Calendar conflicts (e.g., "'Dinner with your mom' + 'Boys night' same day — DANGER")
- Text length changes (e.g., "Average text length: 2 words — down from 47 — RED ALERT")

### 3. Danger Zone Calendar
Month view. Days color-coded green/yellow/orange/red. Hover tooltips explain flags:
- "Valentine's Day — no reservation detected"
- "Anniversary — 0 mentions in recent texts"
- "Sunday — her parents visiting + your fantasy draft"

### 4. Mood Factors Panel
Breakdown of what's contributing to current threat level:
- Response Time Score (weighted highest)
- Emoji Sentiment Score
- Calendar Risk Score
- Text Length Trend
- "Fine" Frequency Index (how often "fine" or "k" appears)

### 5. Mock Data Scenarios
Button to cycle through pre-built scenarios:
- "Honeymoon Phase" — all green, hearts everywhere
- "Forgot Anniversary" — instant DEFCON 1
- "Left on Read (6 Hours)" — escalating threat
- "Liked Ex's Instagram" — maximum danger
- "Brought Home Flowers (No Reason)" — threat level dropping
- "Said 'We Need to Talk'" — DEFCON 1, all signals red

### 6. Integration Architecture (hooks, not wired)
Clearly documented adapter pattern for:
- iMessage / SMS export
- Google Calendar API
- WhatsApp export
- Custom CSV import

## Visual Design

- Dark background (#0a0a0a to #1a1a1a)
- Green/amber/red terminal-style text
- Monospace fonts for the "intercepted signals"
- Subtle scan-line CSS effect
- Pulsing red glow on DEFCON 1

## README Plan

- Hero screenshot of DEFCON 1 state
- Badges: "Zero Dependencies", "Relationship Status: It's Complicated", "Works On My Machine"
- Quick humor-driven description
- Feature list with emoji
- "How It Works" section explaining the "algorithm"
- Scenarios gallery
- Contributing section encouraging new scenarios
- License: MIT

## Non-Goals

- No backend / server
- No real AI/ML (the weighted algorithm IS the joke)
- No user accounts or persistence beyond localStorage
- No mobile app (responsive web is fine)
