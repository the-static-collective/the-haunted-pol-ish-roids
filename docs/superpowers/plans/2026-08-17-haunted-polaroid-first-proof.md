# Haunted Polaroid First Proof Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Build the first local mobile Haunted Polaroid loop: fresh capture or imported photo → immutable source witness → six materially distinct haunted developments → KEEP / COMPOST / HAUNT → bounded residue/mood/identity growth → persistent living camera + exportable receipt, while proving Phoenix Burn/Egg/Hatch invariants without implementing remote Chrysalis transport.

**Architecture:** Expo/React Native owns the mobile encounter surface. Pure TypeScript domain modules own witness, development-family, living-state, and lineage laws; Expo adapters own camera/import, local files, SQLite, Skia rendering, and sharing. The UI consumes domain projections and never gains authority to rewrite witness or lineage history.

**Tech Stack:** Expo SDK 57; React Native 0.86; React 19.2; TypeScript strict; Expo Router; `expo-camera`; `expo-image-picker`; `expo-file-system`; `expo-sqlite`; `expo-crypto`; `expo-sharing`; `@shopify/react-native-skia`; Jest + `jest-expo` + React Native Testing Library.

**Spec:** `docs/superpowers/specs/2026-08-17-haunted-polaroid-organism-design.md`

## Global Constraints

- Fresh capture and imported photographs are equal ingress paths into one development pipeline.
- A shutter press creates the canonical source witness; auxiliary frames may contribute later but may never replace the shutter event.
- User-perceived shutter acknowledgement happens before development work.
- Every first-proof family contains exactly six independently addressed candidate developments.
- Public UI exposes personality through behavior, not raw vectors or numeric personality controls.
- Long-lived memory stores distilled influence, not reconstructible hidden photo history.
- `KEEP`, `COMPOST`, and `HAUNT` are attributable human dispositions, not universal quality labels.
- A single disposition may not rewrite identity wholesale.
- Burn is irreversible and produces at most one valid Phoenix Egg.
- Hatch consumes one egg exactly once and creates a descendant, not a clone.
- Remote Chrysalis transport is explicitly out of first-proof scope.
- No cloud transformation, account system, marketplace, social feed, engagement score, or blockchain dependency in this plan.
- Android and iOS remain supported by the scaffold; the first packaged human field gate may be performed on one physical device before cross-platform polish.
- Use local deterministic rendering for the first proof so creative behavior can be replayed and tested without external model availability.

---

## File map

```text
app/
  _layout.tsx                  Expo Router root
  index.tsx                    capture/import home
  develop/[familyId].tsx       six-up family screen
  camera.tsx                   live camera surface
  about.tsx                    minimal provenance/privacy note

src/domain/
  types.ts                     shared branded domain types
  sourceWitness.ts             immutable witness admission
  livingState.ts               residue → mood → identity transition law
  development.ts               deterministic six-up recipe planning
  lineage.ts                   Burn / Egg / Hatch pure transition law
  receipt.ts                   stable public receipt projection

src/adapters/
  assetStore.ts                FileSystem asset persistence + SHA-256
  database.ts                  SQLite schema + transactional writes
  sourceIngress.ts             camera/import admission coordinator
  expoCamera.ts                expo-camera adapter
  expoImporter.ts              expo-image-picker adapter
  candidateRenderer.ts         Skia candidate rendering/materialization
  receiptExport.ts             JSON receipt file + OS share sheet

src/components/
  ShutterButton.tsx            immediate shutter acknowledgement
  CandidateCanvas.tsx          Skia visual recipe renderer
  SixUpGrid.tsx                candidate family presentation
  DispositionBar.tsx           KEEP / COMPOST / HAUNT controls
  CameraPresence.tsx           subtle mood/identity expression surface

src/state/
  cameraStore.ts               app orchestration; no domain law

src/__tests__/
  sourceWitness.test.ts
  livingState.test.ts
  development.test.ts
  lineage.test.ts
  receipt.test.ts
  database.test.ts
  sourceIngress.test.ts
  cameraStore.test.ts

assets/fixtures/
  witness-grid.png             known geometry fixture
  witness-dark.png             difficult low-light fixture
  witness-flat.png             low-detail negative control
```

---

### Task 1: Scaffold the mobile app and deterministic test harness

**Files:**
- Create: `package.json`
- Create: `app.json`
- Create: `eas.json`
- Create: `tsconfig.json`
- Create: `jest.config.js`
- Create: `app/_layout.tsx`
- Create: `app/index.tsx`
- Create: `src/__tests__/smoke.test.tsx`

**Interfaces:**
- Consumes: approved design spec only.
- Produces: Expo SDK 57 application root; strict TypeScript; `npm test`, `npm run typecheck`, and `npm run lint` gates available to every later task.

- [ ] **Step 1: Create the SDK 57 scaffold without overwriting repository docs**

Run from a temporary directory and copy the generated app files into the repository root:

