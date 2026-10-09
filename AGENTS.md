Read AGENTS-shape.md first — the rules of this repository's shape.

This is the assembly root of **openWallet** (`openwallet`): the repository an
engineer clones. It holds `project.yaml`, the pins and the gate, and it mounts
the two legs.

| role | repository | path |
|---|---|---|
| assembly | `opensoft/openWallet` | `.` |
| spec | `opensoft/openWallet-spec` | `spec/` |
| code | `opensoft/openWallet-code` | `code/` |

Everything below this line is openWallet's own. The shape wrote the block above
once and does not pin this file, so how this project is built, tested, reviewed
and released belongs here and nothing upstream will overwrite it.

## Read beside `AGENTS-shape.md`: the declared Q7 override

`AGENTS-shape.md` says that a contract the code reads but does not own lives in
the SPEC leg. openRepoShape's path classification
(`contracts/path-classification.yaml`, at
`7f84ca42ca86a8902928345109d2bf6bad87bd91`) sends `contracts/**` there under the
rule `spec-governance`. openWallet departs from that default for its two
contract families, and the departure is DECLARED, not implied:

- **The ruling.** Brett Heap, 2026-10-08, in session, by multiple choice:
  "Code leg, declared override (Recommended)" (RULED Q7, recorded at
  2026-10-08T17:01:43Z in opensoft/openXwallet
  `openspec/changes/split-openwallet-neutral-core/proposal.md`).
  `contracts/openxwallet/` and `contracts/openxwallet-agent-profile/` live in
  the CODE leg, beside the validator that resolves every contract path from its
  own location. The schemas, the corpus and the validator are one release unit.
