# openWallet cutover runbook

Status: authored before the carve (pre-carve)
Kind: runbook
Governing change: opensoft/openXwallet
`openspec/changes/split-openwallet-neutral-core/`. It was ratified
2026-10-08T17:10:47Z by Brett Heap (operator authority), verbatim "ratify 26 and
merge". This runbook executes:
- `design.md` D7, "Creation route" steps 3-4, "Required checks, per repository"
  and "The proof";
- the "Migration plan", steps 3-5;
- `tasks.md` 4.1-4.9.

Tracked on: opensoft/openXwallet#25

Models:
- opensoft/openXwallet `docs/openxwallet-cutover-runbook.md`, the `wallet-v1.0`
  carve. This runbook follows its discipline and its phase shape.
- opensoft/openxFactory `docs/opendox-cutover-runbook.md`, the first carve into
  an openRepoShape three-leg project. Its `git filter-repo` mechanics were
  measured there, and are reused here and re-measured against this carve.

**This document was authored BEFORE the carve it describes.** Each phase carries
its rollback, and each rollback is written before the phase is taken. A rollback
written afterwards is not a rollback; it is a description of what happened.

**Every command below was rehearsed while this runbook was written**, against
scratch clones and never against a repository anyone else can reach. Each phase
says what the rehearsal printed. The rehearsal could not perform two things:
- the code leg's declared edits, which are task 4.4's own work;
- the pushes, merges, rulesets and the tag, which are acts on GitHub.

The rehearsal record is at the end.

---

## The NAMED CARVE COMMIT

```
CARVE_COMMIT = 90111df262d6f54f7e82651d860adc12345f83f4
SOURCE       = opensoft/openXwallet
```

`90111df` is openXwallet's `main` at the merge of PR #28, after tasks 2.1 (the
archive of `add-multi-key-wallets`) and 2.2 (the reflow of the promoted specs'
wrapped scenario lines). Brett Heap named it, with operator authority, in
session, at 2026-10-08T18:07:19Z, verbatim: "name 90111df as the carve commit,
do 2.4 and 2.5". **Never "HEAD."** openXwallet's `main` has already moved past
it, and the carve runs at this commit regardless.

The commit is recorded in three places:

1. openXwallet `docs/openwallet-carve-manifest.yaml`, `carve_commit:`. It is
   read by `scripts/validate-carve-manifest.py` and by the required check
   `carve-manifest`.
2. This runbook, which holds the procedure.
3. This root's `contracts/manifest.yaml`, `carved_from:`. It is written in
   Phase 3 as one of the declared manifest field edits. It is hand-authored,
   and no check in this project reads it yet.

There is deliberately **no bare `CARVE_COMMIT` file**. An unschema'd file that
nothing reads is the failure class of a governance floor whose source of truth
is loose markdown.

## The declared path mapping this runbook executes

The manifest is openXwallet's `docs/openwallet-carve-manifest.yaml`. It has one
row per tracked path at the carve commit, 232 rows: 120 `moved_verbatim`, 8
`moved_with_declared_edit` and 104 `not_moved` *(as executed against the amended
manifest at `64ca6eac`: 119 `moved_verbatim`, 9 `moved_with_declared_edit` and
104 `not_moved`)*. **Within each leg, every carved
path keeps its repository-relative path** (`destination_path` equals
`source_path` on every moved row). That is what keeps each carve a pure copy and
every digest whole. It is also why no `--path-rename` appears below.

| Destination | Repository | Rows | Verbatim / edited | Declared edit lines | Edit classes |
| --- | --- | ---: | ---: | ---: | --- |
| `openwallet_code` | `opensoft/openWallet-code` | 80 | 77 / 3 | 1 803 | validator hunks (a)-(e); the test split; the envelope-verify step |
| `openwallet_spec` | `opensoft/openWallet-spec` | 38 | 34 / 4 | 14 | the subject lines: eleven, plus the travelling change's three occurrences |
| `openwallet_root` | `opensoft/openWallet` (this repository) | 10 | 9 / 1 | 67 | the manifest field edits |

*(The code leg's row is as authored. As executed against the amended manifest at
`64ca6eac`, it is 76 / 4 with 1 811 declared edit lines, the fourth edited row
being `tests/multi_key_wallets/test_declared_key_sets.py`; the manifest as a
whole declares 1 892 edit lines on 9 rows.)*

The code leg's 80 rows include 73 that go there under a **declared
leg-classification override**. openRepoShape's classifier sends `contracts/**`
to the spec leg under `spec-governance`. The ruling "Code leg, declared override
(Recommended)" (RULED Q7, recorded 2026-10-08T17:01:43Z) keeps the contracts
beside their validator. 9 of the root's 10 rows go to the root under a second,
PROPOSED override, `d7-root-release-identity`, which follows openDox's
root-release placement. Each overriding row names the override it takes.

**Declared additions, the files a destination creates and the manifest has no
row for:**
- the corpus binding under `contracts/openxwallet/examples/` (RULED Q6). Its
  file name is the plan's call;
- `LICENSE` in each leg. These are the same Apache-2.0 bytes the root receives
  by the carve.

Nothing else may be added by a declared-edit commit.

**The one path a birth commit and the carve both add.** The spec leg's birth
commit (task 3.6) added `openspec/config.yaml`, because the pinned OpenSpec CLI
refuses an instance without it. It is also a carved row. The two are the same
git blob, `b4bbeb946f4c4d9310ee8730c5f89564bc95e9f0` (sha256
`85b53dd24fbe7d19c8b0f0ddccf5e82600c5c372c76b57a2a89dc34dfb0fc5b9`), so the
unrelated-histories merge meets an identical addition on both sides and resolves
it without a conflict. That was rehearsed (Phase 2). D7's sentence "No carved
path collides with a seed" stays true of the scaffold's seeds. This is the one
birth-commit path that coincides with a carved row, and it coincides
byte-for-byte. **If either side's bytes change before the carve, this becomes a
real conflict, and the carve stops at Phase 2 until it is reconciled.**

## Where this runbook sits

| Migration plan step | What | Where |
| --- | --- | --- |
| 3 | birth: name checks (3.1), scaffold (3.2), its verification (3.3); this runbook and `.specify/` (3.4); each repository's `README.md`, `AGENTS.md`, `CLAUDE.md`, `.github/CODEOWNERS` (3.5); the spec leg's own OpenSpec gate (3.6) | done before Phase 0. Its rollback is the plan's: delete the three repositories, which nothing pins |
| 4 | the legs, then the root in one lockstep commit; the declared edits; the path-mapping proof | Phases 0-4 |
| 5 | three rulesets, then the first tag, on the root | Phases 5-6 |
| 6 onward | openXwallet's adapter rebuild, openxFactory, the consumers, the archive | not here: openXwallet's own pull requests |