```bash
npx create-expo-app@latest haunted-polaroid-seed --template default@sdk-57
```

Install native dependencies with Expo's version resolver:

```bash
npx expo install expo-camera expo-image-picker expo-file-system expo-sqlite expo-crypto expo-sharing @shopify/react-native-skia
npm install --save-dev jest jest-expo @testing-library/react-native @types/jest
```

Keep `docs/` and the existing `README.md`; remove demo routes/assets that do not serve the product.

- [ ] **Step 2: Add strict test/typecheck scripts and the first failing smoke test**

`package.json` scripts must include:

```json
{
  "scripts": {
    "start": "expo start",
    "android": "expo start --android",
    "ios": "expo start --ios",
    "test": "jest --runInBand",
    "typecheck": "tsc --noEmit",
    "lint": "expo lint"
  }
}
```

`jest.config.js`:

```js
module.exports = {
  preset: 'jest-expo',
  testMatch: ['**/src/__tests__/**/*.test.ts', '**/src/__tests__/**/*.test.tsx'],
};
```

First test:

```tsx
import { render, screen } from '@testing-library/react-native';
import HomeScreen from '../../app/index';

test('home exposes both first-class ingress doors', () => {
  render(<HomeScreen />);
  expect(screen.getByText('SHOOT')).toBeTruthy();
  expect(screen.getByText('EAT A PHOTO')).toBeTruthy();
});
```

- [ ] **Step 3: Run the test and confirm RED**

Run:

```bash
npm test -- src/__tests__/smoke.test.tsx
```

Expected: FAIL because the product home route does not yet expose both ingress controls.

- [ ] **Step 4: Implement the minimal home and root layout**

`app/_layout.tsx` should contain only a stack with header disabled. `app/index.tsx` should render two accessible `Pressable`s with exact labels `SHOOT` and `EAT A PHOTO`; route actions may be inert until Task 7.

- [ ] **Step 5: Run all scaffold gates and commit**

Run:

```bash
npm test
npm run typecheck
npm run lint
```

Expected: all exit 0.

Commit:

```bash
git add package.json app.json eas.json tsconfig.json jest.config.js app src

git commit -m "chore: scaffold Haunted Polaroid mobile app"
```

---

### Task 2: Admit an immutable canonical source witness

**Files:**
- Create: `src/domain/types.ts`
- Create: `src/domain/sourceWitness.ts`
- Create: `src/__tests__/sourceWitness.test.ts`

**Interfaces:**
- Consumes: no native APIs.
- Produces:
  - `SourceKind = 'capture' | 'import'`
  - `SourceWitness`
  - `createSourceWitness(input: AdmitSourceInput): SourceWitness`
  - `assertSha256(value: string): HexDigest`

- [ ] **Step 1: Write the failing witness-contract tests**

Use these semantic types in `src/domain/types.ts`:

```ts
export type HexDigest = string & { readonly __brand: 'sha256' };
export type SourceKind = 'capture' | 'import';

export interface SourceWitness {
  readonly sourceId: string;
  readonly kind: SourceKind;
  readonly admittedAt: string;
  readonly assetDigest: HexDigest;
  readonly byteLength: number;
  readonly canonicalFrameRef: string;
  readonly temporalEnvelopeRefs: readonly string[];
}
```

Test capture and import parity plus canonical immutability:

```ts
import { createSourceWitness } from '../domain/sourceWitness';

const DIGEST = 'a'.repeat(64);

test('capture preserves the explicit shutter frame as canonical', () => {
  const witness = createSourceWitness({
    sourceId: 'source-1',
    kind: 'capture',
    admittedAt: '2026-08-17T20:00:00.000Z',
    assetDigest: DIGEST,
    byteLength: 42,
    canonicalFrameRef: 'frame-shutter.jpg',
    temporalEnvelopeRefs: ['frame-before.jpg', 'frame-after.jpg'],
  });
  expect(witness.canonicalFrameRef).toBe('frame-shutter.jpg');
  expect(witness.temporalEnvelopeRefs).toEqual(['frame-before.jpg', 'frame-after.jpg']);
});

test('import uses the same witness contract with no fake camera envelope', () => {
  const witness = createSourceWitness({
    sourceId: 'source-2',
    kind: 'import',
    admittedAt: '2026-08-17T20:01:00.000Z',
    assetDigest: DIGEST,
    byteLength: 84,
    canonicalFrameRef: 'import.jpg',
    temporalEnvelopeRefs: [],
  });
  expect(witness.kind).toBe('import');
  expect(witness.canonicalFrameRef).toBe('import.jpg');
});
```

Also test rejection of non-64-char SHA-256, non-positive byte length, empty canonical ref, and an import carrying envelope refs.

- [ ] **Step 2: Run witness tests and verify RED**

```bash
npm test -- src/__tests__/sourceWitness.test.ts
```

Expected: FAIL because `createSourceWitness` does not exist.