- **The declaration.** The carve manifest, opensoft/openXwallet
  `docs/openwallet-carve-manifest.yaml`, declares the override. Its
  `leg_overrides:` entry `q7-code-leg` names the rule it overrides
  (`spec-governance`), the leg it takes (`code`) and its authority. Each of the
  73 rows it governs records `leg_default:` (the classifier's answer) beside
  `leg_override: q7-code-leg`.
- **A second, PROPOSED override** in the same file, `d7-root-release-identity`,
  places the release identity at THIS root: 9 rows, `contracts/manifest.yaml`,
  `contracts/CHANGELOG.md`, the six `contracts/releases/` records and
  `docs/byte-identity-wallet-v1.0.md`. It follows openDox's root release
  placement and is not covered by Q7's ruling.

A later `update-shape` run, an adoption check or a reviewer reading the default
may flag the code leg's contracts. This section is the answer: the placement is
ruled and declared, and it is not drift.

## Shared OpenSpec/Speckit protocol

Use the shared OpenSpec/Speckit workflow from:

- `$HOME/.agents/AGENTS.md`
- `$HOME/.agents/protocols/openspec-speckit-workflow.md`
- `$HOME/.agents/protocols/project-agent-bootstrap.md`

Repository documents remain authoritative for openWallet product facts, contract
ownership, validation, versioning, and release constraints.

This is a three-leg project, and the protocol runs from here:

| artifact | where |
|---|---|
| `.specify/` (templates, scripts, the git extension and its park/resume overlay) | this root |
| the full `openspec/` instance (canonical specs, changes, archive) | spec leg, `spec/openspec/`. Run `openspec` there, through the leg's pinned CLI |
| Speckit feature directories `specs/NNN-*` | spec leg, `spec/specs/NNN-*` |
| implementation and tests | code leg, `code/` |
| feature worktrees | `worktrees/<NNN-feature-name>/{spec,code}/` under this root |

**No feature is active.** `.specify/feature.json` is absent, which is the
overlay's "no feature" state. The feature hook writes that file here when a
feature is created.

**`worktrees/` is NOT ignored by this root's `.gitignore`.** The bootstrap
contract adds `/worktrees/` to the root's `.gitignore`. Here, though,
`.gitignore` is a shape copy, digest-pinned in `contracts/shape-pin.yaml`, and
that edit is reported as `shape-copy-drift`. Until openRepoShape carries the
line upstream:
- stage only the paths you name;
- never run `git add -A` at this root;
- if you use worktrees, add `/worktrees/` to your clone's own
  `.git/info/exclude`.

`AGENTS-shape.md` already forbids committing anything under `worktrees/`.

## What this repository is

**Status: carved** (2026-10-08, task 4.5 of openXwallet's
`split-openwallet-neutral-core`). The content arrived from opensoft/openXwallet
at the carve commit `90111df262d6f54f7e82651d860adc12345f83f4`. The procedure,
with a rollback written before every phase, is
`docs/openwallet-cutover-runbook.md`. The carve is governed by openXwallet's
`split-openwallet-neutral-core` (tracked in opensoft/openXwallet#25). This root
holds:
- the scaffold;
- the runbook;
- `.specify/`;
- these instructions;
- the ten carved `openwallet_root` rows.

The first release, `wallet-v1.6`, is tagged on
`b0af7c2ce53d63786a08a20aa3602a6f90345606` (opensoft/openWallet#7). At that
commit both pins and both gitlinks name `spec` at
`1924500354f472a6298c02db44a3ae2b21b8908e` (the archive merge of
opensoft/openWallet-spec#4, after the spec leg's carve merge `15c15bbd`) and
`code` at `72313daab1f229c049cb90998931564c1904dbbc` (the code leg's carve
merge). `contracts/manifest.yaml`'s eight owned rows point at
`code/contracts/…`.

openWallet is the neutral wallet standard: two contract families, the packaged
corpus, the conformance validator, the syntax gate and the promoted
requirements, carrying no openxFactory input. It is a PRODUCT that other
repositories pin. It is not a factory layer. openXwallet, where it was built,
becomes the openxFactory adapter that pins it. The factory-layer USE of wallet
authority (review-authority registers, the job envelope's vocabulary, the
issuer anchor) stays in openXwallet and openxFactory.

After the split, this root owns:
- `project.yaml`, the manifest of what this project is;
- **the pins**: `contracts/spec-pin.yaml` and `contracts/code-pin.yaml` (in
  lockstep with the gitlinks), and `contracts/shape-pin.yaml`;
- **the release identity**: `contracts/manifest.yaml`, `contracts/CHANGELOG.md`
  and `contracts/releases/`, all carved from openXwallet, plus the annotated
  `wallet-v*` tag, which is cut here and on no leg;
- **the proof**: `docs/byte-identity-wallet-v1.6.md`, for the first tag,
  `wallet-v1.6`, beside the carved lineage record
  `docs/byte-identity-wallet-v1.0.md`;
- `LICENSE`, carved;
- the cutover runbook and `.specify/`.

The spec leg owns the specifications and its own OpenSpec gate. The code leg
owns the contracts, the corpus, the validator, the syntax gate, their tests and
their checks. Each leg's `AGENTS.md` says so in full.

## The rules that are not negotiable here

1. **Consumers pin; nobody forks.** Consumers pin THIS ROOT by commit and
   digest, and verify the code leg through the root's lockstep: its gitlink,
   `contracts/code-pin.yaml` and the leg's tree digest. A consumer that pinned a
   leg directly would bypass the release identity, so the root commit stays the
   one answer to "which openWallet". Domain descendants pin a version and carry
   a profile, and never fork. A need a profile cannot express is an upstream
   change, made through the spec leg's OpenSpec instance.
2. **Advancing a leg is ONE commit here**, moving together the gitlink,
   `contracts/<role>-pin.yaml` and every workflow `@<sha>` naming that leg
   (`AGENTS-shape.md`). `make pins` refuses otherwise. Never edit a file that has
   a row in `contracts/shape-pin.yaml`.
3. **Machine keys do not move casually.** Live consumers pin these BY NAME:
   paths, `kind:` values, capability ids, the `xfactory_wallet_*` prefix, finding
   codes and file names. They reach the code leg's files as
   `openWallet/code/<path>`. Renaming one is a breaking change with a migration
   note, never a tidy-up.
4. **Every gate is offline.** No check reads the network, an upstream tree or
   another repository's working tree.
   - This root's check is the shape's `validate`: names, manifest and lockstep
     pins.
   - The wallet checks run in the code leg, from the code leg's own root. A
     validator run from here prunes both legs, scans nothing and exits 0, so it
     is never wired as a gate.
   - The spec leg's OpenSpec gate installs its pinned CLI from a tarball
     committed in that leg, under that leg's own ruling, "Vendor the tarball
     (Recommended)".
5. **A release is five coordinated values, cut on this root**, across one root
   commit and the leg commits it pins:
   - per-file `contract_schema_version`, inside the bytes in the code leg;
   - `contract_bundle_version`;
   - an annotated `wallet-v<major>.<minor>` tag on this root;
   - the release commit with per-file digests;
   - the `contracts/CHANGELOG.md` entry.

   No leg is tagged. The tag comes only after the proof is green, and the
   version is allocated at realization.
6. **Run the gates before pushing**: `make validate` here, and each leg's own
   gates in that leg (see its `AGENTS.md`).
