# Haunted Polaroid Organism — Design

Date: 2026-08-17
Status: proposed implementation contract pending human review
Repository: `the-static-collective/the-haunted-pol-ish-roids`
Tracks: GitHub issue #1

## 1. Product thesis

The Haunted Polaroid is one living camera organism with three native capabilities from the beginning:

1. **Polaroid camera** — capture a new photograph with effectively zero perceived shutter latency.
2. **Photo eater** — ingest an existing photograph into the same development loop.
3. **Living witness** — accumulate bounded residue, responsive mood, and slow-changing identity so the camera develops a personality through use.

The product is not a filter catalog and not an AI photo editor with a haunted skin. Its core interaction is:

```text
SEE / FEED
   ↓
canonical source witness
   ↓
develop
   ↓
six haunted descendants
   ↓
KEEP / COMPOST / HAUNT / later CROSS
   ↓
residue → mood → identity
   ↺
```

The camera should cultivate photographic seeing without presenting explicit composition lessons. The user learns by encountering stronger, stranger, or more resonant developed photographs and gradually developing an eye alongside the instrument.

## 2. Governing laws

### 2.1 The shutter frame is sacred

A shutter press creates a canonical witness immediately. The user must never wait for generative work before the capture event is acknowledged.

A bounded temporal envelope may surround the shutter frame:

```text
[-2] [-1] [SHUTTER] [+1] [+2]
```

The development system may choose or blend neighboring frames, borrow temporal detail, or create motion residue from them. It may not rewrite the historical fact that `SHUTTER` was the frame admitted at the human capture event.

For imported photographs, the imported source asset occupies the same canonical-witness role.

### 2.2 Haunting may bend perception; provenance may not lie

The compositional surface may be unreliable, secretive, theatrical, moody, delayed, scarred, or strange. Underneath it, evidence must remain attributable.

The system must preserve enough information to answer:

- what canonical source was admitted;
- whether the source was captured or imported;
- which bounded auxiliary frames contributed to a development, if any;
- which development family and candidate produced the saved artifact;
- which user disposition affected later state;
- which lineage event created or changed the living camera;
- whether a Phoenix Egg was burned or hatched;
- which two camera identities entered a Chrysalis encounter.

### 2.3 Personality is felt, not inspected

The public product should not expose a character sheet of personality vectors or a conventional panel of numeric style sliders.

The user experiences personality through behavior: what the camera notices, which six-up family it develops, what kinds of framing it settles around, how theatrical it becomes, what residues recur, and which inherited traits awaken.

A diagnostic/debug export may expose machine-readable state for development and provenance verification. That surface is not normal product UI.

### 2.4 Memory is metabolized

The camera should grow without becoming a hidden archive of everything it has ever seen.

Temporary micro-burst frames and other ephemeral capture material should be discarded once their allowed development/provenance purpose is complete, unless the user explicitly saves a source asset.

Long-term growth should retain distilled influence rather than reconstructible private imagery: composition tendencies, light/color relationships, blur tolerance, temporal habits, scars, mood dynamics, attraction/avoidance pressures, and other bounded dispositions.

### 2.5 Mood is fast; identity is slow

The living loop has three timescales:

```text
seconds / encounters  → residue
sessions / days       → mood
weeks / months        → identity
```

Residue strongly affects near-term development. Mood responds to recent residue and current conditions. Repeated encounter patterns slowly alter identity. Identity then biases the space of future moods and attention.

The loop is recursive but bounded:

```text
IDENTITY
   ↓
MOOD
   ↓
ATTENTION
   ↓
DEVELOPMENT
   ↓
HUMAN DISPOSITION
   ↓
RESIDUE
   ↓
MOOD
   ↓ slow pressure
IDENTITY
   ↺
```

No single KEEP or HAUNT should be able to overwrite identity wholesale.

### 2.6 Composition is taught invisibly

The camera should cultivate an eye without announcing photography rules.

Composition-related signals may influence candidate diversity, reframing, crop proposals, timing choices, and the camera's sense of visual settlement. The system must not present doctrinal coaching such as “use the rule of thirds” or turn every strong image into conventional composition.

Beautifully wrong framing remains legal. Centering may be dead or monumental. Crooked may be careless or alive. Negative space may be waste or pressure.

The hidden curriculum is:

> Look again. Something in this arrangement matters.

