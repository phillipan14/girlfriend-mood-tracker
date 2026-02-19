# Girlfriend Mood Tracker — Implementation Plan

> **For Claude:** REQUIRED SUB-SKILL: Use superpowers:executing-plans to implement this plan task-by-task.

**Goal:** Build a single-file, zero-dependency "DEFCON: Relationship" dashboard that predicts danger zones from mock relationship data.

**Architecture:** Single `index.html` with embedded CSS + JS. Mock data engine generates scenarios. Weighted scoring algorithm produces threat levels. Canvas API for the gauge. CSS grid for layout. localStorage for persistence.

**Tech Stack:** Vanilla HTML/CSS/JS, Canvas API, localStorage

---

### Task 1: Scaffold — HTML skeleton + dark theme CSS + layout grid

**Files:**
- Create: `index.html`

**Step 1: Create base HTML with embedded CSS**

Build the page shell with:
- Dark ops-center theme (background #0a0a0a, green/amber/red accents)
- CSS grid layout: threat meter (top center), signal timeline (left), calendar (right), factors panel (bottom)
- Monospace font stack (JetBrains Mono from Google Fonts as progressive enhancement, fallback to system monospace)
- Subtle CRT scan-line overlay effect via CSS
- Header: "DEFCON: RELATIONSHIP" with pulsing subtitle "THREAT ASSESSMENT SYSTEM"
- Scenario selector bar (buttons, not wired yet)
- Empty placeholder divs for each section with section headers

**Step 2: Verify in browser**

Open `index.html` — should see dark themed grid layout with labeled empty sections and the header.

**Step 3: Init repo and commit**

```bash
cd ~/girlfriend-mood-tracker
git init
git add index.html docs/
git commit -m "feat: scaffold HTML skeleton with dark ops-center theme and grid layout"
```

---

### Task 2: Mock Data Engine — scenarios + data structures

**Files:**
- Modify: `index.html` (add `<script>` section)

**Step 1: Define data structures and mock scenarios**

Add JS at bottom of `index.html`:

- `Message` object: `{ time, text, responseTimeMin, emojis[], sender }`
- `CalendarEvent` object: `{ date, title, category, riskLevel }`
- `Scenario` object: `{ name, description, messages[], events[], daysSince }`
- Build 6 scenarios with realistic mock data:
  1. **"Honeymoon Phase"** — fast replies, lots of emojis, no conflicts
  2. **"Forgot Anniversary"** — anniversary in calendar, zero mentions in texts, response times normal (she's planning the test)
  3. **"Left on Read (6 Hours)"** — one message sent, no reply, escalating follow-ups
  4. **"Liked Ex's Instagram"** — sudden short responses, "fine" appearing, calendar suddenly "busy"
  5. **"Brought Home Flowers"** — threat level recovering, emoji usage spiking back up
  6. **"Said 'We Need to Talk'"** — the nuclear option, all signals red

- `loadScenario(name)` function that populates global state
- Default to "Forgot Anniversary" on load (dramatic first impression)

**Step 2: Verify in console**

Open browser console, confirm `loadScenario("forgot-anniversary")` populates data and logs it.

**Step 3: Commit**

```bash
git add index.html
git commit -m "feat: add mock data engine with 6 relationship scenarios"
```

---

### Task 3: Threat Level Algorithm — the "AI" scoring engine

**Files:**
- Modify: `index.html`

**Step 1: Build weighted scoring functions**

Add scoring module:

- `calcResponseTimeScore(messages)` — compare avg response time to baseline (3min). Score 0-100. >30min = 80+. >2hrs = 100.
- `calcEmojiScore(messages)` — ratio of emoji messages to total. Baseline ~60%. Dropping below 20% = danger. Zero emojis = max threat.
- `calcCalendarScore(events)` — detect conflicts (overlapping categories), missed milestones (anniversary/birthday with no prep), dangerous combos ("her parents" + "boys night")
- `calcTextLengthScore(messages)` — avg char count trend. Going from paragraphs to "k" = critical.
- `calcFineIndex(messages)` — frequency of "fine", "k", "whatever", "okay", "sure" as complete messages
- `calcThreatLevel()` — weighted composite:
  - Response Time: 30%
  - Emoji Usage: 20%
  - Calendar Risk: 20%
  - Text Length: 15%
  - "Fine" Index: 15%
- Map composite 0-100 score to DEFCON 1-5 (inverted — DEFCON 1 is worst)

**Step 2: Verify in console**

Load each scenario, call `calcThreatLevel()`, confirm sensible DEFCON levels:
- Honeymoon → DEFCON 5
- Forgot Anniversary → DEFCON 1-2
- Left on Read → DEFCON 2-3

**Step 3: Commit**

```bash
git add index.html
git commit -m "feat: add weighted threat level scoring algorithm"
```

---

### Task 4: DEFCON Threat Meter — Canvas gauge with animation

**Files:**
- Modify: `index.html`

**Step 1: Build animated gauge**

- Canvas-based semicircular gauge
- Color gradient from green (right) through yellow/orange to red (left)
- Animated needle that swings to current threat level on load and scenario change
- Large DEFCON number display below gauge
- Status text: "ALL CLEAR" / "SLIGHT DISTURBANCE" / "PROCEED WITH CAUTION" / "DANGER ZONE" / "SLEEP ON THE COUCH"
- Pulsing red glow effect when DEFCON 1 (CSS animation on container)
- `renderGauge(defconLevel)` function with requestAnimationFrame for smooth needle animation

**Step 2: Verify visually**

Load page — gauge should animate from 0 to current threat level. Switch scenarios to see it move.

**Step 3: Commit**

```bash
git add index.html
git commit -m "feat: add animated DEFCON threat meter gauge"
```

---

### Task 5: Signal Timeline — scrolling feed of intercepted signals

**Files:**
- Modify: `index.html`

**Step 1: Build signal timeline component**

- Scrollable container (max-height, overflow-y)
- Each signal is a card with:
  - Timestamp (monospace, green)
  - Icon (emoji based on type)
  - Description text
  - Severity badge (color-coded: green/yellow/orange/red)
- `generateSignals(scenario)` function that converts scenario data into signal entries:
  - Response time anomalies
  - Emoji drops
  - Calendar conflicts
  - "Fine" detections
  - Text length crashes
- Signals sorted by severity (worst first)
- New signals fade in with CSS animation

**Step 2: Verify visually**

Load "Forgot Anniversary" — should see multiple red/orange signals. Load "Honeymoon Phase" — should see green signals.

**Step 3: Commit**

```bash
git add index.html
git commit -m "feat: add scrolling signal timeline feed"
```

---

### Task 6: Danger Zone Calendar — color-coded month view

**Files:**
- Modify: `index.html`

**Step 1: Build calendar component**

- CSS grid calendar (7 columns, Sun-Sat)
- Month/year header with prev/next arrows
- Each day cell color-coded based on predicted threat for that day
- Today highlighted with border
- Hover tooltip showing why a day is flagged (e.g., "Valentine's Day — no reservation detected")
- `renderCalendar(month, year, events)` function
- Days with events get a small dot indicator
- "Danger days" pulse subtly

**Step 2: Verify visually**

Calendar renders current month, some days show colored threat levels matching scenario events.

**Step 3: Commit**

```bash
git add index.html
git commit -m "feat: add color-coded danger zone calendar"
```

---

### Task 7: Mood Factors Panel — score breakdown

**Files:**
- Modify: `index.html`

**Step 1: Build factors breakdown**

- Horizontal bar chart for each factor (CSS, no canvas needed)
- Each bar shows: factor name, score 0-100, color based on severity
- Factors:
  - Response Time Score
  - Emoji Sentiment Score
  - Calendar Risk Score
  - Text Length Trend
  - "Fine" Frequency Index
- Bars animate on load (CSS transition width)
- Small explanatory text under each bar (e.g., "Avg reply: 47min — baseline: 3min")

**Step 2: Verify visually**

Switch scenarios — bars should animate to different levels. "Forgot Anniversary" should show high calendar risk.

**Step 3: Commit**

```bash
git add index.html
git commit -m "feat: add mood factors breakdown panel"
```

---

### Task 8: Scenario Selector — wire up buttons + transitions

**Files:**
- Modify: `index.html`

**Step 1: Wire scenario switching**

- Style scenario buttons in top bar
- Click handler: load scenario → recalculate scores → animate all components
- Brief "RECALCULATING..." flash overlay during transition
- Active scenario button highlighted
- Each button shows scenario name + a small emoji hint

**Step 2: Verify end-to-end**

Click through all 6 scenarios. Each should:
- Move the gauge needle
- Update signal timeline
- Recolor calendar
- Animate factor bars
- Change DEFCON status text

**Step 3: Commit**

```bash
git add index.html
git commit -m "feat: wire scenario selector with animated transitions"
```

---

### Task 9: Polish — responsive design, animations, details

**Files:**
- Modify: `index.html`

**Step 1: Add finishing touches**

- Responsive: stack layout vertically on mobile (<768px)
- CRT flicker animation on page load (brief, then stops)
- Footer: "CLASSIFIED — BOYFRIEND INTELLIGENCE AGENCY (BIA)"
- Keyboard shortcuts: 1-6 to switch scenarios
- Favicon: red warning emoji via SVG data URI
- Meta tags: og:title, og:description for social sharing
- Subtle ambient sound toggle (optional, off by default) — just a CSS toggle button, no actual audio

**Step 2: Test on mobile viewport**

Chrome DevTools responsive mode — verify layout stacks cleanly.

**Step 3: Commit**

```bash
git add index.html
git commit -m "feat: add responsive design, polish, and meta tags"
```

---

### Task 10: README — the showpiece

**Files:**
- Create: `README.md`

**Step 1: Write the README**

- Hero: large screenshot of DEFCON 1 state
- Badges: `Zero Dependencies`, `Relationship Status: It's Complicated`, `Works On My Machine`, `Girlfriend Approved: Pending`
- One-liner description
- Feature list with emoji
- "How the Algorithm Works" section (tongue-in-cheek explanation of the weights)
- Scenarios gallery (table with name + description + DEFCON level)
- "Quick Start" — literally just `open index.html`
- "Adding Your Own Scenario" — contributing guide
- "Integrations (Coming Soon)" — list the adapter hooks
- "Disclaimer" — "This is a joke. Please do not actually use this to manage your relationship. Talk to your partner like a normal human being."
- License: MIT

**Step 2: Commit**

```bash
git add README.md
git commit -m "docs: add README with badges, features, and disclaimer"
```

---

### Task 11: GitHub Setup — create repo + push

**Step 1: Create GitHub repo and push**

```bash
cd ~/girlfriend-mood-tracker
gh repo create girlfriend-mood-tracker --public --description "Cross-references text response times, emoji usage, and calendar events to predict relationship danger zones. Zero dependencies. One HTML file." --source . --push
```

**Step 2: Enable GitHub Pages (optional)**

```bash
gh api repos/phillipan14/girlfriend-mood-tracker/pages -X POST -f source.branch=main -f source.path=/
```

**Step 3: Verify**

Visit repo URL — README renders, index.html accessible via Pages.
