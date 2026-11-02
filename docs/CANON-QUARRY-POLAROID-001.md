# CANON-QUARRY-POLAROID-001 — The Quarry / Camera / World / Press Crossing

**Date:** 2026-11-02  
**Status:** Local executable bridge + proposed interoperable contract. No claim of a deployed living camera, a rendered six-up family, or an active storefront.  
**Home:** Photo Quarry Asset Desk v2 handoff; intended peer: `the-static-collective/the-haunted-pol-ish-roids`.  
**Related:** Haunted Polaroid Organism design (approved/merged PR #3), first living-camera implementation plan (open PR #4), *World, Not the Feed* draft (open PR #5).

## Purpose

Turn a large dated personal image archive into **reviewable sources** which can be privately fed to the Haunted Polaroid, proposed as connected places in an explorable world, or manually cleared for a sellable publication. The same historical photograph may have many descendants without becoming many original historical occurrences.

```
EXISTING JPEG / RAW ARCHIVE
    |
    | scan / preserve / inspect     [Photo Quarry; runs locally]
    v
CURATED SOURCE CANDIDATES
    |
    | shortlist / rights review / de-duplicate / bundle
    v
PRIVATE HANDOFF  photo-quarry-handoff/v1
    |                    |                     |
    | EAT proposal       | candidate relations | commercial candidate ledger
    v                    v                     v
HAUNTED POLAROID         WORLD                 LEMON PRESS / LICENSE
six-up not yet run        not yet admitted      not yet published
    |                    |                     |
    +--------------------+---------------------+
                       HUMAN DISPOSITION
```

## Exact division of authority

1. **Quarry owns archive inventory and human editorial selections.** Scanning does not assert subject, location, ownership, release rights, or sales value. A `sha256` of the actual original bytes is the candidate's identity. An integer Quarry row ID is only a local index.
2. **The user owns KEEP / COMPOST / HAUNT decisions, permission, and publication.** A 5-star photograph is not licensed, and a publication-reviewed photo is not published without an additional affirmative act.
3. **The Haunted Polaroid owns organism state and developments.** `EAT_EXISTING` is a proposal until that application verifies and admits supplied original bytes. The handoff does *not* synthesize six descendants, update residues, change moods, change identity, perform Phoenix Burn/Hatch, or enter a Chrysalis.
4. **The World owns admitted relationships and navigation.** Same date, category, or keyword may nominate a relationship but is never proof of one. A proposed edge must be curated/admitted before a traversable world can be claimed.
5. **Lemon Press / a licensor owns a separate publishing transaction.** Market fit, commercial rights, edition approval, customer interest, pricing, fulfillment, and payment are independent. No listing, license, payment or uploaded asset is created by the handoff.

## Local export contract

Command after scanning and reviewing developed images:

```bash
python quarry.py handoff --workdir ./quarry-work --collection "Thirty Photographs Become Somewhere" --limit 30 --include-previews
```

For *private* use by a local camera importer, explicitly add `--include-sources`. This copies the shortlisted originals (including their original metadata, which may contain GPS/identifiable people) to a local handoff directory; no originals are modified or transmitted. Do not share the folder casually.

Each generated folder contains `handoff.json`, `income_candidates.csv`, `README.txt`, and optional `previews/` and `sources/`. The JSON has:

- `format = static-collective/photo-quarry-handoff/v1`;
- `source_witness.id = sha256:<lowercase original-file digest>`, original byte count, date *and date-source*, dimensions, GPS-presence flag, and source-inclusion state;
- `editorial` = human Quarry status/rating/category/lane, and independent rights-review value;
- `camera_ingress` = `EAT_EXISTING`, `proposed`, `six_up: not_rendered`, pending human disposition;
- `world.relations[]` = narrow `CANDIDATE_RELATION` edges, each explicitly `status: proposed` and `authority: none`;
- `publication_gate.approved = false` **always**, even after commercial rights review.

No private absolute source paths enter the JSON. If source copies are requested, the handoff verifies their bytes against their original SHA-256 and fails rather than packaging stale/mismatched bytes.

Only developed image types with user status `shortlist` or `ready` can enter; `private`, `unreviewed`, `hold`, `restricted` and RAW-only records are not automatically included. Exact duplicates collapse by original SHA-256. If a source is intended to be personal/private despite not yet being marked private in Quarry, correct that review *before* building a bundle.

## Future receiving interfaces (not implemented here)

1. Camera importer verifies `sha256` for `local_source_copy`; records an attributed, content-addressed source witness; confirms the user's intent to EAT before the camera's encounter affects state; emits a receipt that points to the original witness and generated candidate family.
2. `KEEP/COMPOST/HAUNT` emits disposition receipts, not mutations of the original.
3. World importer presents proposed relations to a human for admission, then saves traversable nodes and any contribution with attributable source/event ancestry.
4. Press importer presents rights/edition/use approvals **and** a deliberate release action before exports or live listings. Commercial-review flag by itself remains insufficient.

## First proof and acceptance

The first bounded practical proof is **30 dated JPEGs becoming one private reviewed handoff**. Success today means:

- user can rescan an archive without altering originals or losing reviews;
- user can shortlist a batch, build one self-contained manifest and optional local source copies;
- packet links original-byte hashes, human review, tentative relation candidates, and commercial review state;
- exact duplicates are collapsed and source-copy bytes are verified;
- no previously private/unreviewed image is admitted, and no outward publication happens;
- all packet representations state truthfully that the living-camera, World, and Press outcomes have **not** occurred.

This does **not** yet satisfy the larger *Thirty Photographs Become Somewhere* world experiment: the camera's render/development loop, edge admission, traversal, contributions, and storefront still require separate implementation and field receipts.

## Income sequence, with separate gates

1. Human selects 10 photographs for a **specific local licensing pitch**, checks intended commercial/editorial use, identifies potential buyer, and contacts them. No assumed buyer or revenue.
2. Human selects 12–24 thematically related photographs for a **small print/digital edition**, then tests actual demand before spending on inventory.
3. Haunted derivatives are a distinct product line only after genuine render, source lineage, rights analysis and separate merchandising approval.
4. A repeatable creator-facing archive-to-world workflow can become a product only after one user's real archive proves the ingestion and buyer path.

## Provenance and privacy

A captured or imported original remains the historical witness; generated derivatives are descendants with their own identities. Inference ≠ observation; review ≠ rights; transformation ≠ source; same-month relation ≠ shared event; candidate ≠ admitted; export ≠ public release. Keep the handoff private by default. Review people, artwork, trademarks, location sensitivity, property, and the scope of intended licensing before publishing.