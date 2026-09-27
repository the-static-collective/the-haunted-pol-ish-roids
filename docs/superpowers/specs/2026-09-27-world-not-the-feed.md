# THE WORLD, NOT THE FEED — Haunted Pol-ish-roids Expansion

Date: 2026-09-27  
Status: proposed product expansion / branch experiment  
Repository: `the-static-collective/the-haunted-pol-ish-roids`

## 1. Thesis

Instagram and similar systems treat the photograph as the finished unit of publication.

Haunted Pol-ish-roids should be able to treat a photograph as a **door**.

A source image is still admitted through the existing canonical `SourceWitness` boundary. Nothing in this expansion weakens the existing law that provenance may not lie. The new layer begins *after* admission and development: accumulated photographs, sounds, text, people, places, recurring objects, and human contributions may form an explorable relational world.

The product direction is:

> **THE WORLD, NOT THE FEED.**

The system should not become a better infinite scroll. It should make the feed feel like a lossy projection of something richer.

## 2. Product inversion

Conventional social-photo systems commonly collapse lived material into:

```text
post
  ↓
feed
  ↓
reaction
  ↓
engagement score
  ↓
replacement by newer post
```

This expansion proposes:

```text
witness
  ↓
relations
  ↓
place / person / object / era / event
  ↓
door
  ↓
exploration
  ↓
contribution
  ↓
new relation
  ↺
```

The photograph is not the end product. It is an entrance into a world that can continue to acquire structure.

## 3. Governing laws

### 3.1 No feed as the primary ontology

A chronological feed may exist later as a convenience projection, but it must not be the fundamental model.

The primary model is relational:

- people;
- places;
- objects;
- events;
- eras;
- journeys;
- media;
- contributions;
- relationships among them.

Navigation should answer questions like:

- What else happened here?
- Where else does this object appear?
- Who was present across this era?
- What sound belongs with this image?
- What did this image later cause someone to make?
- Which memory opens from this one?

### 3.2 A photograph is a door

Every admitted photograph may expose one or more routes into neighboring material.

A door can be weak, uncertain, latent, user-confirmed, machine-proposed, inherited from explicit metadata, or created by another human contribution.

The world must preserve uncertainty. A proposed relation is not silently promoted to fact merely because a model found resemblance.

### 3.3 Source witness remains sacred

The world layer may organize, transform, narrate, and connect admitted material.

It may not rewrite:

- which source asset was admitted;
- whether it was captured or imported;
- original timestamps or metadata;
- provenance receipts;
- human-authored claims;
- lineage events.

Interpretive world structure and canonical witness remain distinct layers.

### 3.4 Profiles become worlds

A person's public or private surface should be able to become an explorable accumulated world rather than a thumbnail grid.

The identity surface emerges from what has been:

- witnessed;
- made;
- revisited;
- contributed;
- connected;
- maintained;
- deliberately withheld.

Follower count is not identity.

### 3.5 Reactions become verbs

The product should privilege consequential actions over low-information reaction counters.

Candidate verbs include:

- SAVE
- SAMPLE
- ANSWER
- LOCATE
- SING
- ANNOTATE
- CONTINUE
- CONTRADICT
- HAUNT
- CONNECT
- REMEMBER

A low-friction lightweight reaction may still exist, but it should not become the principal social grammar.

### 3.6 Contributions grow objects

Comments should be able to become first-class material.

A contribution may be:

- text;
- image;
- audio;
- video;
- location;
- relation proposal;
- annotation;
- alternate witness;
- derivative artifact.

A contribution does not overwrite the original object. It extends the local world around it.

### 3.7 Old material may become newly alive

Recency is not authority.

A ten-year-old photograph may become newly relevant because:

- the same object reappears;
- a person returns to the same place;
- another contributor adds a related witness;
- a song references it;
- a later event changes its meaning;
- a relation is newly discovered.

The system should support resurfacing through relation, not merely through anniversaries or engagement optimization.

### 3.8 Camera equals world ingestion

Capture is not merely publishing.

A fresh camera event can become new world material immediately after its canonical witness is sealed.

Imported material enters the same world boundary.

### 3.9 The system may eat legacy social archives

A user-authorized archive from Instagram or another service may be ingested as historical material.

The goal is not to clone the old profile.

The goal is to metabolize the archive into candidate structure such as:

```text
people
places
eras
recurring objects
journeys
relationships
sounds
visual motifs
unfinished threads
```

Import must use material the user is authorized to provide. The system should not depend on bypassing platform access controls.

### 3.10 No engagement sovereign

Ranking for exploration must not silently collapse into "maximize time on app."

Any ranking or path-selection mechanism must remain subordinate to declared product purposes such as:

- relevance to the current object;
- user-selected curiosity;
- temporal continuity;
- spatial continuity;
- explicit relation strength;
- novelty;
- unfinished threads;
- human-maintained importance.