The spec leg's birth change (task 4.8) is authored after Phase 2 lands, in that
leg's own OpenSpec instance, and is not a phase of this runbook.

**Nothing in Phases 0-4 touches openXwallet.** The carve COPIES and deletes
nothing. openXwallet sheds its carved rows only in its own adapter rebuild
(Migration plan step 6), after this runbook is complete. **Nothing pins any
openWallet repository until that rebuild**, so every rollback through Phase 6
costs nothing outside openWallet.

---

## The conventions every phase uses

Run everything under **bash**: the commands use bash arrays and bash word
splitting. Run them from a scratch directory made for this carve and nowhere
else, and use a fresh directory for each attempt. A carve reads only trees that
nobody else is editing.

**Stop at the first command that exits non-zero, or that prints anything other
than what this runbook says to expect.** A carve continued past a refusal works
on a half-made tree. The rehearsal of this runbook proved the point: a mirror
made without `--no-local` from a path on disk made filter-repo refuse, the next
commands ran anyway, and an unfiltered history was merged into a scratch leg.

```bash
WORK=$(mktemp -d)                         # the carve's own scratch directory
cd "$WORK" || exit 1
CARVE_COMMIT=90111df262d6f54f7e82651d860adc12345f83f4
SRC_URL=https://github.com/opensoft/openXwallet.git
OXW=<an openXwallet checkout at main>     # holds the manifest and its checker
MANIFEST=$OXW/docs/openwallet-carve-manifest.yaml
```

Requirements:
- `git-filter-repo` (the rehearsal used 2.47.0 with git 2.43.0);
- PyYAML for the helpers below;
- for the manifest checker, the packages `.github/workflows/carve-manifest.yml`
  installs, with the versions it pins.

### The five helpers

These go in `$WORK/bin`, which is outside every clone. Each is
standard-library Python plus PyYAML, and each exits non-zero on any
disagreement.