- [ ] **Step 3: Implement the minimal admission law**

`createSourceWitness` must validate first, freeze/copy the envelope array, and never derive the canonical frame from envelope order:

```ts
export function createSourceWitness(input: AdmitSourceInput): SourceWitness {
  const assetDigest = assertSha256(input.assetDigest);
  if (!input.sourceId.trim()) throw new Error('source_id_required');
  if (!input.canonicalFrameRef.trim()) throw new Error('canonical_frame_required');
  if (!Number.isSafeInteger(input.byteLength) || input.byteLength <= 0) {
    throw new Error('invalid_byte_length');
  }
  if (input.kind === 'import' && input.temporalEnvelopeRefs.length > 0) {
    throw new Error('import_cannot_claim_temporal_envelope');
  }
  return Object.freeze({
    ...input,
    assetDigest,
    temporalEnvelopeRefs: Object.freeze([...input.temporalEnvelopeRefs]),
  });
}
```

- [ ] **Step 4: Run tests/typecheck and commit**

```bash
npm test -- src/__tests__/sourceWitness.test.ts
npm run typecheck
git add src/domain src/__tests__/sourceWitness.test.ts
git commit -m "feat: add canonical source witness admission"
```

---

### Task 3: Implement the recursive residue → mood → identity engine

**Files:**
- Create: `src/domain/livingState.ts`
- Modify: `src/domain/types.ts`
- Create: `src/__tests__/livingState.test.ts`

**Interfaces:**
- Consumes: `Disposition = 'KEEP' | 'COMPOST' | 'HAUNT'`; candidate `VisualSignature`.
- Produces:
  - `LivingState`
  - `createInitialLivingState(identityId: string): LivingState`
  - `applyDisposition(state: LivingState, event: DispositionEvent): LivingState`
  - `projectDevelopmentInfluence(state: LivingState): DevelopmentInfluence`

- [ ] **Step 1: Define hidden internal vectors and failing bounded-update tests**

Use eight internal visual axes, all clamped to `[-1, 1]`:

```ts
export const VISUAL_AXES = [
  'negativeSpace',
  'centerGravity',
  'depth',
  'motionTolerance',
  'chromaMemory',
  'temporalEcho',
  'asymmetry',
  'hauntSensitivity',
] as const;
```

The UI must never render these names or values.

Tests must prove:

```ts
test('one disposition cannot move any identity axis by more than 0.03', () => {
  const before = createInitialLivingState('cam-1');
  const after = applyDisposition(before, keepEvent('evt-1', extremeSignature()));
  for (const axis of VISUAL_AXES) {
    expect(Math.abs(after.identity[axis] - before.identity[axis])).toBeLessThanOrEqual(0.03);
  }
});

test('mood moves faster than identity', () => {
  const before = createInitialLivingState('cam-1');
  const after = applyDisposition(before, hauntEvent('evt-2', extremeSignature()));
  expect(vectorDistance(after.mood, before.mood)).toBeGreaterThan(
    vectorDistance(after.identity, before.identity),
  );
});

test('same state plus same event replays exactly', () => {
  const state = createInitialLivingState('cam-1');
  const event = keepEvent('evt-3', extremeSignature());
  expect(applyDisposition(state, event)).toEqual(applyDisposition(state, event));
});
```

- [ ] **Step 2: Run and verify RED**

```bash
npm test -- src/__tests__/livingState.test.ts
```

- [ ] **Step 3: Implement deterministic bounded learning**

Use fixed update strengths:

```ts
const IDENTITY_RATE = { KEEP: 0.02, COMPOST: -0.006, HAUNT: 0.03 } as const;
const MOOD_RATE = { KEEP: 0.12, COMPOST: -0.05, HAUNT: 0.18 } as const;
```

For each visual axis:

```ts
nextIdentity[axis] = clamp(
  state.identity[axis] + IDENTITY_RATE[event.disposition] * event.signature[axis],
  -1,
  1,
);

nextMood[axis] = clamp(
  state.mood[axis] + MOOD_RATE[event.disposition] * event.signature[axis],
  -1,
  1,
);
```

Bound recent residue to the last 24 disposition events. `projectDevelopmentInfluence` returns a read-only blended vector where mood contributes 60%, identity 35%, and mean recent residue 5%. Those percentages are internal implementation constants, not product UI.

- [ ] **Step 4: Add decay/recovery tests and implementation**

Add `advanceMood(state, elapsedHours)` and prove that mood exponentially relaxes toward identity at a fixed half-life of 18 hours without changing identity:

```ts
expect(advanceMood(after, 18).identity).toEqual(after.identity);
expect(vectorDistance(advanceMood(after, 18).mood, after.identity))
  .toBeLessThan(vectorDistance(after.mood, after.identity));
```

- [ ] **Step 5: Run gates and commit**

```bash
npm test -- src/__tests__/livingState.test.ts
npm run typecheck
git add src/domain src/__tests__/livingState.test.ts
git commit -m "feat: add recursive camera living state"
```