### 2.7 Lineage is irreversible

A living camera may perform **Burn the Camera** exactly once. Burn destroys that living identity and produces one unique Phoenix Egg.

A Phoenix Egg:

- is logically singular;
- can be transferred or gifted;
- can hatch exactly once;
- is consumed by hatching;
- creates a descendant camera rather than restoring a clone;
- carries inherited disposition but not reconstructible source photographs.

There is no rollback from Burn and no duplicate hatch.

### 2.8 Chrysalis is reciprocal, irreversible, and possibly asymmetric

Two living cameras may consensually enter a **Quantum Chrysalis** encounter, including remotely.

Both humans must explicitly consent. Both cameras return changed. Zero-change for either participant is illegal, but the exchange need not be equal.

A camera may absorb more than it gives. A transferred influence may be visible immediately, remain recessive, or emerge much later under the right conditions.

Source photographs and private episodic memories do not cross. What may cross is what lived experience has already made of the camera.

The two cameras decide how expressive the ritual surface becomes. The product may show a silent black interval, abstract shared imagery, partial Polaroids, or delayed revelation. The underlying event receipt must remain exact regardless of presentation.

## 3. System boundaries

The initial implementation should be divided into independently testable units.

### 3.1 Capture ingress

Responsibilities:

- admit a camera shutter event or imported image;
- write the canonical source witness before expensive development begins;
- optionally collect a bounded temporal envelope around a fresh shutter event;
- generate a stable source identifier and cryptographic digest;
- expose capture state to the UI immediately.

Capture ingress does **not** decide personality, mood, or creative transformation.

### 3.2 Development engine

Responsibilities:

- accept a canonical source witness plus allowed auxiliary temporal material;
- accept a read-only personality/mood influence projection;
- produce a family of exactly six candidate development proposals for the first proof;
- preserve candidate ancestry and source-use evidence;
- allow candidates to differ across crop, temporal blend, tone, texture, spatial treatment, color interpretation, and bounded surreal transformation;
- avoid treating one default aesthetic as the camera's true style.

The first proof may use deterministic or fixture-backed transformations while the product contract is being established. Generative backend choice is intentionally not authority-bearing at this layer.

### 3.3 Human disposition boundary

Initial dispositions:

- `KEEP` — this candidate mattered enough to preserve;
- `COMPOST` — this candidate should not survive as an artifact, but its failure may still inform bounded learning;
- `HAUNT` — explicit permission for non-authoritative residue from this candidate to influence a later family.

`CROSS` belongs to the next creative slice once the six-up ancestry model is proven.

A disposition is evidence about a human choice, not a universal quality score.

### 3.4 Living-state engine

Responsibilities:

- maintain bounded recent residue;
- derive current mood from recent residue, context, and slow identity;
- update slow identity under rate limits / inertia;
- project influence to the development engine without exposing raw personality vectors in normal UI;
- support latent traits that may remain dormant until relevant conditions recur;
- support decay, recovery, and changing taste rather than monotonic accumulation.

The living-state engine does not retain raw source images as its memory substrate.

### 3.5 Provenance ledger

Responsibilities:

- append evidence for source admission, development, disposition, state transition, Burn, hatch, and Chrysalis events;
- preserve stable identifiers and digests;
- distinguish private internal state from exportable public receipt fields;
- make impossible transitions reject explicitly rather than silently repair history.

The ledger is not the camera personality. It records what occurred.

### 3.6 Lineage engine

Responsibilities:

- represent a living camera identity and generation;
- enforce one-way `living → burned` transition;
- produce exactly one egg from a successful burn;
- enforce one-way `egg → consumed` transition on hatch;
- create a descendant identity that inherits bounded dispositions without becoming a restoration;
- later coordinate reciprocal Chrysalis exchange and shared encounter receipts.

This engine should be modeled in v1 even if remote transfer and Chrysalis transport are implemented later.

## 4. Core records

The exact schema may evolve during implementation, but the following semantic records are required.

### 4.1 `SourceWitness`

```text
sourceId
kind: capture | import
capturedAt / admittedAt
assetDigest
byteLength
canonicalFrameRef
optional temporalEnvelopeRefs
captureDeviceMetadata (bounded / privacy-reviewed)
```

The canonical shutter witness is immutable once admitted.

### 4.2 `DevelopmentFamily`