```bash
mkdir -p "$WORK/bin"

# 1. the destination's paths, one per line, FROM THE MANIFEST
cat > "$WORK/bin/carve-paths.py" <<'PY'
import sys, yaml
dest, manifest = sys.argv[1], sys.argv[2]
doc = yaml.safe_load(open(manifest, encoding="utf-8"))
assert doc["carve_commit"] == "90111df262d6f54f7e82651d860adc12345f83f4", doc["carve_commit"]
for row in doc["rows"]:
    if row.get("destination") == dest:
        assert row["destination_path"] == row["source_path"], row["source_path"]
        print(row["source_path"])
PY

# 2. the CARVE LAYER is exactly the destination's rows, blob + mode identical
cat > "$WORK/bin/carve-layer.py" <<'PY'
import hashlib, subprocess, sys, yaml
dest, manifest, repo, ref = sys.argv[1:5]
def git(*a):
    return subprocess.run(["git", "-C", repo, *a], check=True, capture_output=True).stdout
doc = yaml.safe_load(open(manifest, encoding="utf-8"))
rows = {r["destination_path"]: r for r in doc["rows"] if r.get("destination") == dest}
tree = {}
for rec in filter(None, git("ls-tree", "-r", "-z", ref).split(b"\0")):
    meta, path = rec.split(b"\t", 1)
    mode, _type, oid = meta.decode().split()
    tree[path.decode()] = (mode, oid)
missing = sorted(set(rows) - set(tree))
extra = sorted(set(tree) - set(rows))
bad = sorted(p for p, r in rows.items() if p in tree and (
    tree[p][0] != str(r["git_mode"])
    or hashlib.sha256(git("cat-file", "blob", tree[p][1])).hexdigest() != r["sha256"]))
print(f"{dest}: {len(rows)} row(s); {len(tree)} path(s) at {ref}; "
      f"missing {len(missing)}, extra {len(extra)}, blob/mode mismatch {len(bad)}")
for label, ps in (("MISSING", missing), ("EXTRA", extra), ("MISMATCH", bad)):
    for p in ps:
        print(f"  {label} {p}")
sys.exit(1 if (missing or extra or bad) else 0)
PY

# 3. the DECLARED-EDIT LAYER: every difference from the pure carve is declared
#    usage: DEST MANIFEST CARVE_REF BASE_REF HEAD_REF [--may-change P]... [--added P]...
#    run from inside the destination clone
#    It reads changed lines from `git diff -U0` hunk headers, so its answer
#    depends on how the diff aligns the two texts, and it pins
#    --diff-algorithm=histogram rather than inherit git's default. Under the
#    default, an undeclared blank line between two declared runs can be folded
#    into one replaced hunk and refused, although a blank line still stands
#    there. On the code leg the default refused lines 182, 255 and 2559 of the
#    validator; histogram and helper 5 both accepted them.
cat > "$WORK/bin/declared-edits.py" <<'PY'
import re, subprocess, sys, yaml
dest, manifest, carve, base, head = sys.argv[1:6]
allowed = {"--may-change": set(), "--added": set()}
rest = sys.argv[6:]
while rest:
    allowed[rest[0]].add(rest[1])
    rest = rest[2:]
def git(*a):
    return subprocess.run(["git", *a], check=True, capture_output=True).stdout
def tree(ref):
    out = {}
    for rec in filter(None, git("ls-tree", "-r", "-z", ref).split(b"\0")):
        meta, path = rec.split(b"\t", 1)
        out[path.decode()] = meta.decode()          # "<mode> <type> <oid>"
    return out
doc = yaml.safe_load(open(manifest, encoding="utf-8"))
rows = {r["destination_path"]: r for r in doc["rows"] if r.get("destination") == dest}
t_carve, t_base, t_head = tree(carve), tree(base), tree(head)
hunk = re.compile(rb"^@@ -(\d+)(?:,(\d+))? \+\d+(?:,\d+)? @@", re.M)
refusals, applied, unapplied = [], 0, 0
for p, r in sorted(rows.items()):
    declared = {n for e in r.get("edits") or [] for n in e["lines"]}
    if p not in t_head:
        refusals.append(f"carved path deleted: {p}")
        continue
    if t_head[p] == t_carve[p]:
        unapplied += bool(declared)
        continue
    if not declared:
        refusals.append(f"verbatim row changed: {p}")
        continue
    before = len(refusals)
    if t_head[p].split()[0] != t_carve[p].split()[0]:
        refusals.append(f"mode changed: {p}")
    undeclared = set()
    diff = git("diff", "-U0", "--diff-algorithm=histogram", "--no-ext-diff", "--no-textconv",
               carve, head, "--", p)
    for m in hunk.finditer(diff):
        start, count = int(m.group(1)), int(m.group(2) or 1)
        if count:                                   # old lines start..start+count-1 replaced or removed
            undeclared |= set(range(start, start + count)) - declared
        elif not {start, start + 1} & declared:     # pure insertion after old line `start`
            undeclared.add(start)
    if undeclared:
        refusals.append(f"undeclared line(s) in {p}: {sorted(undeclared)}")
    applied += len(refusals) == before
for p in sorted(set(t_head) - set(rows)):
    if p in t_base:
        if t_head[p] != t_base[p] and p not in allowed["--may-change"]:
            refusals.append(f"changed outside the carve, not declared: {p}")
    elif p not in allowed["--added"]:
        refusals.append(f"added, not declared: {p}")
for p in sorted((set(t_base) | set(rows)) - set(t_head)):
    if p not in rows:
        refusals.append(f"deleted: {p}")
for p in refusals:
    print(f"REFUSE {p}")
print(f"{dest}: {len(rows)} carved row(s); {applied} edited on declared lines only; "
      f"{unapplied} declaring edits left unapplied; {len(refusals)} refusal(s)")
sys.exit(2 if refusals else 0)
PY

# 4. the CONTROL: the eight owned digests recomputed at the carve commit
cat > "$WORK/bin/control.py" <<'PY'
import hashlib, subprocess, sys, yaml
carve, repo = sys.argv[1:3]
def show(spec):
    return subprocess.run(["git", "-C", repo, "show", spec], check=True, capture_output=True).stdout
contracts = yaml.safe_load(show(f"{carve}:contracts/manifest.yaml"))["contracts"]
owned = [c for c in contracts if c.get("sha256") and c.get("member_class", "owned") == "owned"]
ok = 0
for c in owned:
    got = hashlib.sha256(show(f"{carve}:{c['path']}")).hexdigest()
    ok += got == c["sha256"]
    print("match   " if got == c["sha256"] else "MISMATCH", c["id"], got)
print(f"control: {ok}/{len(owned)} owned digest(s) recomputed equal at {carve[:12]}")
sys.exit(0 if ok == len(owned) == 8 else 1)
PY

# 5. the DECLARED LINES, with no diff algorithm: the authority when it and
#    helper 3 disagree about a line (see "What a line is" below)
#    usage: DEST MANIFEST CARVE_REF HEAD_REF
#    run from inside the destination clone
cat > "$WORK/bin/declared-lines-exact.py" <<'PY'
"""Alignment-independent declared-line check (no diff algorithm involved).

For every moved row of DEST, compare the carve-layer blob with HEAD's:
- a verbatim row must be byte-identical;
- a declared-edit row must read U0 X1 U1 X2 ... Un, where U0..Un are the
  maximal runs of the carve blob's UNDECLARED lines, unchanged and in order,
  and each Xi is whatever now stands where the i-th run of declared lines
  stood (possibly nothing). A line is a \\n-terminated record of the blob.
usage: DEST MANIFEST CARVE_REF HEAD_REF   (run inside the destination clone)
"""
import subprocess, sys, yaml
from functools import lru_cache
dest, manifest, carve, head = sys.argv[1:5]
def blob(ref, path):
    r = subprocess.run(["git", "show", f"{ref}:{path}"], capture_output=True)
    return r.stdout if r.returncode == 0 else None
doc = yaml.safe_load(open(manifest, encoding="utf-8"))
bad = 0
for row in doc["rows"]:
    if row.get("destination") != dest:
        continue
    p = row["destination_path"]
    old, new = blob(carve, p), blob(head, p)
    declared = {n for e in row.get("edits") or [] for n in e["lines"]}
    if not declared:
        if old != new:
            print(f"REFUSE verbatim row changed: {p}"); bad += 1
        continue
    o, n = old.split(b"\n"), new.split(b"\n")       # last element: after final \n
    segs, cur, kind = [], [], None                   # [("U", lines) | ("D", count)]
    for i, line in enumerate(o[:-1], start=1):
        k = "D" if i in declared else "U"
        if k != kind and cur:
            segs.append((kind, cur)); cur = []
        kind = k; cur.append(line)
    segs.append((kind, cur))
    tail_o, tail_n = o[-1], n[-1]
    body = n[:-1]
    @lru_cache(maxsize=None)
    def fit(si, pos):
        if si == len(segs):
            return pos == len(body)
        k, lines = segs[si]
        if k == "U":
            m = len(lines)
            return body[pos:pos + m] == lines and fit(si + 1, pos + m)
        return any(fit(si + 1, q) for q in range(pos, len(body) + 1))
    sys.setrecursionlimit(100000)
    ok = fit(0, 0) and tail_o == tail_n
    runs = sum(1 for k, _ in segs if k == "D")
    print(f"{'ok    ' if ok else 'REFUSE'} {p}: {len(declared)} declared line(s) in {runs} run(s); "
          f"{sum(len(l) for k, l in segs if k == 'U')} undeclared line(s) preserved in order: {ok}")
    bad += not ok
print(f"{dest}: {bad} refusal(s)")
sys.exit(2 if bad else 0)
PY
```

**What a line is.** The manifest's `edits[].lines` use the line numbers of the
blob at the carve commit, as `git diff` and `grep -n` number them. Helper 3
reads them from `git diff -U0 --diff-algorithm=histogram` hunk headers, so it
shares that numbering. A modified or removed line must be declared. A pure
insertion must sit next to a declared line (hunk (e) adds its extension points
exactly where hunks (c) and (d) remove code).

**Helper 5 is the authority on a declared line.** Helper 3 judges a line by
where a diff puts it, and two diff algorithms can place one edit differently.
Helper 5 runs no diff. It cuts each carved blob into runs of declared and
undeclared lines, and requires every undeclared run to stand in the new blob
unchanged and in order, with anything, or nothing, where each declared run
stood. Where helper 3 and helper 5 disagree about a line, helper 5's answer
stands. It judges only the lines of carved rows: a mode change, a deleted path
and a path outside the carve remain helper 3's. Helper 5 was added at
realization, after the refusal described at helper 3, so the rehearsal record
below predates it.

### One carve, per destination: the mirror and the filter

These five steps are the same for every destination, and they produce the
destination's **carve layer**: the branch `carve-src` in a fresh mirror, holding
exactly that destination's rows with their full history.