## 4. Relationship to the living camera

This expansion does not replace the Haunted Polaroid organism.

The living camera continues to own:

- source admission;
- six-up development;
- residue;
- mood;
- identity;
- KEEP / COMPOST / HAUNT;
- Burn / Phoenix Egg;
- Chrysalis;
- camera lineage.

The world layer owns:

- relational organization of admitted and contributed material;
- explorable paths among world nodes;
- contribution surfaces;
- world projections;
- archive digestion into candidate relations.

A useful boundary is:

```text
CAMERA ORGANISM
capture / import
    ↓
SourceWitness
    ↓
development / disposition / living state
    ↓
admitted artifacts
    ↓

WORLD LAYER
nodes
    ↓
relations
    ↓
doors
    ↓
exploration
    ↓
contribution
    ↓
new nodes / relation proposals
```

The world layer may observe camera state projections where explicitly allowed, but it must not become the hidden authority over camera identity.

## 5. Candidate records

### 5.1 `WorldNode`

```text
nodeId
kind:
  source | development | person | place | object | event |
  era | journey | sound | text | contribution | collection
canonicalRef?
title?
createdAt
visibility
authorityClass
```

A `WorldNode` may refer to a canonical witness, but not every node is itself canonical evidence.

### 5.2 `RelationEdge`

```text
edgeId
fromNodeId
toNodeId
relationType
origin:
  explicit | metadata | inferred | contributed
confidence?
assertedBy?
evidenceRefs[]
status:
  proposed | accepted | rejected | held
createdAt
```

Machine inference should normally begin as `proposed`, not `accepted`.

### 5.3 `Contribution`

```text
contributionId
targetNodeId
contributorIdentity
kind
artifactRef
sourceWitnessRef?
createdAt
visibility
relationIntent?
```

Where a contribution is media, it should pass through an appropriate witness boundary rather than existing as an unattributed blob.

### 5.4 `Door`

A Door is a navigable projection, not necessarily a persistent canonical record.

```text
doorId
originNodeId
destinationNodeId
edgeIds[]
presentation
reasonClass
```

A Door answers: "Why can I go there from here?"

### 5.5 `WorldProjection`

```text
projectionId
rootNodeId
viewerContext
selectionPolicy
visibleNodes
visibleEdges
generatedAt
```

A projection is one view of the graph, not the graph itself.

## 6. Import digestion

A legacy photo archive should pass through staged digestion.

### Stage A — admit

Preserve each authorized imported asset as a source witness with digest and original metadata where available.

### Stage B — extract candidates

Generate non-authoritative candidate features:

- timestamps;
- coarse location;
- face clusters where explicitly allowed;
- recurring objects;
- visual motifs;
- text/caption references;
- audio associations;
- album/sequence adjacency.

### Stage C — propose relations

Build candidate relation edges without silently claiming certainty.

Examples:

- same-place candidate;
- same-person candidate;
- same-object candidate;
- near-in-time;
- repeated visual motif;
- likely trip;
- possible event sequence.

### Stage D — human settlement

Allow the human to accept, reject, hold, merge, split, or rename candidate structures.

### Stage E — inhabit

Generate an explorable world projection from the settled and still-provisional graph.

## 7. First executable slice — THIRTY PHOTOGRAPHS BECOME SOMEWHERE

The first proof should be intentionally small.

### Input

A folder of approximately 30 photographs.

### Required behavior

1. Admit all 30 through immutable source-witness records.
2. Extract simple candidate relations from available metadata and visual analysis.
3. Produce an explorable node/edge world.
4. Let the human enter one photograph.
5. Show at least two meaningful relational doors when evidence permits.
6. Follow a door into another photograph or discovered entity.
7. Permit one text, audio, or image contribution.
8. Make that contribution create or alter at least one navigable path.
9. Preserve the difference between:
   - source fact;
   - machine inference;
   - human assertion;
   - creative transformation.
10. Export a receipt for the resulting world graph.

### Success condition

A human should be able to drop in thirty ordinary photographs and experience the result as **somewhere**, not as a gallery.

The minimum magic test is:

> I entered one photograph, followed a relation I had not manually arranged, added something of my own, and the available world changed without the system pretending its guesses were facts.

## 8. Kindtroll surface — EMBARRASS THE RECTANGLE

The world layer should be able to travel back through conventional scroll surfaces without becoming one.

The posture is not hostility toward people who scroll, creators who use feeds, or the platforms themselves. The joke is representational: let the flattened post advertise the existence of a richer object behind it.

Governing law:

> **Never shame the scroller. Embarrass the rectangle.**

Candidate mechanics:

### 8.1 Anti-Carousel

A conventional carousel may begin like an ordinary post, then reveal that the photograph has somewhere to go.