---

### Task 4: Plan six deterministic, materially distinct haunted developments

**Files:**
- Create: `src/domain/development.ts`
- Modify: `src/domain/types.ts`
- Create: `src/__tests__/development.test.ts`

**Interfaces:**
- Consumes: `SourceWitness`, `DevelopmentInfluence`.
- Produces:
  - `DevelopmentRecipe`
  - `DevelopmentFamily`
  - `planDevelopmentFamily(input: PlanDevelopmentInput): DevelopmentFamily`
  - `recipeDistance(a, b): number`

- [ ] **Step 1: Write the failing six-up and replay tests**

A recipe must contain enough visual structure to render locally:

```ts
export interface DevelopmentRecipe {
  readonly candidateId: string;
  readonly crop: { x: number; y: number; width: number; height: number };
  readonly rotationDeg: number;
  readonly mirrorX: boolean;
  readonly colorMatrix: readonly number[]; // 20 values
  readonly blurSigma: number;
  readonly displacementScale: number;
  readonly displacementSeed: number;
  readonly temporalBlend: readonly { frameRef: string; opacity: number }[];
  readonly signature: VisualSignature;
}
```

Tests:

```ts
test('first proof always plans exactly six independently addressed candidates', () => {
  const family = planDevelopmentFamily(fixtureInput());
  expect(family.candidates).toHaveLength(6);
  expect(new Set(family.candidates.map(c => c.candidateId)).size).toBe(6);
});

test('same witness, living projection, and seed replay exactly', () => {
  expect(planDevelopmentFamily(fixtureInput())).toEqual(planDevelopmentFamily(fixtureInput()));
});

test('candidate recipes satisfy a minimum pairwise diversity floor', () => {
  const family = planDevelopmentFamily(fixtureInput());
  for (let i = 0; i < 6; i++) for (let j = i + 1; j < 6; j++) {
    expect(recipeDistance(family.candidates[i], family.candidates[j])).toBeGreaterThanOrEqual(0.22);
  }
});
```

- [ ] **Step 2: Verify RED**

```bash
npm test -- src/__tests__/development.test.ts
```

- [ ] **Step 3: Implement seeded recipe generation with diversity-before-randomness**

Use a deterministic PRNG seeded from `familySeed + sourceId + cameraIdentityId`. Generate six proposals from six internal starting pressures—`witness`, `drift`, `scar`, `threshold`, `echo`, `misremember`—but do not expose those as user-selectable filters.

Each candidate must perturb at least three independent dimensions. Re-roll only the recipe-local seed when pairwise distance is `< 0.22`; cap retries at 12 and fail explicitly with `development_diversity_unsatisfied` rather than silently returning duplicates.

- [ ] **Step 4: Add temporal-envelope legality tests**

When `SourceWitness.temporalEnvelopeRefs` is empty, every recipe must use an empty `temporalBlend`. When non-empty, any blend ref must come from that exact bounded list; the shutter frame remains outside `temporalBlend` because it is already the canonical source.

- [ ] **Step 5: Run gates and commit**

```bash
npm test -- src/__tests__/development.test.ts
npm run typecheck
git add src/domain src/__tests__/development.test.ts
git commit -m "feat: plan deterministic haunted six-up families"
```

---

### Task 5: Render and materialize candidate photographs locally with Skia

**Files:**
- Create: `src/components/CandidateCanvas.tsx`
- Create: `src/adapters/candidateRenderer.ts`
- Create: `assets/fixtures/witness-grid.png`
- Create: `assets/fixtures/witness-dark.png`
- Create: `assets/fixtures/witness-flat.png`
- Create: `src/__tests__/candidateRenderer.test.ts`

**Interfaces:**
- Consumes: `DevelopmentRecipe`, source image URI.
- Produces:
  - `<CandidateCanvas sourceUri recipe canvasRef />`
  - `materializeCandidate(canvasRef, candidateId): Promise<Uint8Array>`

- [ ] **Step 1: Add failing renderer contract tests around recipe interpretation**

Keep pixel-exact native rendering out of Jest. Instead unit-test `buildRenderModel(recipe)` so each recipe deterministically maps to crop transform, color matrix, blur, displacement, and temporal overlays.

```ts
test('render model preserves all recipe-owned visual parameters', () => {
  const recipe = fixtureRecipe();
  expect(buildRenderModel(recipe)).toMatchObject({
    crop: recipe.crop,
    rotationDeg: recipe.rotationDeg,
    blurSigma: recipe.blurSigma,
    displacementScale: recipe.displacementScale,
  });
});
```

- [ ] **Step 2: Verify RED**

```bash
npm test -- src/__tests__/candidateRenderer.test.ts
```

- [ ] **Step 3: Implement `CandidateCanvas` using React Native Skia**