```bash
DEST=openwallet_code          # or openwallet_spec, or openwallet_root

# (i) a FRESH MIRROR, one per destination. Never the shared checkout, and never
#     a worktree of it. git-filter-repo refuses a clone that does not look fresh,
#     and a mirror is the shape that passes without --force. A mirror used for
#     one destination is not reused for the next. --no-local matters only when
#     SRC_URL is a path on disk: a local clone hard-links objects and is then
#     not "fresh" in filter-repo's sense.
git clone --mirror --no-local "$SRC_URL" "src-$DEST.git"

# (ii) the manifest verifies at the carve commit. Pass --manifest explicitly:
#      without it the checker looks for the manifest inside the mirror, finds
#      no working tree, prints `NO MANIFEST` and exits 0, having checked nothing.
python3 "$OXW/scripts/validate-carve-manifest.py" \
    --repo "src-$DEST.git" --at "$CARVE_COMMIT" --manifest "$MANIFEST"

# (iii) the destination's paths, then ONE exact --path per row: no globs, no
#       --path-rename. `--path` takes a literal path, and a file path matches
#       only that file.
python3 bin/carve-paths.py "$DEST" "$MANIFEST" > "paths-$DEST.txt"
args=(); while IFS= read -r p; do args+=(--path "$p"); done < "paths-$DEST.txt"

# (iv) rewrite a NAMED ref at the carve commit, and only that ref. `--refs` takes
#      refs, and a bare object id is not one: given `--refs "$CARVE_COMMIT"`,
#      the rewrite lands on no ref at all (measured in openxFactory's openDox
#      carve). Full history: everything reachable from the carve commit is
#      rewritten, nothing is squashed.
git -C "src-$DEST.git" branch carve-src "$CARVE_COMMIT"
git -C "src-$DEST.git" filter-repo --refs carve-src "${args[@]}"

# (v) de-fang the mirror. With --refs, filter-repo KEEPS `origin`, and the
#     mirror's origin is openXwallet itself. Removing origin BEFORE the filter
#     makes filter-repo refuse ("expected one remote, origin"), so it is removed
#     here, after the rewrite. The mirror's other refs, including openXwallet's
#     `wallet-v*` tags, are left unfiltered. That is why a destination fetches
#     ONE ref, by refspec, with --no-tags. In a mirror, `remote remove` prints
#     a note listing the branches it did not delete. That note is expected.
git -C "src-$DEST.git" remote remove origin
python3 bin/carve-layer.py "$DEST" "$MANIFEST" "src-$DEST.git" carve-src
git -C "src-$DEST.git" rev-list --count carve-src
```

---

## Phase 0 — preconditions and the CONTROL (task 4.1)

**ROLLBACK (written first): nothing has happened.** Delete `$WORK`. No
repository has changed, and openXwallet is not touched by this or any later
phase of this runbook.

| # | Precondition | How it is shown |
| --- | --- | --- |
| 0.1 | The birth commits (tasks 3.4-3.6) have landed on each repository's `main` | `git log` in each. The root's leg pins still name the scaffold commits `72eca87cedbf79de110abfb903ecf3482ed2841d` (spec) and `9cabda85f8c59d317eee6287e4201946ced2b8a3` (code), and `make bootstrap` in a fresh recursive clone of the root is ok. For each leg it reports that `origin/main` is ahead of the pin, "which the pin deliberately does NOT follow". That is expected, and nothing moves the pins before Phase 3 |
| 0.2 | openXwallet's `carve-manifest` check is green on its `main` | the check run. It recomputes every moved row's digest and fails if anything under the carve surface has changed since the carve commit |
| 0.3 | The manifest verifies at the carve commit, from a fresh mirror | step (ii) above prints `OK … 232 row(s) at opensoft/openXwallet@90111df262d6 … 128 digest(s) recomputed; 1884 declared edit line(s) on 8 row(s); 232 tracked path(s) at the carve commit, each in exactly one row` *(as executed against the amended manifest at `64ca6eac`: the checker prints `1892 declared edit line(s) on 9 row(s)`)* |
| 0.4 | `git filter-repo --version` answers | the rehearsal ran 2.47.0 (`a40bce548d2c`) |
| 0.5 | The spec leg's `openspec-cli-pin` check has reported once (on its birth pull request) | the check run on the birth pull request |
| 0.6 | No ruleset that applies to these repositories requires a linear history or forbids merge commits. An organisation ruleset may already cover them before Phase 5 creates theirs | read the rules in force on each `main`. Phases 1-3 land MERGE COMMITS (see "Landing"), and a rule forbidding them blocks the carve |

**If 0.2 or 0.3 refuses** with `carve-digest-mismatch`, `carve-file-undeclared`
or `carve-path-absent`, the carve commit is stale. **STOP.** Do not carve
against a refused manifest, and never edit a digest to make the checker pass.
Re-cutting the carve commit is Brett Heap's act. It means a new commit, a
re-emitted manifest with every digest recomputed, and every record of it
updated.

**The control.** Before anything is carved, recompute the eight owned digests
in openXwallet's `contracts/manifest.yaml` over the bytes at the carve commit.
Without the control, a later match would prove the manifest stale rather than
the carve faithful.

```bash
git clone --mirror --no-local "$SRC_URL" control.git
python3 bin/control.py "$CARVE_COMMIT" control.git      # expect: control: 8/8 … ; exit 0
```

| # | id | sha256 at the carve commit (rehearsed: 8/8 match) |
| --- | --- | --- |
| 1 | `openxwallet-record` | `20ba39c07564c93b8ffe47382126677a165771244d28fb0c4976ab950173c40a` |
| 2 | `openxwallet-custody-registry-schema` | `df72638497a7f90c2a4dff47c429cb794bc4b6e270ce2dd2b17116478ae3b51a` |
| 3 | `openxwallet-custody-registry` | `94d631d6ee76dab015628a1856afd82582b98d6a3733622c9afe8b13b5278539` |
| 4 | `openxwallet-grant` | `fde433c5821e2e6f62926a72c58a67a784961d2e9e27e9f2b3520fcc8e738e88` |
| 5 | `openxwallet-grant-exercise` | `f16ad31246186cec36e142ae39bd831d98fbc5c0afd48685057bc39e113c8858` |
| 6 | `openxwallet-distinct-holder-constraint` | `c2a6d2fd23fb3743fdaf0e165dabc4cb1dff24e52a8262a38c86ed1482374b25` |
| 7 | `openxwallet-subject-attestation` | `d29eca519462aff7871de3786f19c820e9fc3b95115ce30e57d1f1cc2bc0c0b2` |
| 8 | `openxwallet-agent-composition` | `aed3978e8ae952f3ff5b3de1f672bba5da350d5aaeb442feafaa870b4de4be91` |