Example progression:

```text
frame 1: photograph
frame 2: this photograph has somewhere to go
frame 3: one visible relation / door
frame 4: flattened world map or invitation into the living object
```

The export is a projection, not the canonical world.

### 8.2 Infinite Scroll Has an Ending

Some exported artifacts should terminate deliberately.

The product may say, in effect:

> You reached the end. Go make something, go somewhere, or enter the photograph.

Completion is allowed to feel better than retention.

### 8.3 Dead Comment Resurrection

Low-information reactions such as hearts, fire, applause, or "nice" may be playfully reinterpreted as invitations to act:

```text
LIKE      → SAVE / CONNECT
🔥         → SAMPLE / HAUNT
COMMENT   → ANSWER / ANNOTATE
TAG       → LOCATE / RELATE
SHARE     → CONTINUE / CARRY
```

This is not a judgment on the person who reacted. It reveals how little expressive bandwidth the old grammar gave them.

### 8.4 Feed Fossils

Imported legacy posts may preserve their old social metadata as archaeological context while the photograph acquires new relations.

Old captions, timestamps, and user-authorized reaction counts may appear as a fossil layer beneath the living object.

The fossil may be displayed; it may not become the governing importance score for the new world.

### 8.5 Scroll Receipt

After a bounded exploration, the system may summarize traversal in world terms rather than engagement terms.

Example:

> You did not view 10 posts. You crossed 4 places, 3 years, 2 people, and one recurring object.

The receipt should derive from actual traversed nodes and edges rather than inventing narrative coherence.

### 8.6 Reward Leaving

The system is permitted to have no next thing.

A world may explicitly end a session with:

> There is nothing else here for you today.

The absence of another engagement unit is not a product failure.

### 8.7 Posts That Escape

Exports to conventional feeds may carry a small, recognizable marker that indicates the artifact is only a flattened projection of a larger living object.

The export should still stand on its own. It should not degrade into spam, bait, or an unusable advertisement.

### 8.8 Thirty-Photo Challenge

A public invitation may compress the first executable proof into a simple promise:

> Give it 30 forgotten photographs. See whether they become somewhere.

This is a product demonstration, not a demand that the user abandon another service.

### 8.9 Last Post ritual

A person may deliberately mark a conventional social post as a final flattened post while allowing the underlying world to keep growing elsewhere.

This is an optional human ritual, not a platform-war mechanic.

The conceptual move is:

```text
LAST POST
   ↓
not disappearance
   ↓
migration from timeline
   ↓
into inhabitable world
```

### 8.10 Kindtroll safety boundary

Kindtrolling must not become:

- harassment;
- brigading;
- unsolicited mass posting;
- deceptive links;
- impersonation;
- platform sabotage;
- manipulation of ranking systems;
- attempts to make another person's experience worse;
- shame aimed at people for using scroll-based products.

The strongest troll is the product comparison itself.

Let the user experience:

```text
post → post → post → post
```

and then:

```text
photograph
  → person
  → place
  → song
  → year
  → another witness
  → recurring object
  → contribution
  → new door
```

The world should win by being more expressive.

## 9. Explicit non-goals for the first slice

- infinite scrolling;
- follower mechanics;
- public popularity ranking;
- engagement optimization;
- attempting to reconstruct a complete biography;
- claiming face identity without human confirmation;
- automatically publishing private imported archives;
- cloning Instagram UI;
- replacing the existing six-up camera loop;
- letting inferred relations mutate canonical provenance.

## 10. Cross-project seams

This expansion has natural compatibility with neighboring Static Collective work, but those projects do not silently gain authority here.

Potential imports:

- **MEMENTO** — inhabitable memory and relationship-unlocked affordances;
- **Visual Dreaming** — graph traversal as visual discovery;
- **Door Instrument** — doors whose openness can vary continuously;
- **WITNESS** — multiple humans contributing to a living corpus;
- **Pantry** — media ingestion and asset digestion;
- **Haunted Blender** — derivative media and mutation;
- **3rdi** — occurrence, availability, attention, and known-at remain distinct;
- **Dogram** — explicit relational structure and path semantics;
- **Static Live** — presence as a live world event;
- **GOATnote** — identity-carry notes and durable human context;
- **Workbench** — creation surfaces and composition tools;
- **Full Measure** — world-layer interaction.

Each seam should be imported as a capability or law with provenance, not as automatic canon.

## 11. Strategic test

The product is on the right path when importing a legacy social-photo archive does **not** make the user say:

> Here is my old profile again.

It should make the user say something closer to:

> I thought that service had my photographs. This thing exposed relationships among parts of my life that the grid could never express.

That is the target.

The competitive move is not to attack a feed directly.

It is to build a richer representational object until the feed becomes visibly inadequate.