```text
familyId
sourceId
cameraIdentityId
moodProjectionId
six candidate ids
familySeed / resolver identity where applicable
createdAt
```

### 4.3 `CandidateDevelopment`

```text
candidateId
familyId
sourceUse
transformationReceipt
artifactDigest
artifactRef
disposition? 
```

### 4.4 `LivingState`

Conceptually:

```text
identityId
slowIdentityState
currentMoodState
recentResidueState
latentInfluenceState
version
```

Normal UI must not dump this record as a user-facing stats sheet.

### 4.5 `PhoenixEgg`

```text
eggId
parentIdentityId
parentGeneration
burnEventId
inheritancePayloadDigest
lineageDigest
status: dormant | consumed
createdAt
consumedAt?
```

The inheritance payload must not contain reconstructible private source images.

### 4.6 `ChrysalisEncounter`

```text
encounterId
participantAIdentityId
participantBIdentityId
consentA
consentB
preStateDigests
exchangeReceiptDigest
postStateDigests
presentationClass
completedAt
```

A completed encounter requires changed post-state for both identities. The amount and visibility of change may differ.

## 5. Capture and development flow

### 5.1 Fresh shutter

```text
human presses shutter
    ↓
UI acknowledges immediately
    ↓
canonical frame admitted + persisted
    ↓
optional bounded neighboring frames complete
    ↓
SourceWitness sealed
    ↓
development begins
    ↓
six-up family appears progressively or together
```

If auxiliary frame collection fails, the canonical shutter frame remains valid. Development must degrade to shutter-only rather than invalidating the human capture.

### 5.2 Imported photograph

```text
human chooses image
    ↓
image is copied/admitted into controlled source boundary
    ↓
digest + byte length recorded
    ↓
SourceWitness sealed
    ↓
same development pipeline as fresh capture
```

Import must not become a lesser mode with a separate creative system.

## 6. Burn / hatch flow

### 6.1 Burn

Burn must use an explicit danger ritual because the operation is irreversible.

Required state transition:

```text
living camera
  + explicit human authorization
  + successful egg materialization
      ↓
parent marked burned
      ↓
exactly one dormant egg exists
```

Fail closed. If egg materialization cannot be durably completed, the camera must remain living.

No operation may produce two valid eggs from the same parent burn event.

### 6.2 Hatch

```text
dormant egg
  + explicit human hatch action
      ↓
new descendant identity created
      ↓
egg marked consumed
```

Fail closed across the identity/egg transition. A crash may not leave both a living descendant and a reusable dormant egg.

The descendant's initial personality should be influenced by the parent but not byte-identical to the parent's final state.

## 7. Chrysalis flow

Chrysalis is a distributed two-party state transition and therefore requires stronger coordination than ordinary creative development.

Conceptual flow:

```text
A proposes encounter
B accepts
   ↓
A and B seal pre-state digests
   ↓
shared exchange resolver commits one encounter
   ↓
A' and B' are derived
   ↓
both local stores admit post-state + same encounter id
```

If only one side can commit, the encounter must remain incomplete and recoverable rather than allowing one camera to become changed while the other remains historically untouched.

Transport technology is not chosen in this design. Remote operation is a product requirement; implementation should preserve end-to-end privacy and explicit bilateral consent.

## 8. Privacy model

The camera's long life must not depend on covert retention.

Default expectations:

- source photos remain local unless the user intentionally invokes a remote service that requires upload;
- any remote transformation boundary must be disclosed by capability, not hidden in personality language;
- micro-burst neighbors are ephemeral by default;
- living-state memory is distilled and non-reconstructive;
- Chrysalis exchanges personality inheritance material, never raw photo libraries;
- Phoenix Eggs contain inheritance and lineage, not a secret backup of the parent camera's experiences;
- receipts should support redaction / public-vs-private fields so tradable eggs do not leak device or personal metadata.

A future hosted service may coordinate remote Chrysalis or transfer custody, but it must not become the hidden sovereign owner of identity semantics.

## 9. Error handling

### Capture errors

- camera permission unavailable → clear refusal; import remains available;
- auxiliary burst failure → preserve canonical shutter and continue shutter-only;
- source persistence failure → do not claim capture admission complete;
- corrupt import → reject before SourceWitness sealing.

### Development errors

