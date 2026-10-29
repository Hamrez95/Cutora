# Cutora: repository instructions

## Start and authority

- Read `START.md`, `docs/decisions/USER_DECISIONS.md`, and `docs/implementation/STATUS.md` before implementing or resuming.
- The human's latest instruction wins. Current handoff instructions supersede historical review-only STOP statements in `docs/planning/` and `docs/reference/ORIGINAL_BRIEF.md` when the human asks to execute START on the target PC.
- This repository currently contains planning and concept mockups, not working application code. Do not present design as implementation.
- Keep UI and user-facing reports in natural Persian; product name is Cutora / کاتورا. Existing mockups retain the old HomeVlog Studio label as historical design references.

## Scope and autonomy

- On an authorized START run, implement the bounded personal Windows release through the PLAN milestones, including tests and installer; do not stop after scaffolding or a single spike merely to request the same approval again.
- Use observed hardware and the current repository state. Do not hardcode paths, drive letters, credentials, machine usernames, GPU availability, or the source machine's capacity figures.
- Keep the app local-first. No paid services, subscriptions, license purchases, public deployment, social publishing, account messaging, or private-media upload without specific human authorization.
- DaVinci is the main editor. Do not build a competing timeline/compositor, social scheduler, or analytics platform.
- Resolve integration is capability-based. Unsupported functionality must be visibly unavailable with a genuine fallback; never return fake success or pretend to control Resolve.

## Data safety

- Camera/card/external source is read-only by default. Ingest, categorization, AI and background jobs must never delete or overwrite originals.
- Copy, archive, working copy, backup, relocation and restore are different operations. Implement `docs/specs/MEDIA_WORKFLOWS.md`, including preview, checksums, replica state, cancellation and recovery.
- Exact dedupe uses whole-file content hash. A redundant filename, similar video, quick hash or AI tag is never enough to remove data.
- Release of an old original after a relocation requires a clear per-operation human authorization, verified destination and the independent retained copy required by the spec. Missing backup may allow safe copy, but must prevent destructive cleanup.
- Never recursively delete computed user paths. Cache cleanup is confined to resolved app-owned paths and must reject traversal, symlinks/reparse escapes and archive roots.
- Never use real originals for corruption, interruption or delete tests. Use synthetic fixtures or disposable authorized copies.
- Media and personal catalogs stay outside the repository. Do not commit real footage, source manifests, secrets, models, render output or local machine state.

## Engineering and verification

- Baseline: Electron + React + TypeScript + Node + SQLite + FFmpeg/FFprobe. Processing and database work stay outside the renderer; IPC and process arguments must be validated.
- Inspect existing code/instructions before edits. Preserve unrelated work. Use narrow commits; never force-push or rewrite remote history without explicit permission.
- Choose compatible supported versions using current official docs at implementation time; pin dependencies and binary provenance. Test native SQLite ABI and clean-machine installation early.
- Import/transfer state is durable, journaled and idempotent. Filesystem operations and SQLite transactions are not magically one atomic transaction; implement reconciliation.
- A green status must correspond to verified observable state. Keep `copy_verified`, `backup_verified`, `offline`, `pending`, `failed`, `unknown` and `needs_review` distinguishable.
- Check integrity separately from media decodability. Hardware acceleration needs runtime probing and a working CPU fallback.
- Keep heavy work off the UI thread; use bounded queues, virtualized media grids and on-demand proxies.
- Every completed milestone requires relevant real tests and evidence. Record pass/fail/not-run honestly; no demo-only completion, simulated progress or fake integrations.

## Handoff

- Update `docs/implementation/STATUS.md` after meaningful progress and before ending a session: exact next action, completed acceptance IDs, tests, failures, versions, artifact paths and blockers.
- Put current decisions in `docs/decisions/USER_DECISIONS.md`; preserve historical evidence rather than silently changing the meaning of earlier research.
- A context limit is not completion. Resume from STATUS; do not repeat finished work or reopen settled questions without new evidence.