---

## Phase 1 — the CODE leg: carve, then its declared edits (tasks 4.2, 4.4)

**ROLLBACK (written first): close the pull request. If it has merged, revert
its merge commit on `opensoft/openWallet-code` `main`, and delete `$WORK`.**
Nothing pins the code leg's new commits until Phase 3. The root still pins
the scaffold commit, so a reverted arrival leaves exactly the birth state.
openXwallet is untouched.

**1a. The carve layer.** Run the five steps with `DEST=openwallet_code`.
Rehearsed result: `openwallet_code: 80 row(s); 80 path(s) at carve-src; missing
0, extra 0, blob/mode mismatch 0`, and 31 commits of history. Both `examples/`
prefixes must be present at their exact paths: `contracts/openxwallet/examples/`
and `contracts/openxwallet-agent-profile/examples/`. The validator's corpus
exclusion keys on them, so a flattened prefix would re-adjudicate the
intended-invalid negatives as live records. The negatives number 38 under the
first prefix and 4 under the second: 41 + 4, less the three `grant-review-*`
negatives that stay in openXwallet.

**1b. Commit A, the arrival, a pure carve.** On a branch of the leg, never on
`main`:

```bash
git clone https://github.com/opensoft/openWallet-code.git dest-code
cd dest-code || exit 1
git switch -c carve/code-arrival
git remote add carved "../src-$DEST.git"
git fetch --no-tags carved carve-src:refs/remotes/carved/carve-src
git merge --allow-unrelated-histories --no-edit \
    -m "Carve the openwallet_code rows from opensoft/openXwallet@$CARVE_COMMIT (commit A, byte-identical)" \
    carved/carve-src

git diff --stat HEAD^2 HEAD -- $(cat "../paths-$DEST.txt")                      # EMPTY: the carved paths are the carve layer's
git diff --stat HEAD^1 HEAD -- . $(sed 's/^/:!/' "../paths-$DEST.txt")          # EMPTY: nothing of the leg's own changed
python3 ../bin/declared-edits.py "$DEST" "$MANIFEST" HEAD^2 HEAD^1 HEAD         # 0 refusals; 3 declaring edits left unapplied
python3 ../bin/declared-lines-exact.py "$DEST" "$MANIFEST" HEAD^2 HEAD          # 0 refusal(s)
```

Rehearsed against the code leg's birth branch: both `diff`s were empty. Helper 3
reported `80 carved row(s); 0 edited on declared lines only; 3 declaring edits
left unapplied; 0 refusal(s)`. *(As executed against the amended manifest at
`64ca6eac`, the code leg declares edits on 4 rows, so commit A leaves 4
declaring edits unapplied, not 3, in the expected line above and here.)*

**Commit A is RED by construction, and that is measured, not feared.** Run from
the leg's own root at commit A, the rehearsal gave:
- `wallet-yaml-syntax-gate.py .` exits 0;
- `validate-openxwallet.py .` exits 2, with `contracts/schemas/hermes-job-envelope.schema.yaml
  not found; the approval-scope vocabulary is read from the canonical job
  envelope`, because the envelope does not travel;
- `python3 -m pytest tests/ -q` gives 30 failed, 12 passed, 1 skipped.

Commit B is what turns the leg green, so **A and B are ONE pull request, CI
judges its head, and A is never merged alone.**

**1c. Commit B, the declared-edit layer, one auditable diff.** On top of A, in
the same pull request. Line numbers are those of the carve-commit blob:

- `scripts/validate-openxwallet.py`, hunks (a)-(e):
  - (a) removes the envelope: `ENVELOPE_SCHEMA_PATH` (:254), the hard exit when
    it is absent (:3498-3503) and the vocabulary note (:3529-3530);
  - (b) takes the vocabulary from ONE DECLARED BINDING the caller supplies,
    refused when absent (RULED Q6): rule (g)'s envelope sentences (:73-78),
    `approval_policy_vocabulary()` (:422-428) and its read in `main` (:3507);
  - (c) moves rule (t) out to the adapter: its docstring (:172-181), constants
    (:256-283), the OXWR-R1/R2 rows (:323-328), the check inside `check_grant`
    (:986-1032) and its self-test probes (:1789-1974);
  - (d) moves the register reader out to the adapter: rule (u)'s docstring
    (:183-212), the S4 self-test (:2036-2558), the reader (:2561-3326) and its
    call in `repo_scan` (:3464-3465);
  - (e) adds the declared, EMPTY-by-default extension points at the anchors (c)
    and (d) vacate (:986, :1789, :2036, :3464). It adds lines and removes none
    (RULED Q1).
- `tests/nested_repo_prune/test_prune_and_register_note.py`, **the test split**.
  The prune half travels and the register half stays. The docstring's account
  of the two behaviours (:1, :4-7), the register-note patterns (:40-42) and the
  US2 block (:247-408) leave this copy.
- `.github/workflows/wallet-validation.yml`, **the envelope-verify step** and
  its comment block (:44-51).
- **Declared additions:** the corpus binding (Q6) and `LICENSE`.

```bash
python3 ../bin/declared-edits.py "$DEST" "$MANIFEST" HEAD~1^2 HEAD~1^1 HEAD \
    --added LICENSE --added <the corpus binding's path>
# expect: 80 carved row(s); 3 edited on declared lines only; 0 declaring edits left unapplied; 0 refusal(s)
python3 ../bin/declared-lines-exact.py "$DEST" "$MANIFEST" HEAD~1^2 HEAD
# expect: openwallet_code: 0 refusal(s)
```

*(As executed against the amended manifest at `64ca6eac`: 4 edited on declared
lines only, not 3. The fourth row is
`tests/multi_key_wallets/test_declared_key_sets.py` (:108-111, :117-118), and
the test split also takes the pinned corpus note (:47-48) of the prune test.)*

A line in no declared hunk, or a path that is neither carved nor declared,
REFUSES. In the rehearsal, a one-line undeclared change and one stray file
printed `REFUSE undeclared line(s) in …: [11]` and `REFUSE added, not declared:
stray.txt`, and the helper exited 2.

**1d. The checks.** `wallet-validation` and `pytest-suite` run on the pull
request, from INSIDE the leg, with the carved workflows. They must be green on
the head. A wallet run from the assembly root prunes both legs and scans
nothing (exit 0; measured in D0). It is never a gate.

**1e. Land it with a MERGE COMMIT** (see "Landing"). The leg's `main` then
carries the carved history, A and B.

---

