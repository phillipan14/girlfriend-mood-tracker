# DEFCON: RELATIONSHIP

**Cross-references text response times, emoji usage, and calendar events to predict relationship danger zones.**

![Zero Dependencies](https://img.shields.io/badge/dependencies-0-brightgreen)
![Relationship Status](https://img.shields.io/badge/relationship%20status-it's%20complicated-orange)
![Works On My Machine](https://img.shields.io/badge/works%20on-my%20machine-blue)
![Girlfriend Approved](https://img.shields.io/badge/girlfriend%20approved-pending-yellow)
![License](https://img.shields.io/badge/license-MIT-green)

A single HTML file. No dependencies. No build step. No backend. Just open it and find out how much trouble you're in.

---

## Features

- **DEFCON Threat Meter** -- Animated gauge that swings from "All Clear" to "Sleep on the Couch"
- **Intercepted Signals** -- Real-time feed of relationship red flags, sorted by severity
- **Danger Zone Calendar** -- Color-coded month view showing upcoming threat days
- **Mood Factor Analysis** -- Breakdown of what's driving the current threat level
- **6 Pre-Built Scenarios** -- From "Honeymoon Phase" to "We Need to Talk"
- **Keyboard Shortcuts** -- Press 1-6 to switch scenarios instantly
- **CRT Aesthetic** -- Dark ops-center theme with scanlines, because relationship analysis is serious business

## Quick Start

```bash
git clone https://github.com/phillipan14/girlfriend-mood-tracker.git
open girlfriend-mood-tracker/index.html
```

That's it. No `npm install`. No `docker compose`. No existential dread about dependency versions. Just a file and a browser.

## Scenarios

| # | Scenario | DEFCON | Description |
|---|----------|--------|-------------|
| 1 | Honeymoon Phase | 5 | Everything is perfect. Too perfect. |
| 2 | Forgot Anniversary | 1 | The calendar knows. She knows you don't know. |
| 3 | Left on Read (6 Hours) | 2 | Two blue checkmarks. Zero replies. Maximum anxiety. |
| 4 | Liked Ex's Instagram | 1 | She has notifications on. She always has notifications on. |
| 5 | Brought Home Flowers | 4 | Threat level decreasing. Diplomacy is working. |
| 6 | "We Need to Talk" | 1 | Five words. Zero survivors. |

## How the Algorithm Works

The Boyfriend Intelligence Agency (BIA) uses a proprietary five-factor threat model:

| Factor | Weight | What It Measures |
|--------|--------|------------------|
| Response Time | 30% | How long she takes to reply vs. her baseline |
| Emoji Sentiment | 20% | Emoji frequency drop = emotional shutdown |
| Calendar Risk | 20% | Missed anniversaries, scheduling conflicts, suspicious events |
| Text Length | 15% | Going from paragraphs to "k" is never good |
| "Fine" Index | 15% | Frequency of "fine", "k", "whatever", "ok" as complete messages |

These scores combine into a composite threat level, mapped to DEFCON 1-5 (because if the military can track incoming missiles, you can track incoming arguments).

## Adding Your Own Scenario

Edit the `SCENARIOS` object in `index.html`:

```javascript
'your-scenario': {
  name: 'Your Scenario Name',
  emoji: '...',
  description: 'A brief description',
  messages: [
    { time: '9:00 AM', text: 'message text', responseTimeMin: 5, emojis: [], sender: 'her' },
    // ... more messages
  ],
  events: [
    { date: 15, title: 'Event name', category: 'conflict', riskLevel: 80 },
    // ... more events
  ]
}
```

PRs with new scenarios are welcome. Bonus points if they're based on real experiences (names changed to protect the guilty).

## Integrations (Architecture Ready)

The codebase is designed with adapter hooks for real data sources:

- iMessage / SMS export
- Google Calendar API
- WhatsApp chat export
- Custom CSV import

These aren't wired up yet because, honestly, if you're feeding real relationship data into a threat assessment algorithm, you might need a different kind of help.

## Tech Stack

- HTML
- CSS
- JavaScript
- Canvas API
- That's it. That's the stack.

## Disclaimer

This is a joke. Please do not actually use this to manage your relationship. If your partner finds out you're running threat analysis on their texting patterns, no algorithm can predict the DEFCON level that follows.

Talk to your partner like a normal human being.

## License

MIT -- because love should be open source.