Use `<Canvas>`, `<Image fit="cover">`, `<ColorMatrix>`, `<Blur>`, and a deterministic turbulence/displacement filter. Apply crop/rotation/mirror transforms before filters. Temporal blends, when present, render as low-opacity additional source images with deterministic offsets derived from `displacementSeed`.

Do not add random calls in render code; all variation must already exist in the recipe.

- [ ] **Step 4: Implement materialization through the canvas snapshot API**

`candidateRenderer.ts`:

```ts
export async function materializeCandidate(
  ref: React.RefObject<SkiaDomView>,
): Promise<Uint8Array> {
  const image = await ref.current?.makeImageSnapshotAsync();
  if (!image) throw new Error('candidate_snapshot_failed');
  return image.encodeToBytes();
}
```

Adapt the exact ref type to the SDK-exported type during implementation; keep the function boundary and error contract unchanged.

- [ ] **Step 5: Run unit gates and perform one manual native visual smoke**

Run:

```bash
npm test -- src/__tests__/candidateRenderer.test.ts
npm run typecheck
npx expo start
```

On a native simulator/device, render `witness-grid.png` through six fixture recipes and confirm all six surfaces visibly differ. Record this as a manual development note; do not call it the human product witness yet.

Commit:

```bash
git add src/components src/adapters/candidateRenderer.ts assets/fixtures src/__tests__/candidateRenderer.test.ts
git commit -m "feat: render local haunted candidate photographs"
```

---

### Task 6: Add durable local asset storage, SHA-256, SQLite ledger, and camera identity persistence

**Files:**
- Create: `src/adapters/assetStore.ts`
- Create: `src/adapters/database.ts`
- Create: `src/__tests__/database.test.ts`
- Create: `src/__tests__/assetStore.test.ts`

**Interfaces:**
- Produces:
  - `persistSourceAsset(uri): Promise<PersistedAsset>`
  - `persistCandidateBytes(candidateId, bytes): Promise<PersistedAsset>`
  - `openDatabase(): Promise<SQLiteDatabase>`
  - `appendEvent(tx, event): Promise<void>`
  - `loadLivingState(identityId): Promise<LivingState | null>`
  - `saveLivingState(tx, state): Promise<void>`

- [ ] **Step 1: Write failing schema and adapter tests**

Required SQLite tables:

```sql
CREATE TABLE camera_identity (
  identity_id TEXT PRIMARY KEY,
  generation INTEGER NOT NULL,
  status TEXT NOT NULL CHECK(status IN ('living','burned')),
  state_json TEXT NOT NULL,
  version INTEGER NOT NULL,
  updated_at TEXT NOT NULL
);

CREATE TABLE source_witness (
  source_id TEXT PRIMARY KEY,
  kind TEXT NOT NULL,
  admitted_at TEXT NOT NULL,
  asset_digest TEXT NOT NULL,
  byte_length INTEGER NOT NULL,
  canonical_frame_ref TEXT NOT NULL,
  envelope_json TEXT NOT NULL
);

CREATE TABLE event_ledger (
  event_id TEXT PRIMARY KEY,
  event_type TEXT NOT NULL,
  occurred_at TEXT NOT NULL,
  payload_json TEXT NOT NULL,
  payload_digest TEXT NOT NULL
);

CREATE TABLE development_family (
  family_id TEXT PRIMARY KEY,
  source_id TEXT NOT NULL,
  camera_identity_id TEXT NOT NULL,
  family_json TEXT NOT NULL,
  created_at TEXT NOT NULL
);

CREATE TABLE phoenix_egg (
  egg_id TEXT PRIMARY KEY,
  parent_identity_id TEXT NOT NULL,
  payload_json TEXT NOT NULL,
  status TEXT NOT NULL CHECK(status IN ('dormant','consumed')),
  created_at TEXT NOT NULL,
  consumed_at TEXT
);
```

Tests must prove re-opening the database preserves identity state and duplicate `event_id` insertion rejects rather than silently duplicating history.

- [ ] **Step 2: Verify RED**

```bash
npm test -- src/__tests__/database.test.ts src/__tests__/assetStore.test.ts
```

- [ ] **Step 3: Implement app-private asset directories and hashing**

Use `Directory(Paths.document, 'haunted-polaroid')` with `sources/`, `candidates/`, and `receipts/` children. Copy admitted sources out of temporary camera/picker caches before sealing their witness.

Hash bytes using:

```ts
const bytes = await file.bytes();
const digestBuffer = await Crypto.digest(Crypto.CryptoDigestAlgorithm.SHA256, bytes);
const digestHex = [...new Uint8Array(digestBuffer)]
  .map(b => b.toString(16).padStart(2, '0'))
  .join('');
```

The persisted asset result must contain URI, 64-character digest, and byte length.

- [ ] **Step 4: Implement SQLite initialization and transaction helpers**

Enable WAL and run schema creation on open. All multi-record domain transitions later used for dispositions, Burn, and Hatch must run inside SQLite transactions.