## Phase 2 — the SPEC leg: carve, then its declared edits (tasks 4.3, 4.4)

**ROLLBACK (written first): close the pull request. If it has merged, revert
its merge commit on `opensoft/openWallet-spec` `main`, and delete `$WORK`.**
Nothing pins the spec leg's new commits until Phase 3. openXwallet is
untouched.

Phases 1 and 2 are independent. Either may go first, and both precede Phase 3.

**2a. The carve layer.** Run the five steps with `DEST=openwallet_spec`.
Rehearsed result: `openwallet_spec: 38 row(s); 38 path(s) at carve-src; missing
0, extra 0, blob/mode mismatch 0`, and 33 commits.

**2b. Commit A.** This is 1b with `dest-spec`, `carve/spec-arrival` and
`opensoft/openWallet-spec`. The merge meets `openspec/config.yaml` on both sides
as the same blob. **Rehearsed against the spec leg's birth branch, the merge
was clean**, both `diff`s were empty, and helper 3 reported `38 carved row(s); 0
edited …; 4 declaring edits left unapplied; 0 refusal(s)`.

**2c. Commit B, the declared-edit layer.** `openXwallet` becomes `openWallet` on
exactly these lines, and on no other:

| File (at the carve commit) | Lines |
| --- | --- |
| `openspec/specs/openxwallet/spec.md` | 10, 59, 80, 102, 139, 175, 206, 227: the eight requirement subjects |
| `openspec/specs/openxwallet-agent-profile/spec.md` | 8, 29, 52: the three requirement subjects |
| `openspec/changes/add-composition-drift-cascade/specs/openxwallet/spec.md` | 7, 36 |
| `openspec/changes/add-composition-drift-cascade/specs/openxwallet-agent-profile/spec.md` | 7 |

Under the ruling "keep the prefix", no capability id, `kind:`, finding code or
file name moves. The one declared addition is `LICENSE`.

```bash
python3 ../bin/declared-edits.py openwallet_spec "$MANIFEST" HEAD~1^2 HEAD~1^1 HEAD --added LICENSE
# expect: 38 carved row(s); 4 edited on declared lines only; 0 declaring edits left unapplied; 0 refusal(s)
python3 ../bin/declared-lines-exact.py openwallet_spec "$MANIFEST" HEAD~1^2 HEAD
# expect: openwallet_spec: 0 refusal(s)
```

**2d. The gate.** The leg's `openspec-cli-pin` check runs on the pull request.
**Rehearsed with the fourteen lines and `LICENSE` applied, the gate's own
command printed `Totals: 3 passed, 0 failed (3 items)` and `OK
openspec-cli-pin`, exit 0.** The three items are the two promoted specs and
`add-composition-drift-cascade`. In the same rehearsal, helper 3 run without
`--added LICENSE` refused `added, not declared: LICENSE` and exited 2.

**2e. Land it with a MERGE COMMIT.**

---

## Phase 3 — the ROOT: its carve layer, the manifest field edits, both gitlinks and both pins in ONE commit (task 4.5)

**ROLLBACK (written first): close the pull request. If it has merged, revert
the one root commit.** The legs keep their arrivals and are pinned by nothing
else. Nothing outside this repository reads the root yet: openXwallet mounts it
only in its adapter rebuild.

Run this only after Phases 1 and 2 have LANDED on the legs' `main`. The pins
then name commits that exist upstream.

**3a. The carve layer.** Run the five steps with `DEST=openwallet_root`.
Rehearsed result: `openwallet_root: 10 row(s); 10 path(s) at carve-src; missing
0, extra 0, blob/mode mismatch 0`, and 16 commits. None of the 10 paths exists
in the root's own tree. `docs/` holds only this runbook, and the scaffold wrote
no `LICENSE`.

**3b. The one commit.** It merges the root's carve layer, applies the manifest
field edits, and moves each leg's gitlink with its `contracts/<role>-pin.yaml`.
That is the lockstep invariant, in one commit:

```bash
git clone --recurse-submodules https://github.com/opensoft/openWallet.git dest-root
cd dest-root || exit 1
git switch -c carve/root-arrival
git -C spec fetch origin main && git -C code fetch origin main
SPEC_SHA=$(git -C spec rev-parse origin/main); CODE_SHA=$(git -C code rev-parse origin/main)
git -C spec checkout -q "$SPEC_SHA" && git -C code checkout -q "$CODE_SHA"
git -C spec cat-file -t "$SPEC_SHA"; git -C code cat-file -t "$CODE_SHA"   # each must print: commit

digest() { python3 -c 'import sys; from pathlib import Path; sys.path.insert(0, "scripts"); import repo_shape; print(repo_shape.tree_digest(Path(sys.argv[1]), sys.argv[2]))' "$1" "$2"; }
SPEC_DIGEST=$(digest spec "$SPEC_SHA"); CODE_DIGEST=$(digest code "$CODE_SHA")

git remote add carved "../src-$DEST.git"
git fetch --no-tags carved carve-src:refs/remotes/carved/carve-src
git merge --no-commit --allow-unrelated-histories carved/carve-src

sed -i -E "s/^commit: \"[0-9a-f]{40}\"/commit: \"$SPEC_SHA\"/; s/^  tree_sha256: \"[0-9a-f]{64}\"/  tree_sha256: \"$SPEC_DIGEST\"/" contracts/spec-pin.yaml
sed -i -E "s/^commit: \"[0-9a-f]{40}\"/commit: \"$CODE_SHA\"/; s/^  tree_sha256: \"[0-9a-f]{64}\"/  tree_sha256: \"$CODE_DIGEST\"/" contracts/code-pin.yaml
# then the manifest field edits to contracts/manifest.yaml (below), by hand
git add spec code contracts/spec-pin.yaml contracts/code-pin.yaml contracts/manifest.yaml
git commit -m "Carve the openwallet_root rows from opensoft/openXwallet@$CARVE_COMMIT and pin both legs at their carve, in one commit"
```

Git records a gitlink without checking that the object exists in the
submodule, so a wrong pin commits and pushes clean. The `cat-file -t` lines are
what catch that.

`tree_digest` is the root's own `scripts/repo_shape.py` definition,
`sorted-ls-tree-r-v1`, which `validate-pins.py` recomputes. No workflow in
this root names a leg by `@<sha>` at the scaffold commit. If one has been added
since, it moves in this same commit.

**The manifest field edits**, at the lines the carve-commit blob has them:
- `carved_from:` (:52-54) names `opensoft/openXwallet` at
  `90111df262d6f54f7e82651d860adc12345f83f4`;
