# Drop Radar

**A real-time drop-alert system with a self-improving AI agent, built in one weekend for a collector in my family.**

Limited releases (trading cards, collectible toys, small-batch watches) sell out in minutes, mostly to bots. Drop Radar watches about 40 stores and community sources around the clock, keeps only what the person actually wants (online, at retail price, from the real store) and puts it on their phone in seconds with a direct link. They still tap Buy themselves.

What makes it different: the alert bot is also a two-way line to an AI agent. The user texts it in plain words, sends a voice note or a screenshot ("watch this brand", "that alert was junk", "this came in late"), and the agent works out the fix, changes its own sources or code, runs the tests and replies with what it changed. The user never touches code.

> This repository is a showcase. The source code and the setup kit are private.
> Want one set up for you? See [taylererbe.com](https://taylererbe.com).

## Results

- **First win within days:** the AI deep search found a 100-piece limited-edition watch that sold out in minutes, and the user got one. None of the scripted trackers caught it.
- **About one second** from a community restock post to the phone.
- **Live 24/7** since 22 October 2026, on one home PC.
- **22 stores researched** for their bot rules and terms before anything was automated.
- 44 automated tests, all on invented data.

## What it does

- **Watches four kinds of source:** store product feeds (new items and back-in-stock), store waiting rooms (a queue appearing means a drop is starting), page and keyword watchers, and news feeds.
- **Three alert levels:** LIVE (buyable now, loud), SOON (announced, normal) and INFO (dashboard only), with quiet hours and de-duplication across sources.
- **Drop windows:** checks every 30 to 60 seconds during each store's known drop hours, slowly the rest of the day.
- **Reminders:** a day before and 15 minutes before announced drops, with time zones converted.
- **Discord:** community restock channels are followed into the user's own server and read through Discord's official live connection, then filtered hard: online only, retail price only, no resellers, no "spotted in a store three states away".
- **Tap-to-choose:** questions to the user arrive as buttons on Telegram, never as walls of text.
- **Purchase and resale ledger (private):** reads a dedicated inbox for order, shipping and eBay sale emails; tracks cost, holdings, profit after fees and ship-by deadlines; suggests sell, hold or watch. All of it stays on the home PC.
- **Weekly check-in:** every week the agent asks the user Keep / Change / Drop about each change it made, plus one open question. The user steers it.

## How the self-improving loop works

```
 user's phone ──text / voice / screenshot──▶ Telegram bot ──▶ feedback inbox
      ▲                                                          │
      │                                                          ▼
  "here's what I changed"  ◀── tests pass ◀── AI agent reads the note, edits sources or code
```

Scheduled reviews run daily and weekly on their own, and a monthly research pass looks for new sources. A source that fails for a day triggers a review automatically.

## Alerts only, by design

Drop Radar tells a person that something is available. It never acts on a store for them.

- It never adds to cart, checks out or buys.
- It never joins, skips or works around a waiting room, never solves CAPTCHAs and never tries to get past bot protection.
- It backs off when a store pushes back, and pauses a source rather than working around it.
- It uses Discord's official bot connection only, in the user's own server.

Every major store bans checkout bots in its terms, so this was a deliberate choice: do the part a person can't (watch everything, all the time) and leave the purchase to the person.

## Built with

Python (standard library only), SQLite, the Telegram Bot API, the Discord Gateway and REST APIs, Gmail over IMAP, GitHub Pages, Windows Task Scheduler, and a Claude Code agent with written rules and a living knowledge file, run on a schedule by an autonomous job queue. ChatGPT served as an independent second opinion on strategy.

## What I learned

- The person using the tool is the real product manager. Every big improvement came from their feedback, which is why the weekly check-in is built in.
- For the rarest drops, an AI that goes looking beats a feed that waits.
- Health checks should tell the truth: "the code ran" is not "the feed is working".
- Read the store rules before building anything.

© 2026 Tayler Erbe. All rights reserved.