- [ ] **Step 5: Run gates and commit**

```bash
npm test -- src/__tests__/database.test.ts src/__tests__/assetStore.test.ts
npm run typecheck
git add src/adapters src/__tests__/database.test.ts src/__tests__/assetStore.test.ts
git commit -m "feat: add local provenance storage"
```

---

### Task 7: Wire fresh shutter and photo ingestion into the same admission coordinator

**Files:**
- Create: `src/adapters/expoCamera.ts`
- Create: `src/adapters/expoImporter.ts`
- Create: `src/adapters/sourceIngress.ts`
- Create: `src/components/ShutterButton.tsx`
- Create: `app/camera.tsx`
- Create: `src/__tests__/sourceIngress.test.ts`

**Interfaces:**
- Produces:
  - `captureCanonicalFrame(cameraRef): Promise<RawSourceAsset>`
  - `pickImportedImage(): Promise<RawSourceAsset | null>`
  - `admitRawSource(raw, kind): Promise<SourceWitness>`

- [ ] **Step 1: Write failing ingress parity and failure tests**

Use dependency injection so native capture/picker and persistence can be faked:

```ts
test('capture and import both end in SourceWitness admission', async () => {
  const capture = await admitRawSource(fakeRaw('capture.jpg'), 'capture', deps);
  const imported = await admitRawSource(fakeRaw('import.jpg'), 'import', deps);
  expect(capture.kind).toBe('capture');
  expect(imported.kind).toBe('import');
});

test('failed durable copy never seals a witness', async () => {
  const deps = failingPersistDeps();
  await expect(admitRawSource(fakeRaw('capture.jpg'), 'capture', deps))
    .rejects.toThrow('source_persistence_failed');
  expect(deps.database.insertWitness).not.toHaveBeenCalled();
});
```

- [ ] **Step 2: Verify RED**

```bash
npm test -- src/__tests__/sourceIngress.test.ts
```

- [ ] **Step 3: Implement camera capture with immediate UI acknowledgement**

`ShutterButton` must synchronously enter a `pressed` visual state in the `onPress` handler before awaiting `takePictureAsync`:

```ts
const onPress = () => {
  setAcknowledged(true);
  void onShutter();
};
```

`expoCamera.ts` waits for `CameraView` readiness and uses `takePictureAsync`. The returned cache URI becomes the explicit canonical frame candidate; do not wait for development before presenting the captured state.

The first proof may set `temporalEnvelopeRefs: []` on real device capture. Keep the domain abstraction and fixture coverage for bounded envelopes; true pre/post burst capture is a later native optimization unless a safe device API becomes available during implementation.

- [ ] **Step 4: Implement photo eater through `expo-image-picker`**

Pick a single image without editing/cropping in the system picker. Copy it into controlled storage, hash it, then seal a `kind: 'import'` witness with no temporal envelope.

- [ ] **Step 5: Run tests and a native ingress smoke, then commit**

```bash
npm test -- src/__tests__/sourceIngress.test.ts
npm run typecheck
npm run lint
```

Native smoke criteria:

1. deny camera permission → camera door refuses clearly while photo eater remains usable;
2. grant camera permission → one shutter produces one canonical witness;
3. import an existing photo → produces the same post-admission route.

Commit:

```bash
git add src/adapters src/components/ShutterButton.tsx app/camera.tsx src/__tests__/sourceIngress.test.ts
git commit -m "feat: add camera and photo-eater ingress"
```

---

### Task 8: Complete the living six-up interaction loop

**Files:**
- Create: `src/state/cameraStore.ts`
- Create: `src/components/SixUpGrid.tsx`
- Create: `src/components/DispositionBar.tsx`
- Create: `src/components/CameraPresence.tsx`
- Create: `app/develop/[familyId].tsx`
- Modify: `app/index.tsx`
- Create: `src/__tests__/cameraStore.test.ts`

**Interfaces:**
- Consumes: witness admission, living state, development planning, renderer, database.
- Produces: `CameraStore` commands `developSource`, `materializeCandidate`, `applyCandidateDisposition`, `startNextFamily`.

- [ ] **Step 1: Write failing orchestration tests**

```ts
test('developSource creates one persisted family of six from current living state', async () => {
  const store = makeTestStore();
  const family = await store.developSource(fixtureWitness());
  expect(family.candidates).toHaveLength(6);
  expect(store.db.saveFamily).toHaveBeenCalledWith(family);
});

test('disposition is recorded before living-state mutation is persisted', async () => {
  const store = makeTestStore();
  await store.applyCandidateDisposition('candidate-1', 'HAUNT');
  expect(store.calls).toEqual([
    'append:disposition',
    'save:living-state',
  ]);
});
```

Add an idempotency test: replaying the same `eventId` must return the already-applied result instead of changing identity twice.

- [ ] **Step 2: Verify RED**

```bash
npm test -- src/__tests__/cameraStore.test.ts
```

