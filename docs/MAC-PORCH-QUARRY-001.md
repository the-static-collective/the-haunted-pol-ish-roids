# MAC-PORCH-QUARRY-001 — A local macOS host for Photo Quarry

**Date:** 2026-11-02  
**Status:** Prototype adapter, **not physically verified on a macOS host**.  
**Owner of photo semantics:** Photo Quarry.  
**Receiver of proposed EAT artifacts:** Haunted Pol-ish-roids.  
**Companion contract:** [CANON-QUARRY-POLAROID-001](CANON-QUARRY-POLAROID-001.md).

## Purpose

An intentionally narrow host adapter lets a Mac user ingest an existing JPEG/RAW archive and curate photographs without typing commands, while preserving the original Photo Quarry → Haunted Polaroid → World → Press authority boundaries.

The adapter is distributed as a ZIP with an executable `START PHOTO QUARRY.command`, which installs beside an existing STATIC Mac workspace. It **does not** overwrite the STATIC Mac House launcher or replace macOS.

## Host boundary / explicit actions

1. Human double-clicks the launcher. The installer copies program code to `~/static/apps/photo-quarry`, preserves the data directory `~/static/data/photo-quarry`, and uses a separate Python virtual environment in `~/static/.venvs/photo-quarry`.
2. The local browser porch binds only to `127.0.0.1`, preferring port 8765 (then 8766/8767). Fixed action requests require a per-session token and same-origin checks.
3. **Choose folder / first 100** requests a directory using macOS's native folder picker, then invokes Photo Quarry's existing incremental scan. A separate explicit action scans the entire selected source. This is not an automatic drive crawl.
4. The human reviews thumbnails, grades images, and marks selected candidates as shortlist or ready. Existing Photo Quarry rights and privacy review boundaries remain intact.
5. **Make contact sheets**, **Export review queues**, and **Prepare 30-photo handoff** are fixed local actions with output in the work directory. The handoff is `photo-quarry-handoff/v1`, with canonical image digest identities, previews, a private World candidate graph and a proposal for EAT ingress.
6. Commercial publication remains separately and explicitly authorized per image and use; an exported handoff is **not** a camera-rendering result, an admitted World location, or a published Lemon Press product.

## Invariants

- The local archive is never moved, renamed, deleted, modified, or uploaded as part of the host workflow.
- JPEG/RAW originals remain outside the application's managed data directory.
- Human folder selection is required. The browser cannot supply arbitrary shell commands or filesystem paths.
- Original files are not included in the 30-image handoff by default; only small local previews, metadata, and source identities. An EAT receiver must verify its source bytes before creating descendants.
- One local task runs at a time; results are kept locally; reviews survive rescans.
- The scanner has no authority to mark an image commercially cleared, admit a world relation, render a haunted image, or publish a listing.
- A newer host adapter must not silently grant capabilities to the independent camera, world, or press.

## Implementation / maturity receipt

- Mac adapter source is delivered in a user-side ZIP. The launch script is Bash 3.2 compatible (macOS Mojave), and uses a Python 3.10–3.13 runtime. A Python 3.11 installer from python.org and a pinned Pillow 10.4.0 wheel are compatible installation candidates for older Intel macOS, subject to actual machine verification.
- On November 2, 2026, **five** Photo Quarry tests and **two** Mac Porch HTTP/security/scan/handoff tests passed in the working container. Shell and Python syntax checks also passed.
- The installed STATIC Mac v1.1 source bundle was not present in this execution context; this is a **separate adjacent launcher**, not an asserted built-in House tile.
- **Not verified:** Finder double-click Gatekeeper behavior, AppleScript folder chooser permissions, installation on macOS Mojave, local TLS/PyPI connectivity, actual external-drive indexing, live Haunted Polaroid six-up rendering, World traversal, or Lemon Press publication.
- The next field gate is one local Finder-driven 100-JPEG scan on the user's Mac, review of a few photographs, and one 30-photo private manifest after deliberate shortlisting.

**Promotion rule:** do not call this a proven macOS integration until a Mac-generated test receipt is inspected. Do not call a portable manifest a deployed camera or storefront.
