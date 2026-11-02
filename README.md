# Liquid Ecosystem

**A local-first, open-source family of desktop productivity applications.**

> **Project status: Early planning (November 2026).** Liquid Calendar is available as a public beta. **Finishing the existing Liquid Calendar roadmap through its stable 1.0.0 release is the first priority.** Liquid Notes, Liquid Mail, Liquid Connect, and Liquid UI Kit are future proposals; substantial development of those projects is planned only after Calendar 1.0.0. This repository documents the ecosystem vision; it does not contain the application source code.

**[Explore the tentative development roadmap](ROADMAP.md)** · **[Liquid Calendar](https://github.com/jonas101201/liquid-calendar)**

## Development order

**Calendar first.** The [Liquid Calendar roadmap](https://github.com/jonas101201/liquid-calendar/blob/main/ROADMAP.md) plans feature milestones **0.4.0–0.10.0**, followed by release candidates and **1.0.0 stable**. This roadmap takes precedence over ecosystem planning. Only after Calendar reaches 1.0.0 will substantial development of the shared UI Kit, Liquid Notes and other Liquid applications begin. There is **no committed completion date** for Calendar or subsequent applications.

See the [ecosystem roadmap](ROADMAP.md) for the dependent phases and tentative feature scope.

## The vision

Liquid aims to bring planning, knowledge management, and communication into a consistent desktop experience. Each app should be fully useful on its own, with optional, privacy-conscious integrations when other Liquid apps are installed.

| Application | Purpose | Current status |
| --- | --- | --- |
| **[Liquid Calendar](https://github.com/jonas101201/liquid-calendar)** | Calendar, tasks, projects, reminders and daily planning | Public beta — actively developed |
| **Liquid Notes** | Feature-rich note-taking, documents and connected knowledge | Planned concept — development not started |
| **Liquid Mail** | Email with offline access and productivity workflows | Long-term concept — development not started |

Two proposed shared foundations would support the apps:

- **Liquid UI Kit:** A reusable PySide6/QML design system for consistent navigation, themes, interactions, and accessibility.
- **Liquid Connect:** Optional local inter-app communication for linking emails, notes, events, and tasks without a Liquid-operated cloud service.

## Guiding principles

- **Local-first:** Application data is stored locally by default; users remain in control.
- **Independent apps:** Calendar, Notes, and Mail must continue working when other Liquid applications are not installed.
- **Optional integration:** Cross-app data exchange should be explicit, permission-aware, and reversible where possible.
- **Open formats and portability:** Prioritize useful import/export and documented data formats.
- **Reliable before flashy:** Data integrity, testing, backups, accessibility, and usability matter more than feature counts.
- **Open source:** Encourage transparent development, user feedback, and contributions.

**Note:** Email delivery and mailbox synchronization necessarily involve third-party email servers. “Local-first” does not mean email can operate without an email provider.

## Platforms

**Linux (especially Fedora / KDE Plasma)** is the current development focus. **Windows** is being considered as a second platform. **macOS is not currently planned.** Platform coverage may evolve based on feasibility and contributors.

## Example future workflows

- Turn an email invitation into a reviewed Calendar event.
- Attach a Notes document to a Calendar event or project.
- Convert a checklist item in Notes into a Calendar task.
- Navigate between related messages, notes, events, and tasks.
- Search across connected apps, only where access is explicitly enabled.

These are **ideas and goals**, not features currently delivered by Liquid Calendar.

## Roadmap and feedback

Read **[ROADMAP.md](ROADMAP.md)** for indicative time windows, phased milestones, open architectural questions, and what is *not* promised.

Suggestions and constructive feedback are welcome through GitHub Issues. For Calendar bugs or feature requests, use the [Liquid Calendar issue tracker](https://github.com/jonas101201/liquid-calendar/issues).

This is an independently developed, ambitious project. **No release dates or future products are guaranteed.**