- [ ] **Step 3: Implement transactionally ordered orchestration**

For a disposition:

```text
BEGIN
  insert disposition event_id (unique)
  derive next LivingState from previous state + event
  update camera_identity version + state_json
COMMIT
```

If the unique event already exists, read and return the current state without reapplying the delta.

- [ ] **Step 4: Build the six-up UI without exposing personality stats**

`SixUpGrid` renders six `CandidateCanvas` surfaces. Selecting one opens `DispositionBar` with exact actions `KEEP`, `COMPOST`, `HAUNT`.

`CameraPresence` may express current mood only through subtle nonverbal UI behavior—breathing frame, development timing, tiny layout tension, or ambient surface movement. It may not print axis names, numeric scores, or “your camera prefers X.”

After a disposition, show `DEVELOP AGAIN` to generate another family from the same canonical source under the now-changed state. The original source witness remains addressable and unchanged.

- [ ] **Step 5: Run gates and interaction smoke, then commit**

```bash
npm test
npm run typecheck
npm run lint
```

Human development smoke:

- shoot one photo and obtain six;
- import one photo and obtain six;
- HAUNT one candidate, develop again, and see a changed family;
- confirm the app never displays personality vectors;
- restart app and confirm the same living camera identity returns.

Commit:

```bash
git add app src/state src/components src/__tests__/cameraStore.test.ts
git commit -m "feat: close the living camera development loop"
```

---

### Task 9: Prove irreversible Phoenix Burn / Egg / Hatch lineage locally

**Files:**
- Create: `src/domain/lineage.ts`
- Create: `src/__tests__/lineage.test.ts`
- Modify: `src/adapters/database.ts`

**Interfaces:**
- Produces:
  - `planBurn(identity, burnEvent): BurnTransition`
  - `planHatch(egg, hatchEvent): HatchTransition`
  - `commitBurn(db, transition): Promise<PhoenixEgg>`
  - `commitHatch(db, transition): Promise<CameraIdentity>`

- [ ] **Step 1: Write failing pure lineage invariants**

```ts
test('burn creates one dormant egg and permanently burns parent', () => {
  const result = planBurn(livingIdentity(), burnEvent('burn-1'));
  expect(result.parent.status).toBe('burned');
  expect(result.egg.status).toBe('dormant');
  expect(result.egg.parentIdentityId).toBe('cam-1');
});

test('burned camera cannot burn again', () => {
  expect(() => planBurn(burnedIdentity(), burnEvent('burn-2')))
    .toThrow('camera_not_living');
});

test('consumed egg cannot hatch twice', () => {
  expect(() => planHatch(consumedEgg(), hatchEvent('hatch-2')))
    .toThrow('egg_not_dormant');
});

test('descendant inherits bounded disposition but receives a new identity id', () => {
  const result = planHatch(dormantEgg(), hatchEvent('hatch-1'));
  expect(result.descendant.identityId).not.toBe(dormantEgg().parentIdentityId);
  expect(result.descendant.generation).toBe(dormantEgg().parentGeneration + 1);
});
```

- [ ] **Step 2: Verify RED**

```bash
npm test -- src/__tests__/lineage.test.ts
```

- [ ] **Step 3: Implement pure Burn/Hatch transitions**

Phoenix inheritance payload includes only normalized identity/mood-dynamics parameters, lineage digest, parent generation, and bounded scars. It must not contain source URIs, source image bytes, candidate image bytes, or temporal-frame refs.

The descendant starts from inherited identity plus deterministic mutation derived from `eggId + hatchEventId`, with every inherited axis perturbation clamped to `±0.08` so hatch is related but not byte-identical restoration.

- [ ] **Step 4: Implement atomic database commits and crash-safe idempotency**

`commitBurn` transaction order:

```text
BEGIN
  require parent status = living
  insert burn event (unique)
  insert exactly one egg keyed by burn event
  update parent status = burned
COMMIT
```

`commitHatch` transaction order:

```text
BEGIN
  require egg status = dormant
  insert hatch event (unique)
  create descendant identity
  update egg status = consumed + consumed_at
COMMIT
```

A retry of the same event id returns the already-created egg/descendant. A different second burn/hatch event rejects.

- [ ] **Step 5: Add a privacy regression test and commit**

Serialize the egg payload and assert none of these keys or values appear: `canonicalFrameRef`, `temporalEnvelopeRefs`, `sourceId`, `file://`, `.jpg`, `.png`.

Run:

```bash
npm test -- src/__tests__/lineage.test.ts src/__tests__/database.test.ts
npm run typecheck
git add src/domain/lineage.ts src/adapters/database.ts src/__tests__
git commit -m "feat: prove irreversible Phoenix lineage"
```

Do not add Burn/Hatch UI in this task. The first proof establishes the law beneath a later danger ritual.

---

### Task 10: Export truthful receipts and run the packaged human witness gate