- each of the eight owned rows' `path:` gains `code/` (it then names the bytes
  the root's own `code` gitlink holds), and its `source_path:` changes with it
  (:76-77, :106-107, :119-120, :132-133, :145-146, :158-159, :171-172,
  :184-185);
- the consumed `hermes-job-envelope` row and its comment block are removed
  (:197-244). The envelope does not travel.

The exact `source_path:` spelling is realization's to fix.

**3c. Verify, before pushing.**

```bash
make validate                                    # names, manifest, lockstep pins: "pins ok"
python3 ../bin/declared-edits.py openwallet_root "$MANIFEST" HEAD^2 HEAD^1 HEAD \
    --may-change spec --may-change code --may-change contracts/spec-pin.yaml --may-change contracts/code-pin.yaml
# expect: 10 carved row(s); 1 edited on declared lines only; 0 declaring edits left unapplied; 0 refusal(s)
python3 ../bin/declared-lines-exact.py openwallet_root "$MANIFEST" HEAD^2 HEAD
# expect: openwallet_root: 0 refusal(s)

python3 - <<'PY'
# part one (b), the THIRD way: the root manifest's owned rows equal the code leg's bytes
import hashlib, subprocess, yaml
contracts = yaml.safe_load(open("contracts/manifest.yaml", encoding="utf-8"))["contracts"]
owned = [c for c in contracts if c.get("sha256") and c.get("member_class", "owned") == "owned"]
ok = 0
for c in owned:
    assert c["path"].startswith("code/"), c["path"]
    blob = subprocess.run(["git", "-C", "code", "show", "HEAD:" + c["path"][len("code/"):]],
                          check=True, capture_output=True).stdout
    ok += hashlib.sha256(blob).hexdigest() == c["sha256"]
print(f"three-way: {ok}/{len(owned)} root-manifest digest(s) equal the code leg's bytes; consumed rows left: "
      f"{sum(1 for c in contracts if c.get('member_class') == 'consumed')}")
PY
# expect: three-way: 8/8 …; consumed rows left: 0
```

**This is where the root's declared-edit layer is audited.** The commit is a
merge, and its second parent is the pure carve layer:
- `git diff HEAD^2 HEAD -- contracts/manifest.yaml` is the manifest's declared
  edit, and helper 3 holds it to the 67 declared lines;
- `git diff HEAD^1 HEAD -- spec code contracts/spec-pin.yaml contracts/code-pin.yaml`
  is the lockstep move.

So one commit still yields one auditable diff for the declared edits.

**Rehearsed end to end.** The rehearsal used the rehearsal legs as the
submodules, and applied the field edits with a rehearsal spelling of
`source_path:`:
- `validate-pins.py` printed `pins ok`, and `make validate` passed;
- helper 3 printed `10 carved row(s); 1 edited on declared lines only; 0
  declaring edits left unapplied; 0 refusal(s)`;
- the three-way check printed `8/8 … consumed rows left: 0`;
- a further commit that moved the `code` gitlink ALONE was refused:
  `FINDING pin-gitlink-mismatch: code: gitlink … != contracts/code-pin.yaml
  commit …`, exit 1.

**3d. Land it with a MERGE COMMIT.** `validate` must be green on the pull
request.

---

## Phase 4 — the PROOF, a declared path mapping (task 4.6)

**ROLLBACK (written first): revert the commit that adds the proof document.**
Nothing is tagged yet, and no leg changes.

`docs/byte-identity-<first openWallet tag>.md`, at this root. Every part can
fail, and each names the command above that produces it:

| Part | Claim | Produced by |
| --- | --- | --- |
| zero | the CONTROL: the eight recorded sha256s recomputed at the carve commit, 8/8 | `bin/control.py` (Phase 0) |
| one (a) | the MAPPING is total and functional: every tracked path at the carve commit sits in exactly one row, every moved row's `destination_path` equals its `source_path`, and per destination the carve layer's sorted listing equals that destination's rows. Counts: 80 / 38 / 10, with both `examples/` prefixes preserved | `validate-carve-manifest.py` (step (ii)), then `bin/carve-layer.py` per destination |
| one (b) | the eight digests THREE-WAY: the carve-commit manifest = the bytes at `contracts/…` in the code leg = this root's manifest rows at `code/contracts/…` | `bin/control.py`, `bin/carve-layer.py` (code), and the three-way check (3c) |
| two (a) | per destination, git blob + mode identity 100% at the carve layer, recorded per path | `bin/carve-layer.py`, and helper 3's report at each commit A |
| two (b) | the declared-edit layer: every changed line falls in its declared class, and every added path is a declared addition. A line or path in no class REFUSES | `bin/declared-edits.py` and `bin/declared-lines-exact.py` at 1c, 2c and 3c |
| three | behaviour, run from the CODE leg's own root: openWallet standalone reports 21 / 42 / 11 of 11 and refuses a posture under no binding, and D5's neutrality gate is empty over the composed adapter | the code leg's validator and tests, from `code/`; the neutrality gate, from openXwallet (see below) |
| four | every verifier observed REFUSING a mutated input before it is trusted. That includes a root whose `code` gitlink and `contracts/code-pin.yaml` disagree | the negatives recorded in this runbook, re-run for the proof: a mutated blob in a carve layer, an undeclared line, an undeclared file, a gitlink moved alone, and the spec leg's mutated tarball |
| five | the shape's `validate` green at the root: names, manifest, lockstep pins | `make validate` at the landed root commit |

**Part four must be re-run, not cited.** A refusal observed in a rehearsal
proves the helper refuses. It does not prove that the proof's run used a helper
that refuses.

**One sequencing question this runbook does not decide.** D7 puts "D5's
neutrality gate is empty over the composed adapter" inside part three, and so
before the tag. The Migration plan builds the composed adapter in step 6, after
the tag, where task 5.4 runs that gate. Part three's adapter half can only run
against the adapter's pull-request branch, pinning this root's untagged commit,
or else move to step 6. That choice belongs to the plan and to the operator.

---

## Phase 5 — three rulesets: EVALUATE, then ACTIVE (task 4.7) [OPERATOR]

**ROLLBACK (written first): set the ruleset back to `evaluate`, or delete it.**
Neither act touches a commit.

| Repository | Required check(s) | First reported on |
| --- | --- | --- |
| `opensoft/openWallet` (root) | `validate` | every pull request since the scaffold |
| `opensoft/openWallet-spec` | `openspec-cli-pin` | the spec leg's birth pull request (task 3.6) |
| `opensoft/openWallet-code` | `wallet-validation`, `pytest-suite` | the Phase 1 pull request, where the carved workflows first run |

