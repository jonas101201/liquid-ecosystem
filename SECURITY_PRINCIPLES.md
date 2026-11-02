# Liquid — Local-First & Security Principles

**Status: Architecture policy and proposed requirements, not a certification or an implemented-feature claim.** This document guides future design and reviews. In particular, database encryption and automatic OS-backed unlocking are **not implemented in the current Liquid Calendar beta**.

## Product commitments

1. **Local-first:** User data lives on the user's device by default. Core Calendar/Notes functionality must work without a Liquid account, proprietary backend or internet connection. Network features such as CalDAV are opt-in and documented; Mail necessarily communicates with the user's email provider.
2. **Privacy by default:** No analytics, trackers or uploads of personal content without an explicit, understandable opt-in. Network requests, update checks, integrations and permissions must be documented.
3. **Secure by design:** Protect confidentiality, integrity and availability together. Encrypting a database does not replace sound application security, tested backups or recovery.
4. **Data ownership:** Give users practical export, backup, restore and deletion controls; minimize lock-in.
5. **Independent apps:** Each app owns its data and encryption keys. Local inter-app integration must be optional, narrow and permission-aware.

## Proposed encryption and unlocking model

- **Target:** Encrypt sensitive local databases at rest, evaluating **SQLCipher** for SQLite. Encrypt sensitive attachment storage, backups and other persisted copies as well; review search indexes, SQLite WAL/journal files, temporary files, logs and exports.
- **Keys:** Generate unique, high-entropy data encryption keys per application/database, using vetted cryptographic libraries. Never hardcode keys, place them in source control, or store them in plaintext adjacent to encrypted data.
- **Convenient default:** Where supported, protect/retrieve the key through the OS credential store (e.g. **KDE Wallet / Secret Service** on Linux, appropriate **Windows credential protection** on Windows). Reuse an already-unlocked system wallet where secure and possible; avoid an unnecessary Liquid password prompt on every launch.
- **Optional extra protection:** Offer an additional password-based lock for users who require it; evaluate **Argon2id** for password-derived key wrapping. Explain that the additional mode may limit unattended reminders and background access.
- **Recovery:** Design key migration, password changes, encrypted backup portability and a user-controlled recovery option *before* rollout. Never promise that a forgotten password/key can be recovered if it cannot.
- **Fallback:** If secure OS key storage is unavailable, explain the limitation and offer a safe password-based setup rather than silently falling back to plaintext.
- **Platform specifics:** The Linux Plasma widget should never read or embed plaintext database keys in QML. Evaluate a minimal authenticated local service for approved event data; design secure reminder access when the UI is closed.

**Threat-model boundary:** At-rest encryption helps if a database or backup file is copied or a device is lost while keys are unavailable. It does **not** reliably defend against malware acting as the signed-in user, an unlocked app, or a compromised operating system. Full-disk encryption remains recommended.

## Validation required before claiming encryption support

- [ ] Document threat model, assets, trust boundaries and OS/Flatpak constraints.
- [ ] Inventory all persistent data paths, attachments, logs, caches, indexes, backup formats and widget access.
- [ ] Prototype SQLCipher integration and verify dependency licensing, packaging and platform support.
- [ ] Design migration from existing plaintext SQLite with atomic rollback, space checks and recovery from interruptions.
- [ ] Verify wrong-key handling, key rotation, wallet locked/unavailable, upgrade/downgrade and password recovery workflows.
- [ ] Verify event reminders and Plasma widget behavior while app/window is closed or locked.
- [ ] Test backup encryption, restore and device migration without information leakage.
- [ ] Test with real data-size samples; include adversarial and failure-injection checks.
- [ ] Update user-facing privacy/security documentation with actual capabilities and limits.

## Roadmap alignment

The **[Liquid Calendar roadmap](https://github.com/jonas101201/liquid-calendar/blob/main/ROADMAP.md)** remains the prerequisite for ecosystem expansion. Security design and research happen during Calendar's beta phase; a stable, usable implementation should be scheduled against Calendar's 0.10/1.0 quality gate after feasibility and migration validation. Changes to milestone scope must be recorded in Calendar's own roadmap.

A future shared component may be called **Liquid Security**, but it must not introduce mandatory cross-app accounts, shared master keys or tight coupling. Reuse carefully reviewed security primitives and interfaces, not a homemade encryption algorithm.