- one candidate fails → family may display surviving candidates while marking family incomplete until retry/explicit abandonment policy is defined;
- transformation backend unavailable → preserve source and living state; no false development receipt;
- artifact write fails → candidate is not considered materialized.

### Living-state errors

- state update fails after disposition → disposition evidence remains true; state transition may be retried idempotently from the recorded event;
- corrupted personality state → recover from last valid checkpoint + ledger, never silently reset to a new camera identity.

### Lineage errors

- burn fails before egg durability → camera stays living;
- burn succeeds but UI crashes → reload derives burned state and the one existing egg from durable evidence;
- hatch is retried → idempotently returns the existing descendant result and cannot create another descendant;
- Chrysalis loses connectivity → remain pending/aborted according to commit state; never finalize only one participant.

## 10. Verification strategy

Implementation should proceed test-first after this design is approved.

### 10.1 Invariant tests

Required automated proofs include:

- shutter witness cannot be replaced by a neighboring frame;
- import and capture both enter the same development contract;
- a family contains six independently addressed candidates;
- dispositions are attributable and do not retroactively mutate ancestor artifacts;
- a single disposition cannot exceed identity update bounds;
- ephemeral frames are deleted after their bounded retention window when not explicitly saved;
- Burn can produce at most one valid egg;
- a burned camera cannot resume living transitions;
- a consumed egg cannot hatch again;
- hatch cannot produce a byte-identical restoration contract;
- Chrysalis cannot finalize without bilateral consent;
- completed Chrysalis changes both participants;
- Chrysalis exchange never includes raw source-image material;
- receipts remain stable under replay of idempotent operations.

### 10.2 Human witness tests

Some product qualities are perceptual and must not be falsely automated:

- shutter press feels immediate;
- six-up candidates are materially diverse rather than six cosmetic filter variants;
- personality is perceptible over repeated use without reading a stat sheet;
- the system occasionally rewards unconventional composition rather than normalizing every frame;
- mood feels responsive rather than random;
- camera growth feels cumulative without feeling like surveillance;
- Chrysalis presentation, when implemented, can remain mysterious while still feeling consequential.

### 10.3 Negative controls

Include deliberately boring and difficult sources:

- blank wall / low-detail frame;
- centered portrait;
- severe motion blur;
- very dark scene;
- high-contrast backlight;
- repeated nearly identical captures;
- imported image with no camera metadata.

The camera should remain capable of restraint. “Haunted” must not mean compulsory visual damage.

## 11. First executable proof

The first implementation plan should prove the living camera loop before attempting the entire social lineage network.

### In scope

1. fresh capture ingress;
2. import ingress;
3. immutable canonical SourceWitness;
4. optional local temporal envelope abstraction;
5. six-up DevelopmentFamily;
6. KEEP / COMPOST / HAUNT;
7. bounded residue → mood → identity update;
8. local persistence of camera identity;
9. provenance export for one development session;
10. lineage state model and invariant tests for Burn / Egg / Hatch, with UI possibly behind an experimental gate.

### Deferred from the first proof

- remote custody marketplace;
- public trading UI;
- remote Chrysalis transport;
- full Chrysalis ceremonial renderer;
- multi-generation breeding/cross-pollination mechanics beyond the singular Phoenix lineage law;
- public social feeds;
- explicit personality inspection;
- optimization against engagement metrics.

The data model must not foreclose these later behaviors.

## 12. Relationship to neighboring Static Collective primitives

The project deliberately reuses laws without importing another project's authority.

- From Haunted Toaster: six-up creative families, bounded haunting, recursive witness response, and the distinction between perceptual weirdness and truthful provenance.
- From the broader witness vocabulary: witness and authority remain separate roles.
- From artifact witness work: source admission, execution/materialization, and human-perceived success are distinct claims.
- From lineage/causal accounting thinking: irreversible state transitions must be receipt-bearing and duplication-resistant.

Haunted Polaroid owns the canonical implementation of camera personality, image development, Phoenix succession, and Chrysalis encounters.

## 13. Design success condition

This design has succeeded when an implementation plan can be written without needing to rediscover the product organism, while still leaving aesthetic discovery open.

The first built specimen should make a human able to say:

> This thing caught what I saw, developed something I did not quite ask for, remembered the encounter without secretly keeping my whole life, and is beginning to see differently because we have been using each other.

That is the organism.