**Files:**
- Create: `src/domain/receipt.ts`
- Create: `src/adapters/receiptExport.ts`
- Create: `src/__tests__/receipt.test.ts`
- Modify: `app/about.tsx`
- Modify: `README.md`
- Modify: `eas.json`

**Interfaces:**
- Produces:
  - `buildDevelopmentReceipt(session): PublicDevelopmentReceipt`
  - `exportReceipt(receipt): Promise<string>` returning local JSON URI.

- [ ] **Step 1: Write failing receipt-minimization and replay tests**

Public receipt shape:

```ts
export interface PublicDevelopmentReceipt {
  schema: 'haunted-polaroid-development-receipt-v1';
  cameraIdentityId: string;
  cameraGeneration: number;
  source: {
    sourceId: string;
    kind: 'capture' | 'import';
    assetDigest: string;
    byteLength: number;
  };
  familyId: string;
  candidateId?: string;
  disposition?: 'KEEP' | 'COMPOST' | 'HAUNT';
  eventIds: readonly string[];
  createdAt: string;
}
```

Explicitly exclude raw living vectors, source file URIs, temporary envelope refs, and private candidate file paths.

Test stable key order by canonicalizing before export and prove the same session state generates byte-identical JSON.

- [ ] **Step 2: Verify RED**

```bash
npm test -- src/__tests__/receipt.test.ts
```

- [ ] **Step 3: Implement receipt export and native share action**

Write canonical UTF-8 JSON into `receipts/<familyId>.json` under the app documents directory. Add a `SHARE RECEIPT` action that invokes `Sharing.shareAsync(uri)` only when native sharing is available.

- [ ] **Step 4: Configure an installable Android development build**

`eas.json` development profile:

```json
{
  "build": {
    "development": {
      "developmentClient": true,
      "distribution": "internal",
      "android": { "buildType": "apk" }
    }
  }
}
```

Run final machine gates:

```bash
npm test
npm run typecheck
npm run lint
npx expo export --platform android
```

If EAS credentials are available, also run:

```bash
npx eas-cli@latest build --platform android --profile development
```

Do not claim packaged-device behavior from source tests alone.

- [ ] **Step 5: Perform the first human witness checklist on the installable app**

Witness three sources:

1. **ordinary real-world fresh capture** — press shutter and judge perceived acknowledgement latency;
2. **difficult fresh capture** — low light, motion, or low-detail subject;
3. **existing imported photograph** — verify photo eater parity.

For each specimen record:

```text
source kind:
source digest:
shutter acknowledgement: immediate | perceptible delay | failed
six candidates present: yes | no
six candidates materially diverse: yes | no | mixed
restraint present in at least one candidate: yes | no
KEEP/COMPOST/HAUNT usable: yes | no
second family responds after disposition: yes | no | unclear
camera identity survives restart: yes | no
receipt exports and matches source digest: yes | no
notes:
```

The first proof passes only if capture/import truth is preserved and the living loop works. Aesthetic disappointment is field evidence for later development recipes; it must not be hidden by changing the provenance contract.

- [ ] **Step 6: Update README with witnessed status and commit**

Only after the human field run, update README to distinguish machine-verified invariants from perceptual witness results.

Commit:

```bash
git add src/domain/receipt.ts src/adapters/receiptExport.ts src/__tests__/receipt.test.ts app/about.tsx README.md eas.json
git commit -m "feat: add receipt export and first-proof witness gate"
```

---

## Self-review result

### Spec coverage

Covered in this plan:

- camera + photo eater parity: Tasks 2 and 7;
- canonical shutter witness: Tasks 2 and 7;
- six-up: Tasks 4, 5, and 8;
- KEEP / COMPOST / HAUNT: Tasks 3 and 8;
- residue → mood → identity recursion: Task 3;
- invisible personality: Task 8;
- invisible composition apprenticeship: candidate signatures and diversity pressure in Tasks 3–5, with perceptual validation in Task 10;
- metabolized/private memory boundary: Tasks 3, 6, and 9;
- truthful provenance: Tasks 2, 6, and 10;
- Phoenix irreversible lineage: Task 9;
- remote Chrysalis: deliberately deferred by the approved first-proof scope while the data boundaries remain compatible.

### Placeholder scan

No `TBD`, `TODO`, “implement later,” generic “add error handling,” or undefined placeholder task remains. Remote Chrysalis is named as an explicit out-of-scope product slice rather than an unfinished step.

### Type/interface consistency

`SourceWitness`, `LivingState`, `DevelopmentInfluence`, `DevelopmentRecipe`, `DevelopmentFamily`, `PhoenixEgg`, and `PublicDevelopmentReceipt` each have one owning domain module and flow forward through explicit adapter/store boundaries. No UI component owns domain mutation law.

## Execution handoff

Recommended execution is **Subagent-Driven Development**: one fresh implementation agent per task, with review between tasks and the final human device witness kept explicit. Inline execution remains viable if a single-session implementation is preferred.
