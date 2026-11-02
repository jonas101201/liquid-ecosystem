# Liquid Ecosystem — Tentative Development Roadmap

**Updated:** 2026-11-02  
**Stage:** Long-term vision / early planning  
**Current product:** [Liquid Calendar](https://github.com/jonas101201/liquid-calendar) (public beta)

> **Planning document, not a release commitment.** Dates, features, scope and sequencing are provisional. The goal is to build software people can depend on, not to ship every idea on a fixed schedule.

## Project status at a glance

| Initiative | Status | Priority |
| --- | --- | --- |
| Liquid Calendar | **In development — public beta** | Current focus |
| Liquid UI Kit | **Planned** | Foundation for future apps |
| Liquid Notes | **Planned concept — not started** | Next major application |
| Liquid Connect | **Planned concept — not started** | Introduce alongside Notes integration |
| Windows support | **Under consideration** | After the core Linux experience |
| Liquid Mail | **Long-term concept — not started** | Explore after the first two apps are stable |

## Indicative timeline

| Planning window | Focus | Confidence |
| --- | --- | --- |
| **Q4 2026 – Q1 2027** | Stabilize Liquid Calendar, address critical bugs, test recovery and improve release/install experience | Near-term focus, not a 1.0 deadline |
| **Q1 – Q2 2027** | Extract shared UI patterns and prototype Liquid UI Kit | Tentative |
| **Q2 – Q4 2027** | Explore and build the first Liquid Notes versions; seek external testers | Aspirational |
| **Q4 2027 – Q2 2028** | Prototype optional Calendar ↔ Notes integration and evaluate Windows builds | Aspirational |
| **2028+** | Improve ecosystem cohesion; research Liquid Mail architecture and viability | Exploratory, no release date |

These windows will be revised based on feedback, available development time, stability and technical feasibility. They **do not supersede** the [separate Liquid Calendar roadmap](https://github.com/jonas101201/liquid-calendar/blob/main/ROADMAP.md), which includes its existing 0.4–0.10 beta milestones.

---

## Phase 1 — A dependable Liquid Calendar

**Status:** In progress

The existing Calendar beta is the starting point. Prioritize reliability and real-world use before launching another major app.

- [ ] Resolve confirmed high-impact reminder/notification defects.
- [ ] Audit critical data paths, conflict handling and database recovery.
- [ ] Test backup and restore workflows with representative datasets.
- [ ] Improve responsiveness with larger calendars and task lists.
- [ ] Test clean installations, updates, and Flatpak packaging.
- [ ] Improve keyboard access, accessibility, onboarding and documentation.
- [ ] Recruit external testers and prioritize their reproducible feedback.
- [ ] Define quality-based criteria for a future stable release.

**Exit criteria:** People can install, use, update and recover Calendar confidently. A stable version number will only follow adequate validation—not an arbitrary date.

## Phase 2 — Liquid UI Kit

**Status:** Planned

Create a reusable design language rather than copying entire Calendar UI files into each new application.

- [ ] Inventory existing Calendar QML components and visual tokens.
- [ ] Define shared colors, typography, spacing, glass surfaces and motion guidelines.
- [ ] Make themes, scaling, keyboard navigation and reduced-motion preferences first-class concerns.
- [ ] Extract versioned PySide6/QML components with documented APIs.
- [ ] Add component tests and relevant visual regression checks.
- [ ] Ensure the UI Kit does not import application-specific Calendar logic.

**Exit criteria:** Notes can use the shared design system without depending on Calendar itself.

## Phase 3 — Liquid Notes

**Status:** Planned concept; implementation not started

A **feature-rich** desktop notes and knowledge-management application, not merely a basic text editor.

### Potential capabilities

- [ ] Markdown editing with a carefully chosen rich-text strategy.
- [ ] Folders/workspaces, tags, favorites, templates and advanced search.
- [ ] Internal links, backlinks and optional knowledge graph views.
- [ ] Checklists, tables, code blocks, attachments and split views.
- [ ] Document recovery, history, import/export and portable data access.
- [ ] Optional Canvas / visual knowledge organization.
- [ ] Optional links to Calendar events, tasks and projects.

### Architectural decisions to research first

- [ ] Select a robust editor foundation (rather than rebuilding complex editing from scratch).
- [ ] Choose a durable document model and determine what can be exported losslessly to Markdown.
- [ ] Separate editor/UI, persistence, search indexing, attachments and application services.
- [ ] Define autosave, corruption recovery, migrations and attachment security.
- [ ] Design for Linux first while minimizing unnecessary Windows-specific porting work.

**Exit criteria:** A testable Notes beta with reliable editing and data portability. The entire potential feature list is **not** required before the first beta.

## Phase 4 — Liquid Connect

**Status:** Planned concept; implementation not started

An optional, local integration SDK/protocol—not a mandatory all-in-one process or cloud backend.

### Proposed workflows

- [ ] Create a draft Calendar event from a selected email or note.
- [ ] Create a Calendar task from a Notes checklist item.
- [ ] Link stable Notes IDs to Calendar resources.
- [ ] Open linked resources in the correct application.
- [ ] Explore consent-based, cross-application search.

### Design constraints

- Each application owns its own data and keeps working independently.
- Use stable resource identifiers and documented, versioned APIs.
- Validate permissions and caller identity; do not trust arbitrary local input.
- Handle missing, offline or incompatible application versions gracefully.
- Evaluate **D-Bus on Linux** and an appropriate local IPC adapter on Windows.
- Avoid giving one app broad, implicit access to another app's data.

**Exit criteria:** At least one Calendar ↔ Notes workflow works reliably in both directions without breaking standalone use.

## Phase 5 — Windows feasibility and releases

**Status:** Under consideration; no platform release promised

- [ ] Separate operating-system integrations from reusable Python/application logic.
- [ ] Prototype Notes packaging, installation, notifications and credential storage as relevant.
- [ ] Evaluate Calendar's KDE-specific integrations and replacement adapters.
- [ ] Test on actual Windows systems, including upgrades and uninstall/reinstall.
- [ ] Adapt Liquid Connect transport, application links and IPC permissions.
- [ ] Make a release decision based on support and maintenance capacity.

The Plasma widget remains a Linux/KDE-specific feature. macOS support is **not planned** at this stage.

## Phase 6 — Liquid Mail research

**Status:** Long-term exploration only; development not started

A full mail client is much more demanding than a simple local utility. Research and security validation come before committing to a product.

### Potential features

- [ ] Multi-account IMAP / SMTP mail workflows.
- [ ] OAuth 2.0 where providers require it and secure credential storage.
- [ ] Offline mailbox caching, background synchronization and reconnection behavior.
- [ ] Search, conversation views, drafts, attachments and folder organization.
- [ ] Restricted HTML email rendering, blocked remote content and safe links/attachments.
- [ ] Optional selected-message links to Notes, Calendar events and tasks.

### Go / no-go questions

- Can authentication and provider compatibility be maintained responsibly?
- Can we handle disconnections and synchronization conflicts without message loss?
- Is there enough time to test security-sensitive functionality?
- Does the app offer real value beyond established clients?
- Can users rely on it for important communication?

**No target release window or promise to ship Liquid Mail has been made.** There is no plan to host a mail server or proprietary mail cloud.

---

## Engineering and release principles

1. **Independent apps and narrow interfaces:** Shared libraries should not force shared databases or tight coupling.
2. **Safety of user data:** Use atomic operations, migrations, recovery tests and portable exports.
3. **Testing at multiple levels:** Unit, integration, UI and platform tests, backed by manual desktop validation.
4. **Review every meaningful change:** Automated checks and AI-assisted reviews help, but cannot replace real testing.
5. **Accessible by design:** Keyboard support, contrast, scalable layouts and reduced motion.
6. **No silent data sharing:** Integrations require appropriate user intent and least-privilege access.
7. **Community-informed priorities:** Real problems and adoption matter more than speculative feature counts.

## What this roadmap does not promise

- Specific release dates for Notes, Mail or the ecosystem as a whole.
- A fully synchronized cloud service or mandatory account infrastructure.
- macOS support.
- Immediate support for every Linux distribution.
- Delivery of every feature listed here.

Features may move, change or be cancelled. The project currently prioritizes **usefulness, reliability, privacy and long-term maintainability** over velocity.

## Contributing feedback

Please use [GitHub Issues](https://github.com/jonas101201/liquid-ecosystem/issues) to discuss ecosystem ideas and priorities. File Calendar-specific bugs in [Liquid Calendar](https://github.com/jonas101201/liquid-calendar/issues).

This repository describes the **vision and planning** for the application family. Application code continues to live in its own repository.