In `opensoft` the rulesets are organisation-sourced, so each one is an
**org-admin act**, and `scaffold-project.py` creates none. Each ruleset:
- targets `~DEFAULT_BRANCH`;
- has one `required_status_checks` rule naming the contexts above;
- is created in **EVALUATE**;
- is promoted to **ACTIVE** only once each of its checks has reported in that
  repository.

**Day-one REQUIRED is impossible.** GitHub cannot require a status check that
has never reported in the repository, so the context cannot be selected until a
workflow has reported under it once. Where a check has not yet reported, one
trivial pull request makes it report (openXwallet's runbook used a README
touch). Then promote it, and read the result back from
`repos/opensoft/<repository>/rules/branches/main`.

Keep the merge-commit method allowed, and do not require a linear history,
until Phases 1-3 have landed (precondition 0.6).

---

## Phase 6 — the first release, on the ROOT (task 4.9) [OPERATOR]

**ROLLBACK (written first): delete the tag, locally and on the remote, but
ONLY before anything pins it.** After that, the honest reversal is a following
release, never a deleted tag.

**Only after the proof (Phase 4) is green.** A release is five coordinated
values, realized across one root commit and the leg commits it pins:
- the annotated `wallet-v*` tag on the root commit that pins both legs;
- `contracts/manifest.yaml` and `contracts/CHANGELOG.md` at the root, with
  `contracts/releases/` beside them;
- each artifact's per-file `contract_schema_version`, inside its bytes in the
  code leg;
- the release commit with its per-file digests;
- the `contracts/CHANGELOG.md` entry.

**No leg is tagged**, because a tag on a leg describes half a project. That is
also why every fetch above passes `--no-tags`: the mirrors still carry
openXwallet's `wallet-v1.0`…`wallet-v1.5`, and the rehearsal legs ended with 0
tags. The version number is allocated here, not before.

```bash
git tag -a wallet-v<major>.<minor> -m "openWallet wallet-v<major>.<minor>: the first release on the root, pinning both legs" <the root commit>
git push origin wallet-v<major>.<minor>
```

---

## Landing

Phases 1, 2 and 3 each land as a **pull request merged with a merge commit**.
Never squash and never rebase. A squash would flatten the carved history and
the A/B split into one commit, and would lose the second parent that makes the
root's declared-edit layer auditable. A rebase cannot carry an
unrelated-histories merge. The scaffold's `main` is never rewritten and never
force-pushed. These repositories accept changes by pull request only, and
`AGENTS-shape.md` forbids `--admin`. Each pull request is merged on Brett
Heap's word.

## Rollback, collected per phase

| Phase | Rollback (written before the phase) | Cost |
| --- | --- | --- |
| 0 — preconditions, control | delete `$WORK` | zero; nothing has changed |
| 1 — code leg carve + edits | close the pull request, or revert its merge on the leg; delete `$WORK` | zero; nothing pins the leg's new commits yet |
| 2 — spec leg carve + edits | the same, on the spec leg | zero |
| 3 — the root's one commit | close the pull request, or revert the root commit | zero outside the root; nothing reads it yet |
| 4 — the proof | revert the proof commit | zero |
| 5 — rulesets | set back to `evaluate`, or delete | zero commits touched |
| 6 — the tag | delete it, ONLY before anything pins it | after that, a following release, never a revert |

**The arc-wide rollback:** delete the three repositories. Nothing pins them, the
carve copied, and openXwallet is untouched (Migration plan steps 3 and 4).

## Brett Heap's acts, collected

| # | Act | Phase |
| --- | --- | --- |
| 1 | Merging each carve pull request: the two legs, then the root | 1, 2, 3 |
| 2 | Re-cutting the carve commit, if precondition 0.2 or 0.3 refuses | 0 |
| 3 | The three rulesets, EVALUATE then ACTIVE (org-admin) | 5 |
| 4 | The first tag and its version number | 6 |

**The lane's, as pull requests:** the arrival commits and declared edits on the
legs, the root's one lockstep commit, and the proof. None of them merges
without act 1.

## The rehearsal record

Rehearsed 2026-10-08 by lane `openXwallet-2`, with git 2.43.0 and
git-filter-repo 2.47.0, in a scratch directory. The source was a fresh
`--mirror --no-local` of openXwallet. The destinations were clones of each
repository's `birth/group-3` branch, so precondition 0.1 was simulated rather
than met. The four helpers were extracted from this file's own text and run as
extracted, so the helpers printed above are the helpers that ran. The root's
manifest field edits used a rehearsal spelling of `source_path:`.

| Step | Printed |
| --- | --- |
| manifest checker at the carve commit (step ii) | `OK … 232 row(s) … 128 digest(s) recomputed; 1884 declared edit line(s) on 8 row(s) …` |
| control | `control: 8/8 owned digest(s) recomputed equal at 90111df262d6` |
| carve layers | code 80/80 (31 commits), spec 38/38 (33), root 10/10 (16); missing 0, extra 0, mismatch 0 in each |
| commit A, each leg | merge clean, including `openspec/config.yaml` in the spec leg; both `diff`s empty; helper 3: 0 refusals; 0 tags in either leg |
| commit A, code leg gates | syntax gate 0; validator 2 (no envelope); pytest 30 failed, 12 passed, 1 skipped: red by construction |
| commit B, spec leg (14 lines + `LICENSE`) | helper 3: `4 edited on declared lines only; 0 declaring edits left unapplied; 0 refusal(s)`; the gate: `Totals: 3 passed, 0 failed (3 items)`, `OK` |
| the root's one commit | two parents (the root's `main`, the carve layer); `make validate` passed; helper 3: `1 edited on declared lines only … 0 refusal(s)`; three-way `8/8 … consumed rows left: 0` |
| helper 2, a carved blob with one byte appended | `MISMATCH contracts/openxwallet/openxwallet-grant.schema.yaml`, exit 1 |
| helper 3, one undeclared line and a stray file | `REFUSE undeclared line(s) in openspec/specs/openxwallet/spec.md: [11]`, `REFUSE added, not declared: stray.txt`, exit 2 |
| helper 3, `LICENSE` not declared | `REFUSE added, not declared: LICENSE`, exit 2 |
| the `code` gitlink moved alone | `FINDING pin-gitlink-mismatch: code: gitlink … != contracts/code-pin.yaml commit …`, exit 1 |
| filter-repo, `origin` removed first | refused: `(expected one remote, origin)` |
| filter-repo, mirror cloned from a path without `--no-local` | refused: `(expected freshly packed repo)` |
