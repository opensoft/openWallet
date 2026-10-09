# Byte-identity proof — `wallet-v1.6`

Status: record. Parts zero to five RUN-GREEN, part three's second half (D5's
neutrality gate over the composed adapter) included; the consumer statement
RUN-GREEN to depth 2, depth 3 PENDING group 6
Kind: proof, a DECLARED PATH MAPPING
Governing change: opensoft/openXwallet
`openspec/changes/split-openwallet-neutral-core/`, `design.md` D7 "The proof —
a DECLARED PATH MAPPING", and `tasks.md` 4.6. The procedure is this root's
`docs/openwallet-cutover-runbook.md`, Phase 4.
Tracked on: opensoft/openXwallet#25
Run: 2026-10-09 (UTC), by lane `openXwallet-2`. Part three's second half, the
consumer's depth 2 and the spec-pin snapshot were run the same day, against
opensoft/openXwallet `a02c6c74`; part three's second half and depth 2
re-confirmed at `815b86ce`, group 5's landing commit (opensoft/openXwallet#40's
merge), 2026-10-09

**The claim.** openWallet's first release on this root, `wallet-v1.6`, is a
**declared path mapping** of opensoft/openXwallet at one named commit into three
repositories. The mapping has four properties:
- every path tracked at the carve commit goes to exactly one place, or stays;
- every carved path keeps its repository-relative path inside its leg;
- every carved byte arrives at its carve layer identical, blob and mode;
- every difference after the carve layer falls in one of five closed edit
  classes or is one of the closed declared additions.

Not "essentially the same". Every part below can fail. Part four shows each
verifier failing on a mutated input.

**Why the claim matters more than it looks.** openXwallet's adapter rebuild
(`tasks.md` group 5) mounts this root and sheds the 106 rows its carve manifest
marks `shed`. openxFactory then re-paths its pin two levels deeper (group 6).
Shedding is safe only if the bytes leaving openXwallet are demonstrably the
bytes arriving here. So this document is not a report. As its precedent
`docs/byte-identity-wallet-v1.0.md` was (carried here as lineage), it is the
precondition of a tag.

**The tag.** Brett Heap ruled the number on 2026-10-08, in session, by multiple
choice, label verbatim: **"wallet-v1.6 (Recommended)"**. It continues
openXwallet's `wallet-v1.0`…`wallet-v1.5` series (RULED Q4, "openWallet
continues wallet-v* (Recommended)"). At the run, the number was ALLOCATED and
**the tag was NOT cut.** It waited for three things (runbook Phase 6, task 4.9,
an operator act):
- this proof landing on this root's `main`;
- the spec re-pin landing (part two (b): after the carve, the `spec` pin
  follows the leg's `main` through declared changes);
- the three rulesets of Phase 5 (task 4.7) ACTIVE.

It was to go on this root's `main` after the first two, on the root commit that
carries the completed proof. Brett Heap ruled that on 2026-10-09, label
verbatim: **"The root commit carrying the completed proof (Recommended)"**.

**The tag is now cut.** The annotated tag `wallet-v1.6` (tag object
`3acfa611b69503e809043faff5f3622cc008a3eb`) was cut on 2026-10-09 on
`b0af7c2ce53d63786a08a20aa3602a6f90345606`. That is the merge of
opensoft/openWallet#7, the release commit `88345cc8` on `b4580d16`. Brett Heap
ruled its place on 2026-10-09, label verbatim: **"Release commit on b4580d16,
tag its merge (Recommended)"**. By then the proof and the spec re-pin had
landed (opensoft/openWallet#5 as `bead4bd8`), and openXwallet's `tasks.md`
records 4.7's rulesets ACTIVE before the cut.

**The part run last.** On 2026-10-08, by multiple choice, label verbatim:
**"Start now, neutrality half later (Recommended)"**. Part three's second half
needs the composed adapter, which group 5 builds on lane `openXwallet-3`'s
branch `rebuild/adapter-group-5` of opensoft/openXwallet. This document's first
commit wrote that half as PENDING. A follow-up commit ran it on 2026-10-09
against the branch's head, `a02c6c74`, and quotes the measured output. A later
commit re-confirmed it at `815b86ce`, the commit group 5 landed. Every part
below is now RUN. One thing stays open, stated where it belongs: depth 3 of the
consumer statement, inside openxFactory (group 6).

## The NAMED CARVE COMMIT, and what was measured

```
CARVE_COMMIT = 90111df262d6f54f7e82651d860adc12345f83f4
SOURCE       = opensoft/openXwallet
MANIFEST     = docs/openwallet-carve-manifest.yaml at opensoft/openXwallet@64ca6eac651a63e1b23ac080f66ee5932575d073
```

The manifest is the amended one: Brett Heap, label verbatim "Amend the
manifest: 8 declared lines (Recommended)" (opensoft/openXwallet#25). Its bytes
hash to `3b04bd6bb52b8d247569407f639e67d48db24e28fa07c3cb0785dfbaedb432ee`.
`git diff 64ca6eac..6d056b3 -- docs/openwallet-carve-manifest.yaml
scripts/validate-carve-manifest.py` is empty, so openXwallet's `main` at the
time of the run carries the same manifest and the same checker.

| Object | Commit | What it is |
| --- | --- | --- |
| code leg, carve layer | `13eca06d50cf2c08be31343d77bf89c3c89c8b15` | the `openwallet_code` rows, `git filter-repo`'d at the carve commit, 31 commits of history; it is commit A's second parent |
| code leg, commit A | `32c933551b92d83122a45847215d5ebe92ae6740` | the arrival: the scaffold `main` (`51b8e9c3`) merged with the carve layer |
| code leg, commit B | `75b990dc7ea99823626c18816b37d971f46e341b` | the declared-edit layer, on A |
| code leg, pinned | `72313daab1f229c049cb90998931564c1904dbbc` | opensoft/openWallet-code#2's merge; its tree is B's tree (`c975dc3f`) |
| spec leg, carve layer | `eb0947209c2c4fe50bd2c33a39cffe94b65c2f1c` | the `openwallet_spec` rows, 33 commits; commit A's second parent |
| spec leg, commit A | `c788cba28a81b0dc17da4cea5db1e57eceb3a193` | the scaffold `main` (`cfd0a69c`) merged with the carve layer |
| spec leg, commit B | `5ea9539428eae850ba71e6f0ba8a38db061e809a` | the declared-edit layer, on A |
| spec leg, pinned | `15c15bbd451a803f0acdb24e5234836db829a2d3` | opensoft/openWallet-spec#2's merge; its tree is B's tree (`6dcc8fd7`) |
| root, carve layer | `3c44089c7d880ed2721067f97bbaf471d7b9387b` | the `openwallet_root` rows, 16 commits; the lockstep commit's second parent |
| root, lockstep commit | `b48bcb20b31dece4d582444cf01f617a799d297d` | the root's carve layer and its manifest field edits, merged with both leg pins in ONE commit; first parent `2b8e2234`, the root `main` before |
| root, measured | `1c68717f1ae4ae132d6942f8c7f533baf292d0b6` | opensoft/openWallet#2's merge; it pins spec `15c15bbd` and code `72313daa` |
| openXwallet, the composed adapter | `a02c6c7487171c110490b234643a7e586ed47153` | the head of `rebuild/adapter-group-5` (lane `openXwallet-3`, group 5) at the run, on openXwallet `main` `206e0d4f`; it pins this root at `1c68717f` (part three, second half) |
| openXwallet, group 5 landed | `815b86cef18c6227f649d2cefedb05720069362b` | opensoft/openXwallet#40's merge of `rebuild/adapter-group-5-r2` (head `36c365da`), where part three's second half was re-confirmed; it pins this root at `b0af7c2c` (the `wallet-v1.6` release) and its code leg at `72313daa` |
| spec leg, after the carve | `1506bbdb4194a779bef63d8c4e5eecc7eac0bd68`, then `1924500354f472a6298c02db44a3ae2b21b8908e` | opensoft/openWallet-spec#3's merge (the birth change `bind-approval-posture-vocabulary`), then #4's (its archive): declared post-carve changes that the root's `spec` pin follows (part two (b)) |

The three carve layers that landed are the commits the runbook's filter-repo
steps produced. Each leg's `A^2`, and the root's `b48bcb2^2`, equals the
`carve-src` branch of the mirror that `git filter-repo` rewrote. At the run,
none of the three repositories carried a tag. Since then the root carries
`wallet-v1.6` ("The tag", above); the legs still carry none.

## How to reproduce this document

Every command below uses repo-relative paths and the placeholders `$WORK`,
`$SRC`, `$MANIFEST` and `$CARVE_COMMIT`, so no host path is baked into the
record. The commands are bash.

```bash
WORK=$(mktemp -d)                         # the proof's own scratch directory
cd "$WORK" || exit 1
CARVE_COMMIT=90111df262d6f54f7e82651d860adc12345f83f4
git clone -q --recurse-submodules https://github.com/opensoft/openWallet.git root
git -C root checkout -q 1c68717f1ae4ae132d6942f8c7f533baf292d0b6 && git -C root submodule update -q
git clone -q --mirror --no-local https://github.com/opensoft/openXwallet.git oxw.git
git clone -q https://github.com/opensoft/openXwallet.git oxw
git -C oxw checkout -q --detach 64ca6eac651a63e1b23ac080f66ee5932575d073
SRC=$WORK/oxw.git
MANIFEST=$WORK/oxw/docs/openwallet-carve-manifest.yaml
pip install pyyaml jsonschema rfc3339-validator pytest   # what the code leg's two workflows install
```

**The runbook's five helpers, extracted from its own text.** They are
byte-identical to the copies printed in `docs/openwallet-cutover-runbook.md` at
`1c68717f`, so the helpers the runbook prints are the helpers that ran:

```bash
mkdir -p "$WORK/bin"
python3 - root/docs/openwallet-cutover-runbook.md "$WORK/bin" <<'PY'
import re, sys
text = open(sys.argv[1], encoding="utf-8").read()
for m in re.finditer(r"cat > \"\$WORK/bin/([^\"]+)\" <<'PY'\n(.*?)\nPY\n", text, re.S):
    open(f"{sys.argv[2]}/{m.group(1)}", "w", encoding="utf-8").write(m.group(2) + "\n")
    print("extracted", m.group(1))
PY
(cd bin && sha256sum *.py)
```

```
bdba1605d86ad7d27e35acb49826ec389fdb84b4926237c2143ee87ac978ab33  carve-layer.py
8657c1a31d9c549bab71dfe4451c440e5e711fdf1e7408c986757175b9e7e7f3  carve-paths.py
cf99e91136249a39acf1c4c4e7c4636c4784ebca041a5cfb8fdc53960b15370c  control.py
1ac1bf432a5ab32b362ff0db916e61d253c354ac9dd233acde0d43cfbf17aa8f  declared-edits.py
38c1d340b34213bb86baa890486ff29b64b9681491aeaa750b356da22db6af6a  declared-lines-exact.py
```

**The proof's own four checks.** Each is standard-library Python plus PyYAML,
and each exits non-zero on any disagreement. They live in `$WORK/proof-bin`,
outside every clone. This root gains no script.
- `mapping.py` checks part one (a) independently of openXwallet's checker.
- `per-path.py` records part two (a) per path.
- `three-way-full.py` is part one (b). It is the runbook's 3c check widened to
  all three ways, and it adds an exit code (see "Findings" below).
- `attribute.py` attributes each changed line of part two (b) to its declared
  edit.

```bash
mkdir -p "$WORK/proof-bin"
cat > "$WORK/proof-bin/mapping.py" <<'PY'
# Part one (a), independently of the checker: the mapping is TOTAL and FUNCTIONAL.
# usage: python3 mapping.py MANIFEST SRC_REPO CARVE_COMMIT
import collections, subprocess, sys, yaml
manifest, repo, carve = sys.argv[1:4]
doc = yaml.safe_load(open(manifest, encoding="utf-8"))
assert doc["carve_commit"] == carve
tracked = [p.decode() for p in subprocess.run(["git", "-C", repo, "ls-tree", "-r", "-z", "--name-only", carve],
           check=True, capture_output=True).stdout.split(b"\0") if p]
rows = doc["rows"]
src = collections.Counter(r["source_path"] for r in rows)
dup = sorted(p for p, n in src.items() if n > 1)
in_no_row = sorted(set(tracked) - set(src))
row_no_path = sorted(set(src) - set(tracked))
moved = [r for r in rows if r["disposition"] != "not_moved"]
renamed = sorted(r["source_path"] for r in moved if r["destination_path"] != r["source_path"])
undest = sorted(r["source_path"] for r in moved if r.get("destination") not in doc["destinations"])
stray = sorted(r["source_path"] for r in rows if r["disposition"] == "not_moved" and (r.get("destination") or r.get("destination_path")))
print(f"tracked paths at {carve[:12]}: {len(tracked)}; manifest rows: {len(rows)}")
print(f"path in no row: {len(in_no_row)}; path in two or more rows: {len(dup)}; row for an untracked path: {len(row_no_path)}")
print(f"moved rows: {len(moved)}; destination_path != source_path: {len(renamed)}; "
      f"moved row with no declared destination: {len(undest)}; not_moved row naming a destination: {len(stray)}")
for d in sorted(doc["destinations"]):
    rs = [r for r in moved if r["destination"] == d]
    print(f"  {d}: {len(rs)} row(s) = {sum(r['disposition'] == 'moved_verbatim' for r in rs)} moved_verbatim"
          f" + {sum(r['disposition'] == 'moved_with_declared_edit' for r in rs)} moved_with_declared_edit")
print(f"  not_moved: {sum(r['disposition'] == 'not_moved' for r in rows)}")
for label, ps in (("IN-NO-ROW", in_no_row), ("DUPLICATE", dup), ("UNTRACKED", row_no_path), ("RENAMED", renamed),
                  ("NO-DESTINATION", undest), ("STRAY", stray)):
    for p in ps:
        print(f"  {label} {p}")
bad = in_no_row or dup or row_no_path or renamed or undest or stray or len(tracked) != len(rows)
print("mapping: TOTAL and FUNCTIONAL" if not bad else "mapping: REFUSED")
sys.exit(1 if bad else 0)
PY

cat > "$WORK/proof-bin/per-path.py" <<'PY'
# Part two (a), recorded PER PATH: for each of DEST's rows, the git blob and mode at
# the carve commit in the source equal the git blob and mode at the destination's
# carve layer, and sha256(blob) equals the manifest's sha256.
# usage: python3 per-path.py DEST MANIFEST SRC_REPO CARVE_COMMIT LEG_REPO LAYER_REF
import hashlib, subprocess, sys, yaml
dest, manifest, src, carve, leg, layer = sys.argv[1:7]
def git(repo, *a):
    return subprocess.run(["git", "-C", repo, *a], check=True, capture_output=True).stdout
def tree(repo, ref):
    out = {}
    for rec in filter(None, git(repo, "ls-tree", "-r", "-z", ref).split(b"\0")):
        meta, path = rec.split(b"\t", 1)
        mode, _t, oid = meta.decode().split()
        out[path.decode()] = (mode, oid)
    return out
rows = {r["destination_path"]: r for r in yaml.safe_load(open(manifest, encoding="utf-8"))["rows"]
        if r.get("destination") == dest}
t_src, t_layer = tree(src, carve), tree(leg, layer)
listing_equal = sorted(t_layer) == sorted(rows)
same = 0
print("| # | path | mode | git blob (carve commit = carve layer) | sha256 = manifest |")
print("| ---: | --- | --- | --- | --- |")
for i, p in enumerate(sorted(rows), 1):
    s, l = t_src[p], t_layer.get(p)
    digest = hashlib.sha256(git(leg, "cat-file", "blob", l[1])).hexdigest() if l else None
    ok = l == s and s[0] == str(rows[p]["git_mode"]) and digest == rows[p]["sha256"]
    same += ok
    print(f"| {i} | `{p}` | `{s[0]}` | `{s[1]}` | {'yes' if ok else 'NO: ' + repr((s, l, digest))} |")
print()
print(f"{dest}: sorted listing of {layer} equals the {len(rows)} row(s): {listing_equal}; "
      f"identical git blob and mode: {same}/{len(rows)}")
sys.exit(0 if listing_equal and same == len(rows) else 1)
PY

cat > "$WORK/proof-bin/three-way-full.py" <<'PY'
# Part one (b): the eight digests THREE-WAY.
#   (1) the CARVE-COMMIT manifest: openXwallet contracts/manifest.yaml at the carve commit, sha256: per owned row
#   (2) the BYTES at contracts/... in the code leg's carve layer (and at the code commit this root pins)
#   (3) THIS ROOT's contracts/manifest.yaml owned rows, at code/contracts/...
# usage (from the root clone): python3 three-way-full.py SRC_REPO CARVE_COMMIT CODE_CARVE_LAYER_REF
import hashlib, subprocess, sys, yaml
src, carve, layer = sys.argv[1:4]
def git(repo, *a):
    return subprocess.run(["git", "-C", repo, *a], check=True, capture_output=True).stdout
def owned(contracts):
    return [c for c in contracts if c.get("sha256") and c.get("member_class", "owned") == "owned"]
one = owned(yaml.safe_load(git(src, "show", f"{carve}:contracts/manifest.yaml"))["contracts"])
three_doc = yaml.safe_load(open("contracts/manifest.yaml", encoding="utf-8"))
three = {c["id"]: c for c in owned(three_doc["contracts"])}
pinned = git(".", "ls-tree", "HEAD", "code").split()[2].decode()     # the code gitlink at the root's HEAD
ok = 0
for c in one:
    p = c["path"]
    in_layer = hashlib.sha256(git("code", "show", f"{layer}:{p}")).hexdigest()
    in_pinned = hashlib.sha256(git("code", "show", f"{pinned}:{p}")).hexdigest()
    r = three.get(c["id"], {})
    agree = (c["sha256"] == in_layer == in_pinned == r.get("sha256") and r.get("path") == "code/" + p)
    ok += agree
    print(f"{'agree   ' if agree else 'DISAGREE'} {c['id']}: {c['sha256']} | layer {in_layer[:12]} | "
          f"pinned {in_pinned[:12]} | root {r.get('path')} {str(r.get('sha256'))[:12]}")
consumed = sum(1 for c in three_doc["contracts"] if c.get("member_class") == "consumed")
print(f"three-way: {ok}/{len(one)} agree (carve-commit manifest = code-leg carve layer {layer} = code leg at "
      f"the pinned {pinned[:12]} = this root's manifest at code/contracts/...); root owned rows {len(three)}; "
      f"consumed rows left {consumed}")
sys.exit(0 if ok == len(one) == len(three) == 8 and consumed == 0 else 1)
PY

cat > "$WORK/proof-bin/attribute.py" <<'PY'
# Part two (b), per declared edit: how many of its lines the histogram diff removed or
# replaced. A removed or replaced line that no edit declares is counted as NONE.
# usage (inside the destination clone): python3 attribute.py DEST MANIFEST CARVE_REF HEAD_REF
import re, subprocess, sys, yaml
dest, manifest, carve, head = sys.argv[1:5]
hunk = re.compile(rb"^@@ -(\d+)(?:,(\d+))? \+\d+(?:,\d+)? @@", re.M)
none = 0
for r in yaml.safe_load(open(manifest, encoding="utf-8"))["rows"]:
    if r.get("destination") != dest or not r.get("edits"):
        continue
    p = r["destination_path"]
    diff = subprocess.run(["git", "diff", "-U0", "--diff-algorithm=histogram", "--no-ext-diff", "--no-textconv",
                           carve, head, "--", p], check=True, capture_output=True).stdout
    changed = set()
    for m in hunk.finditer(diff):
        s, c = int(m.group(1)), int(m.group(2) or 1)
        changed |= set(range(s, s + c)) if c else set()
    union = {n for e in r["edits"] for n in e["lines"]}
    for i, e in enumerate(r["edits"], 1):
        print(f"  {p} edit {i} [{e['class']}]: declared {len(e['lines'])}, removed or replaced {len(set(e['lines']) & changed)}")
    stray = sorted(changed - union)
    none += len(stray)
    print(f"{p}: {len(changed)} line(s) removed or replaced; in no declared edit: {len(stray)} {stray if stray else ''}")
print(f"{dest}: removed or replaced line(s) in no declared edit: {none}")
sys.exit(1 if none else 0)
PY
(cd proof-bin && sha256sum *.py)
```

```
a66cb00d2f88e0ceb011e88accfa86ca0321e89f93279e927170caf95f9fba6f  attribute.py
bb54645f4761365332483a96601f5d6783a3ed2ae1ef3c06f77b500af32aaf79  mapping.py
7b291f23509a5c28ba2fae919db49a7cf7a618852cdac889a42948fb40c1d693  per-path.py
1fa1b2734d3b5ff757c1954fb7839427fd45153420dee531d9623fe916d59151  three-way-full.py
```

The run used git 2.43.0, Python 3.12.3, PyYAML 6.0.3, jsonschema 4.26.0,
rfc3339-validator 0.1.4, pytest 9.1.1 and node v24.21.0. Part three's second
half used the same git, Python and packages. Nothing was re-carved, so `git
filter-repo` did not run for this proof.

**This document's own commands were then run again**, as extracted from its
text, in order, in a fresh scratch directory. Every output line quoted in
parts zero to five was printed again, except values that vary by nature from
run to run: the short id of part four's scratch commit in 4.1, and pytest's
elapsed time.

The blocks added with part three's second half were handled in two ways:
- **Re-run as extracted, quoted lines printed again:** the spec-pin snapshot
  (part two (b)), the adapter's setup, and trees (i) and (ii). The one varying
  value is openxFactory's `main` in (ii)'s first line: it had moved on to
  `de70915154f6`, with `governance/` still unchanged.
- **Measured once, before being written into this text, then re-run from
  it:** (iii)'s capture and replay, the other invocations, 4.9 and depth 2.
  Each used the same command this text prints. The quoted lines carry those
  measurements, in the form these blocks print them, and the per-tree table
  holds the replay's results tree for tree. The re-run from this text was
  completed on 2026-10-09 (UTC, the runner finishing at about 01:40Z): the
  blocks as printed here, in order, in a fresh scratch directory, with the
  scratch path read as `$WORK`. The runner exited 0 (`runner exit=0`), and
  every quoted line was printed again:
  - (iii)'s capture: the same hook sha256, `ea9e3e3f…`; `91 passed` and
    `33 passed, 1 skipped` under the hook; 96 and 31 validator invocations
    recorded, and 82 + 28 built trees;
  - the replay: 110 rows, identical to the per-tree table; 110 of 110 EMPTY,
    plain and `--strict`; 52 at exit 0/0 and 58 at 1/1;
  - the other invocations: the self-test alone EMPTY; `--help` differing by
    design, outside the verdict; a path that does not exist EMPTY, with exit
    2; Finding 4's three trees reproducing the same one-line differences,
    with the exported copy EMPTY;
  - 4.9, printing `DIFFERS` on the same `6c6` line;
  - depth 2: `88/88` from this text's script and `88/88` three ways, and
    openXwallet's pin 8/8, unchanged;
  - the one output that varied: pytest's elapsed time, 272.31 s and 32.31 s
    where this text quotes 421.89 s and 30.15 s. The quoted lines stay as
    first measured.

**Re-confirmation at `815b86ce` (2026-10-09).** Group 5 landed as
`815b86cef18c6227f649d2cefedb05720069362b`, opensoft/openXwallet#40's merge of
`rebuild/adapter-group-5-r2` (head `36c365da`). At that merge openXwallet pins
this root at `b0af7c2c`, the `wallet-v1.6` release merge
(opensoft/openWallet#7), and the code leg is still `72313daa`. The blocks of
part three's second half, 4.9 and depth 2 were run again there, extracted by
line number from this text as it stood at `b4580d16`, under the same git,
Python and packages. There were five declared deviations: `WORK` was a fixed
scratch tree, not `mktemp -d`; the adapter's checkout named `815b86ce` instead
of `a02c6c74`; depth 2's block ran in `$WORK/oxw-adapter` with
`PREFIX=openWallet/code/`, as its paragraph says; lane `openXwallet-3`'s gate,
for which this text prints no command, ran as
`python3 -B scripts/neutrality-gate.py --openxfactory-export <dir>` in a second
fresh clone; and any diff of the export was withheld. Rows that name the root
pin were compared with `b0af7c2c` in place of `1c68717f`. Of 38 rows compared,
29 are the same, and they include every neutrality row: (i) and (ii) EMPTY,
plain and `--strict`; (ii)'s summary lines; (i) as both validators print it;
the hook's sha256; the moved suites; the status checks; the self-test, the path
that does not exist, Finding 4's code-leg and carve-commit trees and the code
copy; 4.9; and depth 2, 88/88 three ways, with the pin summary at `b0af7c2c`
and the eight sha256s. The other 9 differ by a count or a wording, and none is
a neutrality failure:
1. The pin verifier reads `(tag label wallet-v1.6)` for
   `(tag label <none yet>)`, and ends `present and unmodified` for `present`:
   #40 re-pinned the root to the release, with its tag label, and reworded the
   verifier.
2. The kept suites print `96 passed` (recorded `91 passed`): #40 added tests.
3. They record `6 file(s), 98 validator invocation(s)` (recorded 5 and 96).
   The sixth file, `tests/openwallet_pin/test_consumer_surface.py`, is new in
   #40 and spells the validator's name.
4. Their kinds are `--help` 2 and built trees 83 (recorded 1 and 82), with the
   self-test 5, no such path 1 and the live checkout 7 unchanged. The new
   `--help` and the new tree come from tests #40 added to
   `tests/openwallet_pin/test_composed_entrypoints.py`. So at `815b86ce`, 18
   invocations hand the validator no built tree, where the record has
   seventeen, and `--help` is invoked 3 times, twice in the kept suites and
   once in the moved, where the record has 2, one in each. Part three keeps the
   recorded values as the `a02c6c74` record.
5. The replay counts 111 trees (recorded 110).
6. 53 are at exit 0/0 in both modes and 58 at 1/1 (recorded 52 and 58): the
   new tree is clean.
7. The per-tree table gains `openwallet_pin`'s
   `test_a_core_that_exits_zero_while_loading_refuses[validator]` as #13,
   EMPTY, 0/0 in both modes. The table numbers trees in invocation order, so a
   test added early renumbers every row after it: the 110 recorded rows follow
   unchanged and in order, #13 to #110 as #14 to #111, and all 111 are EMPTY
   with equal exit codes in both modes.
8. The neutral `--help` diff is `3c3,4` (recorded `75,79c75,79`): #40 rewrote
   the adapter's docstring. `--help` is outside the verdict, as part three
   already says.
9. Lane `openXwallet-3`'s gate prints the reworded summary quoted under part
   three's second half, counting 122 suite invocations (recorded 117), and
   exits 0: #40 reworded the summary and added tests.

---

## Part zero — the CONTROL, recomputed at the carve commit

If the eight recorded digests did not already describe the carve commit's bytes,
a later match would prove the manifest **stale** rather than the carve
**faithful**. So the control comes first, and it is part of the proof. It was
first taken before anything was carved (task 4.1). It is re-run here rather than
cited, against a fresh mirror.

```bash
cd "$WORK" || exit 1
python3 bin/control.py "$CARVE_COMMIT" oxw.git
```

```
match    openxwallet-record 20ba39c07564c93b8ffe47382126677a165771244d28fb0c4976ab950173c40a
match    openxwallet-custody-registry-schema df72638497a7f90c2a4dff47c429cb794bc4b6e270ce2dd2b17116478ae3b51a
match    openxwallet-custody-registry 94d631d6ee76dab015628a1856afd82582b98d6a3733622c9afe8b13b5278539
match    openxwallet-grant fde433c5821e2e6f62926a72c58a67a784961d2e9e27e9f2b3520fcc8e738e88
match    openxwallet-grant-exercise f16ad31246186cec36e142ae39bd831d98fbc5c0afd48685057bc39e113c8858
match    openxwallet-distinct-holder-constraint c2a6d2fd23fb3743fdaf0e165dabc4cb1dff24e52a8262a38c86ed1482374b25
match    openxwallet-subject-attestation d29eca519462aff7871de3786f19c820e9fc3b95115ce30e57d1f1cc2bc0c0b2
match    openxwallet-agent-composition aed3978e8ae952f3ff5b3de1f672bba5da350d5aaeb442feafaa870b4de4be91
control: 8/8 owned digest(s) recomputed equal at 90111df262d6
exit=0
```

**Part zero: RUN-GREEN, 8/8.** openXwallet's `contracts/manifest.yaml` at the
carve commit describes the carve commit's bytes exactly.

---

## Part one (a) — the MAPPING is total and functional

The mapping is **total** when every path tracked at the carve commit sits in
exactly one manifest row. It is **functional** when every moved row has one
destination and its `destination_path` equals its `source_path`. Per
destination, the carve layer's sorted listing must then equal that
destination's rows.

**openXwallet's own checker**, against the fresh mirror. `--manifest` is passed
explicitly, because without it the checker finds no working tree in a mirror and
checks nothing (runbook step (ii)):

```bash
cd "$WORK" || exit 1
python3 oxw/scripts/validate-carve-manifest.py --repo oxw.git --at "$CARVE_COMMIT" --manifest "$MANIFEST"
```

The checker prints the manifest's absolute path, written here as `$MANIFEST`:

```
OK $MANIFEST: phase carve, 232 row(s) at opensoft/openXwallet@90111df262d6 — 119 moved_verbatim, 9 moved_with_declared_edit, 104 not_moved; destinations: openwallet_code 80, openwallet_root 10, openwallet_spec 38; retained_here: kept 124, shed 106, retired_by_archive 2; leg overrides: d7-root-release-identity 9 (proposed), q7-code-leg 73 (ruled); 128 digest(s) recomputed; 1892 declared edit line(s) on 9 row(s); 232 tracked path(s) at the carve commit, each in exactly one row
exit=0
```

**The same claim, independently of that checker.** `mapping.py` lists the
tracked paths with `git ls-tree` itself and holds the rows against them:

```bash
python3 proof-bin/mapping.py "$MANIFEST" oxw.git "$CARVE_COMMIT"
```

```
tracked paths at 90111df262d6: 232; manifest rows: 232
path in no row: 0; path in two or more rows: 0; row for an untracked path: 0
moved rows: 128; destination_path != source_path: 0; moved row with no declared destination: 0; not_moved row naming a destination: 0
  openwallet_code: 80 row(s) = 76 moved_verbatim + 4 moved_with_declared_edit
  openwallet_root: 10 row(s) = 9 moved_verbatim + 1 moved_with_declared_edit
  openwallet_spec: 38 row(s) = 34 moved_verbatim + 4 moved_with_declared_edit
  not_moved: 104
mapping: TOTAL and FUNCTIONAL
exit=0
```

`bin/carve-paths.py` asserts `destination_path == source_path` on every row it
emits. Its lists are reused below:

```bash
cd "$WORK" || exit 1
for d in code spec root; do
  python3 bin/carve-paths.py openwallet_$d "$MANIFEST" > paths-openwallet_$d.txt
  echo "openwallet_$d exit=$? $(wc -l < paths-openwallet_$d.txt)"
done
```

```
openwallet_code exit=0 80
openwallet_spec exit=0 38
openwallet_root exit=0 10
```

Each list is byte-identical to the `paths-<DEST>.txt` that the carve built its
`--path` arguments from.

**Per destination, the carve layer's sorted listing equals that destination's
rows**, run from this root's clone against the carve layers as they landed:

```bash
cd "$WORK/root" || exit 1
python3 ../bin/carve-layer.py openwallet_code "$MANIFEST" code 32c933551b92d83122a45847215d5ebe92ae6740^2
python3 ../bin/carve-layer.py openwallet_spec "$MANIFEST" spec c788cba28a81b0dc17da4cea5db1e57eceb3a193^2
python3 ../bin/carve-layer.py openwallet_root "$MANIFEST" . b48bcb20b31dece4d582444cf01f617a799d297d^2
```

```
openwallet_code: 80 row(s); 80 path(s) at 32c933551b92d83122a45847215d5ebe92ae6740^2; missing 0, extra 0, blob/mode mismatch 0
exit=0
openwallet_spec: 38 row(s); 38 path(s) at c788cba28a81b0dc17da4cea5db1e57eceb3a193^2; missing 0, extra 0, blob/mode mismatch 0
exit=0
openwallet_root: 10 row(s); 10 path(s) at b48bcb20b31dece4d582444cf01f617a799d297d^2; missing 0, extra 0, blob/mode mismatch 0
exit=0
```

### The explicit counts

The design's rehearsal counts were "68 + 8 contract files less 3; 41 + 4
negatives less 3, at `b7c6e0b`". They were re-measured at the carve commit and
at the code leg's carve layer:

```bash
cd "$WORK/root" || exit 1
cnt() { git -C "$1" ls-tree -r --name-only "$2" -- "$3" | wc -l; }
for pfx in contracts/openxwallet/ contracts/openxwallet-agent-profile/ \
           contracts/openxwallet/examples/ contracts/openxwallet-agent-profile/examples/ \
           contracts/openxwallet/examples/negative/ contracts/openxwallet-agent-profile/examples/negative/; do
  echo "$pfx $(cnt "$SRC" "$CARVE_COMMIT" $pfx) $(cnt code 32c933551b92d83122a45847215d5ebe92ae6740^2 $pfx) $(cnt code 72313daab1f229c049cb90998931564c1904dbbc $pfx)"
done
git -C "$SRC" ls-tree -r --name-only "$CARVE_COMMIT" -- contracts/ | grep grant-review
```

| Measure | at the carve commit | at the code leg's carve layer | at the pinned code leg (`72313daa`) |
| --- | ---: | ---: | ---: |
| files under `contracts/openxwallet/` | **68** | **65** | 66 (the corpus binding added) |
| files under `contracts/openxwallet-agent-profile/` | **8** | **8** | 8 |
| contract files carved, 68 + 8 less 3 | 76 | **73** | — |
| `contracts/openxwallet/examples/negative/` | **41** | **38** | 38 |
| `contracts/openxwallet-agent-profile/examples/negative/` | **4** | **4** | 4 |
| negatives carved, 41 + 4 less 3 | 45 | **42** | 42 |
| the three `grant-review-*` negatives | 3 | **0** | 0 |
| `contracts/openxwallet/examples/` at that exact relative path | yes (60 files) | **yes (57)** | yes (58) |
| `contracts/openxwallet-agent-profile/examples/` at that exact relative path | yes (6) | **yes (6)** | yes (6) |

The counts at `90111df` are the design's counts at `b7c6e0b`, unchanged. The
**73** contract rows are exactly the rows under the RULED Q7 override
(`q7-code-leg 73 (ruled)` above). The code leg's other 7 rows are:
- `.github/workflows/pytest-suite.yml` and `.github/workflows/wallet-validation.yml`;
- `scripts/validate-openxwallet.py` and `scripts/wallet-yaml-syntax-gate.py`;
- `tests/multi_key_wallets/test_declared_key_sets.py`,
  `tests/nested_repo_prune/test_prune_and_register_note.py` and
  `tests/wallet_yaml_syntax_gate/test_gate.py`.

The three negatives that stay in openXwallet are
`contracts/openxwallet/examples/negative/grant-review-authority-omits-issued-by.yaml`,
`grant-review-root-issuer-is-a-machine.yaml` and
`grant-review-root-issuer-says-opensoft.yaml`.

**Examples-prefix preservation is an acceptance line, not a hope.**
`repo_scan`'s exclusion keys on `examples` in a path's parts AND a family
directory name. A carve that flattened either prefix would re-adjudicate all 42
intended-invalid negatives as LIVE records. Part three shows that it did not
happen: run from the code leg's root, the corpus note counts `42 negative
confirmation(s)`, and the repo scan validates `0` live artifacts and refuses
none.

**Part one (a): RUN-GREEN.** 232 tracked paths, 232 rows, each path in exactly
one row; 128 moved rows, none renamed; 80 / 38 / 10 per destination; both
`examples/` prefixes at their exact paths.

---

## Part one (b) — the eight digests, THREE-WAY

For each of the eight owned artifacts, three things must agree. Three-way, not
two-way, so a manifest that had been "helpfully corrected" would show up:
1. the `sha256:` recorded in openXwallet's `contracts/manifest.yaml` at the
   carve commit;
2. the sha256 of the bytes at `contracts/…` in the code leg: in its carve layer,
   and again at the commit this root pins;
3. this root's `contracts/manifest.yaml` owned row, whose `path:` is
   `code/contracts/…`.

```bash
cd "$WORK/root" || exit 1
python3 ../proof-bin/three-way-full.py "$SRC" "$CARVE_COMMIT" 32c933551b92d83122a45847215d5ebe92ae6740^2
```

```
agree    openxwallet-record: 20ba39c07564c93b8ffe47382126677a165771244d28fb0c4976ab950173c40a | layer 20ba39c07564 | pinned 20ba39c07564 | root code/contracts/openxwallet/openxwallet-record.schema.yaml 20ba39c07564
agree    openxwallet-custody-registry-schema: df72638497a7f90c2a4dff47c429cb794bc4b6e270ce2dd2b17116478ae3b51a | layer df72638497a7 | pinned df72638497a7 | root code/contracts/openxwallet/openxwallet-custody-registry.schema.yaml df72638497a7
agree    openxwallet-custody-registry: 94d631d6ee76dab015628a1856afd82582b98d6a3733622c9afe8b13b5278539 | layer 94d631d6ee76 | pinned 94d631d6ee76 | root code/contracts/openxwallet/openxwallet-custody.registry.yaml 94d631d6ee76
agree    openxwallet-grant: fde433c5821e2e6f62926a72c58a67a784961d2e9e27e9f2b3520fcc8e738e88 | layer fde433c5821e | pinned fde433c5821e | root code/contracts/openxwallet/openxwallet-grant.schema.yaml fde433c5821e
agree    openxwallet-grant-exercise: f16ad31246186cec36e142ae39bd831d98fbc5c0afd48685057bc39e113c8858 | layer f16ad3124618 | pinned f16ad3124618 | root code/contracts/openxwallet/openxwallet-grant-exercise.schema.yaml f16ad3124618
agree    openxwallet-distinct-holder-constraint: c2a6d2fd23fb3743fdaf0e165dabc4cb1dff24e52a8262a38c86ed1482374b25 | layer c2a6d2fd23fb | pinned c2a6d2fd23fb | root code/contracts/openxwallet/openxwallet-distinct-holder-constraint.schema.yaml c2a6d2fd23fb
agree    openxwallet-subject-attestation: d29eca519462aff7871de3786f19c820e9fc3b95115ce30e57d1f1cc2bc0c0b2 | layer d29eca519462 | pinned d29eca519462 | root code/contracts/openxwallet/openxwallet-subject-attestation.schema.yaml d29eca519462
agree    openxwallet-agent-composition: aed3978e8ae952f3ff5b3de1f672bba5da350d5aaeb442feafaa870b4de4be91 | layer aed3978e8ae9 | pinned aed3978e8ae9 | root code/contracts/openxwallet-agent-profile/openxwallet-agent-composition.schema.yaml aed3978e8ae9
three-way: 8/8 agree (carve-commit manifest = code-leg carve layer 32c933551b92d83122a45847215d5ebe92ae6740^2 = code leg at the pinned 72313daab1f2 = this root's manifest at code/contracts/...); root owned rows 8; consumed rows left 0
exit=0
```

The runbook's own 3c check, extracted verbatim and run from the same directory,
agrees:

```bash
awk "/^python3 - <<'PY'\$/{f=1;next} /^PY\$/{f=0} f" docs/openwallet-cutover-runbook.md > ../runbook-3c.py
python3 ../runbook-3c.py
```

```
three-way: 8/8 root-manifest digest(s) equal the code leg's bytes; consumed rows left: 0
```

| # | id | path in the code leg (this root: `code/` + path) | `sha256` (all three agree) |
| --- | --- | --- | --- |
| 1 | `openxwallet-record` | `contracts/openxwallet/openxwallet-record.schema.yaml` | `20ba39c07564c93b8ffe47382126677a165771244d28fb0c4976ab950173c40a` |
| 2 | `openxwallet-custody-registry-schema` | `contracts/openxwallet/openxwallet-custody-registry.schema.yaml` | `df72638497a7f90c2a4dff47c429cb794bc4b6e270ce2dd2b17116478ae3b51a` |
| 3 | `openxwallet-custody-registry` | `contracts/openxwallet/openxwallet-custody.registry.yaml` | `94d631d6ee76dab015628a1856afd82582b98d6a3733622c9afe8b13b5278539` |
| 4 | `openxwallet-grant` | `contracts/openxwallet/openxwallet-grant.schema.yaml` | `fde433c5821e2e6f62926a72c58a67a784961d2e9e27e9f2b3520fcc8e738e88` |
| 5 | `openxwallet-grant-exercise` | `contracts/openxwallet/openxwallet-grant-exercise.schema.yaml` | `f16ad31246186cec36e142ae39bd831d98fbc5c0afd48685057bc39e113c8858` |
| 6 | `openxwallet-distinct-holder-constraint` | `contracts/openxwallet/openxwallet-distinct-holder-constraint.schema.yaml` | `c2a6d2fd23fb3743fdaf0e165dabc4cb1dff24e52a8262a38c86ed1482374b25` |
| 7 | `openxwallet-subject-attestation` | `contracts/openxwallet/openxwallet-subject-attestation.schema.yaml` | `d29eca519462aff7871de3786f19c820e9fc3b95115ce30e57d1f1cc2bc0c0b2` |
| 8 | `openxwallet-agent-composition` | `contracts/openxwallet-agent-profile/openxwallet-agent-composition.schema.yaml` | `aed3978e8ae952f3ff5b3de1f672bba5da350d5aaeb442feafaa870b4de4be91` |

**Part one (b): RUN-GREEN, 8/8.** The carve-commit manifest, the code leg's
bytes (carve layer and pinned commit) and this root's manifest all agree. The
consumed `hermes-job-envelope` row is gone, as declared.

---

## Part two (a) — git blob and mode identity at the carve layer, recorded per path

`bin/carve-layer.py` (part one (a), above) holds each carve layer's blob
sha256 and mode against the manifest row: `blob/mode mismatch 0` in all three
destinations. `per-path.py` makes the stronger comparison, in git's own terms. It
requires that the git blob id and mode at the carve commit in openXwallet equal
the git blob id and mode at the destination's carve layer, path by path. It also
requires that the blob's sha256 equal the manifest's.

```bash
cd "$WORK/root" || exit 1
python3 ../proof-bin/per-path.py openwallet_code "$MANIFEST" "$SRC" "$CARVE_COMMIT" code 32c933551b92d83122a45847215d5ebe92ae6740^2
python3 ../proof-bin/per-path.py openwallet_spec "$MANIFEST" "$SRC" "$CARVE_COMMIT" spec c788cba28a81b0dc17da4cea5db1e57eceb3a193^2
python3 ../proof-bin/per-path.py openwallet_root "$MANIFEST" "$SRC" "$CARVE_COMMIT" . b48bcb20b31dece4d582444cf01f617a799d297d^2
```

```
openwallet_code: sorted listing of 32c933551b92d83122a45847215d5ebe92ae6740^2 equals the 80 row(s): True; identical git blob and mode: 80/80
openwallet_spec: sorted listing of c788cba28a81b0dc17da4cea5db1e57eceb3a193^2 equals the 38 row(s): True; identical git blob and mode: 38/38
openwallet_root: sorted listing of b48bcb20b31dece4d582444cf01f617a799d297d^2 equals the 10 row(s): True; identical git blob and mode: 10/10
```

Each exits 0. The per-path records follow, one table per destination, exactly
as `per-path.py` printed them. Recording each path rather than one aggregate
claim shows which paths were actually compared.

<details>
<summary><code>openwallet_code</code>: 80/80 paths, identical blob and mode</summary>

| # | path | mode | git blob (carve commit = carve layer) | sha256 = manifest |
| ---: | --- | --- | --- | --- |
| 1 | `.github/workflows/pytest-suite.yml` | `100644` | `33300be0f4ddacb4fb8403a1b000bdb8c5f009b5` | yes |
| 2 | `.github/workflows/wallet-validation.yml` | `100644` | `4db28def5428c6505d99ae1326035c2b66224358` | yes |
| 3 | `contracts/openxwallet-agent-profile/README.md` | `100644` | `4d12a22c94ab03d90ea7a20998521a49e6c5ac53` | yes |
| 4 | `contracts/openxwallet-agent-profile/examples/agent-composition-changed.example.yaml` | `100644` | `71e5f53d2cb9e9d29884bbf97b87715a753093aa` | yes |
| 5 | `contracts/openxwallet-agent-profile/examples/agent-composition.example.yaml` | `100644` | `41151084ae465f7967739922c79dd7f8d585d0ec` | yes |
| 6 | `contracts/openxwallet-agent-profile/examples/negative/composition-changed-grants-still-active.yaml` | `100644` | `e173a0647f40b3fb666affd7f12d0d792e33e88e` | yes |
| 7 | `contracts/openxwallet-agent-profile/examples/negative/composition-declared-for-a-non-agent-wallet.yaml` | `100644` | `edbd7bd1f3ea289173cdb27a3e9e7a5a6c1e9367` | yes |
| 8 | `contracts/openxwallet-agent-profile/examples/negative/composition-for-a-wallet-that-does-not-resolve.yaml` | `100644` | `e874c770b6b916b5a70d2d09df5ce979f18f1033` | yes |
| 9 | `contracts/openxwallet-agent-profile/examples/negative/composition-hash-without-component-set.yaml` | `100644` | `106165b06e245192120006102892754a322922fb` | yes |
| 10 | `contracts/openxwallet-agent-profile/openxwallet-agent-composition.schema.yaml` | `100644` | `a04a91525d306e097e15155b60e0ee6e672f41b4` | yes |
| 11 | `contracts/openxwallet/README.md` | `100644` | `1bb7f2500c3399e1b42f18a83878404a5ca2562b` | yes |
| 12 | `contracts/openxwallet/examples/distinct-holder-constraint-posting.example.yaml` | `100644` | `292247bcfac190b74b22de5ec5b52bf77299a435` | yes |
| 13 | `contracts/openxwallet/examples/exercise-posting-permitted.example.yaml` | `100644` | `ad95cb9cf074e1898b28bf4e96ec156d8f59c8b8` | yes |
| 14 | `contracts/openxwallet/examples/exercise-presented-by-an-additional-key.example.yaml` | `100644` | `c46caa0a3106b1929bfa13a88fda6e6efcae59e8` | yes |
| 15 | `contracts/openxwallet/examples/exercise-unattributable-act.example.yaml` | `100644` | `f303c37adf91b8f4c93a069d35c0bc9318a40eb1` | yes |
| 16 | `contracts/openxwallet/examples/exercise-verification-failure.example.yaml` | `100644` | `e6ab64a5205ecd8a3c7fba46de8ea3c0432a7557` | yes |
| 17 | `contracts/openxwallet/examples/grant-council-act-tier.example.yaml` | `100644` | `71011ec3d1a3028dacb865d80ded657ab9dd271b` | yes |
| 18 | `contracts/openxwallet/examples/grant-council-unsupervised-tier.example.yaml` | `100644` | `48fb7ed194e1932f8e3deac27f83148a57066228` | yes |
| 19 | `contracts/openxwallet/examples/grant-creator-software-custody.example.yaml` | `100644` | `bb90a932c937a4ec9d11bf4ce5bc61f59612016e` | yes |
| 20 | `contracts/openxwallet/examples/grant-posting-derived.example.yaml` | `100644` | `d630b945153353884a33c3b05420828596139b71` | yes |
| 21 | `contracts/openxwallet/examples/grant-posting-parent.example.yaml` | `100644` | `d89758e372520e7b7f2f25d88aa235cc06593b29` | yes |
| 22 | `contracts/openxwallet/examples/grant-revoked-derivation.example.yaml` | `100644` | `50b774cdca95ad62f9e915459332d48e928c8b67` | yes |
| 23 | `contracts/openxwallet/examples/grant-revoked-parent.example.yaml` | `100644` | `1bc356088e26a076612f2406b500b7ca5fa919ed` | yes |
| 24 | `contracts/openxwallet/examples/negative/custody-registry-collapsed-ceilings.yaml` | `100644` | `27a79680e5a431dfdff74850764fb54ce08ee99c` | yes |
| 25 | `contracts/openxwallet/examples/negative/custody-registry-environment-outranks-holder.yaml` | `100644` | `aabd0ecdec8decf3a29afd9b6f24dd04c8a84fa2` | yes |
| 26 | `contracts/openxwallet/examples/negative/custody-registry-readable-claims-holder.yaml` | `100644` | `3656f1c12aaa07d0f0c62b970710a7c5dd3b7266` | yes |
| 27 | `contracts/openxwallet/examples/negative/custody-registry-renamed-top-tier.yaml` | `100644` | `db3930ad38f08bd9f78329805ecb89b2dc80b69c` | yes |
| 28 | `contracts/openxwallet/examples/negative/custody-registry-unearned-ceiling.yaml` | `100644` | `54f49875a7ff3ecbdedd011993c26ae236345b12` | yes |
| 29 | `contracts/openxwallet/examples/negative/exercise-against-revoked-parent.yaml` | `100644` | `eb8ce374cac2e9d421ce8ea2873e5a150168566f` | yes |
| 30 | `contracts/openxwallet/examples/negative/exercise-attributed-to-a-wallet-not-presenting-its-key.yaml` | `100644` | `f25b0f70a4c1c0cea0e83d03eeb03b7948af4ff4` | yes |
| 31 | `contracts/openxwallet/examples/negative/exercise-by-a-wallet-the-grant-does-not-address.yaml` | `100644` | `c10dee84d2360168933a0043594c10c2835d592f` | yes |
| 32 | `contracts/openxwallet/examples/negative/exercise-custody-of-another-key-of-the-same-wallet.yaml` | `100644` | `435a114626d7f91fb9bc8558b886943ad793aae3` | yes |
| 33 | `contracts/openxwallet/examples/negative/exercise-omits-a-declared-constraint.yaml` | `100644` | `8dd6ab10db485c6103de32b7f2d97c26c228dd6a` | yes |
| 34 | `contracts/openxwallet/examples/negative/exercise-one-holder-satisfies-constraint.yaml` | `100644` | `cb59967bd09f39710421f1043a9f0c1964ed3226` | yes |
| 35 | `contracts/openxwallet/examples/negative/exercise-permitted-on-unverified-proof.yaml` | `100644` | `50cc49dd98816473171352ae9d118999c6bb9842` | yes |
| 36 | `contracts/openxwallet/examples/negative/exercise-permitted-under-a-retired-declared-key.yaml` | `100644` | `21f2c049c6f4376774d59b7ef5d25e2d25d5cc4d` | yes |
| 37 | `contracts/openxwallet/examples/negative/exercise-permitted-without-proof-of-possession.yaml` | `100644` | `3664433294c7ed1e02edf34c7da5bf35962f39ed` | yes |
| 38 | `contracts/openxwallet/examples/negative/exercise-presenting-key-of-another-wallet.yaml` | `100644` | `dccb7d8041bcab1819a5f197171afaf37e6b8ac3` | yes |
| 39 | `contracts/openxwallet/examples/negative/exercise-presenting-key-outside-the-declared-set.yaml` | `100644` | `65832237b9a644a11df7cf0d5a1e99fc13932c85` | yes |
| 40 | `contracts/openxwallet/examples/negative/exercise-presenting-key-unknown-to-the-corpus.yaml` | `100644` | `53aa2ce4fc2ff24a7069580adf04e7e77b9c547f` | yes |
| 41 | `contracts/openxwallet/examples/negative/exercise-proof-and-attribution-name-different-keys.yaml` | `100644` | `f375bd762a4c474fc384a105b11f3bb944445165` | yes |
| 42 | `contracts/openxwallet/examples/negative/exercise-refusal-names-the-wrong-absence.yaml` | `100644` | `df160b2fa1b48824fd6cc1b90d27eaf18cbcc7a0` | yes |
| 43 | `contracts/openxwallet/examples/negative/exercise-shared-credential-as-actor.yaml` | `100644` | `33d5c73d4c9bd554c8f52c68f32dd0f034016b9b` | yes |
| 44 | `contracts/openxwallet/examples/negative/exercise-single-key-custody-not-the-wallets.yaml` | `100644` | `68136dfb1b8d72b218c500123a5c0ba1567bae04` | yes |
| 45 | `contracts/openxwallet/examples/negative/exercise-tier-above-the-presenting-key-ceiling.yaml` | `100644` | `7d024333cabb69322db1370d4326d6be5f4af6e9` | yes |
| 46 | `contracts/openxwallet/examples/negative/exercise-verification-failure-as-unauthenticated.yaml` | `100644` | `d8837d7f476ce4c021bd4f96a78b115fb708b491` | yes |
| 47 | `contracts/openxwallet/examples/negative/exercise-verified-key-recorded-unattributed.yaml` | `100644` | `2d7dca9c7d9293f63844c84af859d79a40f689da` | yes |
| 48 | `contracts/openxwallet/examples/negative/exercise-verified-proof-names-no-key.yaml` | `100644` | `d666c7a56a99f44c3d17ede0f8a494469fe27d01` | yes |
| 49 | `contracts/openxwallet/examples/negative/grant-derived-waives-parent-approval.yaml` | `100644` | `adf3b327a646ed66335a3a544ec589367cfd7e7a` | yes |
| 50 | `contracts/openxwallet/examples/negative/grant-derived-wider-than-parent.yaml` | `100644` | `378c641c7d2d86da2280379371f5699645329c21` | yes |
| 51 | `contracts/openxwallet/examples/negative/grant-exceeds-custody-ceiling.yaml` | `100644` | `8cec1d9b94a35859b35f3c47ac651117ef018732` | yes |
| 52 | `contracts/openxwallet/examples/negative/grant-parallel-authority-vocabulary.yaml` | `100644` | `4e4c05de60914f7299615b000beda5100386508c` | yes |
| 53 | `contracts/openxwallet/examples/negative/subject-attestation-resolves-through-wallet.yaml` | `100644` | `5e478b758df4ec6ec3e6a804ce15f8e1d7b5b7a9` | yes |
| 54 | `contracts/openxwallet/examples/negative/wallet-carries-jwk-private-exponent.yaml` | `100644` | `793baaef73f472b53255deafb3e96091ba4710b5` | yes |
| 55 | `contracts/openxwallet/examples/negative/wallet-carries-key-material.yaml` | `100644` | `f418516559919c96c09b89c06e302ebec11b6186` | yes |
| 56 | `contracts/openxwallet/examples/negative/wallet-custody-outside-the-closed-set.yaml` | `100644` | `9ae16b85e2e1d36c1011b02db732b85619697716` | yes |
| 57 | `contracts/openxwallet/examples/negative/wallet-declared-key-fingerprint-does-not-recompute.yaml` | `100644` | `8f1cf787defd4bd2d5da509dbae2fe308a1d5f03` | yes |
| 58 | `contracts/openxwallet/examples/negative/wallet-declared-key-omits-its-custody.yaml` | `100644` | `da2d727ae87c869e71b1de2acada5e6e524294d1` | yes |
| 59 | `contracts/openxwallet/examples/negative/wallet-declared-key-outranks-its-wallet.yaml` | `100644` | `793b1ad562ce67deb9a48d3d46c4cebda7296162` | yes |
| 60 | `contracts/openxwallet/examples/negative/wallet-declares-one-key-identifier-twice.yaml` | `100644` | `d433a45663b8311bd81c0bb5ed6501187d57d2c3` | yes |
| 61 | `contracts/openxwallet/examples/negative/wallet-record-duplicating-another-wallet-id.yaml` | `100644` | `a55e98b1ea678eba531b6998922ebd9f874572d8` | yes |
| 62 | `contracts/openxwallet/examples/subject-attestation.example.yaml` | `100644` | `b0ca8333f2a618bfdf103f5a6c734fc9b841e1a6` | yes |
| 63 | `contracts/openxwallet/examples/wallet-agent-council-multi-key.example.yaml` | `100644` | `39c4cef80f4526b1e4f92d466f7e1fccb3cb92ab` | yes |
| 64 | `contracts/openxwallet/examples/wallet-agent-creator.example.yaml` | `100644` | `94bfce13d70426a24398071d7214ebeaac6736c3` | yes |
| 65 | `contracts/openxwallet/examples/wallet-agent-poster.example.yaml` | `100644` | `2f0468922235795fd6657ec17cd5c847e45e0769` | yes |
| 66 | `contracts/openxwallet/examples/wallet-agent-rsa-platform-verifiable.example.yaml` | `100644` | `7c12628c6c6b7bf2c7e21e8578339d5a1913e06f` | yes |
| 67 | `contracts/openxwallet/examples/wallet-practitioner.example.yaml` | `100644` | `d68ec7cba2b2d4851b33d0be1daf0ef5d4296c1d` | yes |
| 68 | `contracts/openxwallet/examples/wallet-revoked-standing.example.yaml` | `100644` | `6bfffa0f66034e396cc426daac880348164630b6` | yes |
| 69 | `contracts/openxwallet/openxwallet-custody-registry.schema.yaml` | `100644` | `306a84dda2fe29057ee440e871ab0dd064cd2ceb` | yes |
| 70 | `contracts/openxwallet/openxwallet-custody.registry.yaml` | `100644` | `da6dc0ca07b90ee1475f2845b4cf37b1dc739b68` | yes |
| 71 | `contracts/openxwallet/openxwallet-distinct-holder-constraint.schema.yaml` | `100644` | `6deffcaef0bc9245b659abf0986d790c8e9171ee` | yes |
| 72 | `contracts/openxwallet/openxwallet-grant-exercise.schema.yaml` | `100644` | `59fb611d06e306e4fb433063c837dd4a664e8e14` | yes |
| 73 | `contracts/openxwallet/openxwallet-grant.schema.yaml` | `100644` | `83624af789d340847ab87be88dc767c297ac11b2` | yes |
| 74 | `contracts/openxwallet/openxwallet-record.schema.yaml` | `100644` | `1089178792ea0fc187811de413e30afb83f2012a` | yes |
| 75 | `contracts/openxwallet/openxwallet-subject-attestation.schema.yaml` | `100644` | `23ee5370bb6cd5ba5bfa85cd3a87c398693e9c7d` | yes |
| 76 | `scripts/validate-openxwallet.py` | `100755` | `08a4b5c758eba0e60c58f83b4fadb1a34d2dcde9` | yes |
| 77 | `scripts/wallet-yaml-syntax-gate.py` | `100644` | `2a5eb8598162cde56c74a7d48ee2d2d873b48f7a` | yes |
| 78 | `tests/multi_key_wallets/test_declared_key_sets.py` | `100644` | `879f6e030b474a4b9c536af8d0126537cd2b7bee` | yes |
| 79 | `tests/nested_repo_prune/test_prune_and_register_note.py` | `100644` | `fd71629a3f3535e1a6a585e1eb7226df24085cf9` | yes |
| 80 | `tests/wallet_yaml_syntax_gate/test_gate.py` | `100644` | `11d7beddc9a6b9b84a48f821c11c5149a1034c34` | yes |

</details>

<details>
<summary><code>openwallet_spec</code>: 38/38 paths, identical blob and mode</summary>

| # | path | mode | git blob (carve commit = carve layer) | sha256 = manifest |
| ---: | --- | --- | --- | --- |
| 1 | `openspec/changes/add-composition-drift-cascade/.openspec.yaml` | `100644` | `53ae27019b83bfcd1ae596d0585c157ee78c8ed0` | yes |
| 2 | `openspec/changes/add-composition-drift-cascade/design.md` | `100644` | `a46c32b0c13b14bf989a09eea291936696a8dbb8` | yes |
| 3 | `openspec/changes/add-composition-drift-cascade/proposal.md` | `100644` | `e1731efec076abfc327f0fd20249c0c6114242ac` | yes |
| 4 | `openspec/changes/add-composition-drift-cascade/specs/openxwallet-agent-profile/spec.md` | `100644` | `38ee2bd5bc062f829245fd79e3e927e2afe81d0a` | yes |
| 5 | `openspec/changes/add-composition-drift-cascade/specs/openxwallet/spec.md` | `100644` | `bdde5296046952cb7800cfe5e837ed351343750c` | yes |
| 6 | `openspec/changes/add-composition-drift-cascade/tasks.md` | `100644` | `1f1d25f3dc043ef589e63b0f50a5b26972e1ab11` | yes |
| 7 | `openspec/changes/archive/2026-08-08-add-openxwallet/.openspec.yaml` | `100644` | `ca30e246f3480a297c1595ed38fc53c1929dc995` | yes |
| 8 | `openspec/changes/archive/2026-08-08-add-openxwallet/design.md` | `100644` | `0346f90217d7b7558ff2544823aa5b6dbe56a2b7` | yes |
| 9 | `openspec/changes/archive/2026-08-08-add-openxwallet/proposal.md` | `100644` | `b0d53cb19301115e4a52c84a57a5a652e60f6221` | yes |
| 10 | `openspec/changes/archive/2026-08-08-add-openxwallet/specs/openxwallet-agent-profile/spec.md` | `100644` | `4deaf791b5041fd58cdab4c9681c411fbf41f358` | yes |
| 11 | `openspec/changes/archive/2026-08-08-add-openxwallet/specs/openxwallet/spec.md` | `100644` | `8b582cb6c75f3488e13e5860fd15027e17e36fe8` | yes |
| 12 | `openspec/changes/archive/2026-08-08-add-openxwallet/tasks.md` | `100644` | `52c37af1bc1455957e16bd9abbddb34a7e26ebe9` | yes |
| 13 | `openspec/changes/archive/2026-10-08-add-multi-key-wallets/design.md` | `100644` | `80b911cf6dc43e72771274d56c7bd402226c1b87` | yes |
| 14 | `openspec/changes/archive/2026-10-08-add-multi-key-wallets/proposal.md` | `100644` | `d31ad51540527254ff0d84cc5868db015fe0e752` | yes |
| 15 | `openspec/changes/archive/2026-10-08-add-multi-key-wallets/specs/openxwallet/spec.md` | `100644` | `30d57a61f83c6944baac5a6ff97073c927c824cc` | yes |
| 16 | `openspec/changes/archive/2026-10-08-add-multi-key-wallets/tasks.md` | `100644` | `7ed40bfa18079d8b393bb3929f9d08e215df2747` | yes |
| 17 | `openspec/config.yaml` | `100644` | `b4bbeb946f4c4d9310ee8730c5f89564bc95e9f0` | yes |
| 18 | `openspec/specs/openxwallet-agent-profile/spec.md` | `100644` | `9cbccca950dbe2332256f31a9697b9cd6d812ce2` | yes |
| 19 | `openspec/specs/openxwallet/spec.md` | `100644` | `b8e8eba7e4e95431a3e39d24d5f38ece4ef92080` | yes |
| 20 | `specs/006-openxwallet-contracts/evidence/red-proof-output.txt` | `100644` | `0816e2192ee8b09af7267593bd3ed254c1a95c90` | yes |
| 21 | `specs/006-openxwallet-contracts/evidence/red-proof.py` | `100755` | `a466342e1c29702d03c5a11e2aa2830078022c82` | yes |
| 22 | `specs/006-openxwallet-contracts/plan.md` | `100644` | `67cc7d8ff931dc96bc6341d286dfa13779d57c04` | yes |
| 23 | `specs/006-openxwallet-contracts/research.md` | `100644` | `45c696411bf5c709c677d8e3c920b2b411ab52b8` | yes |
| 24 | `specs/006-openxwallet-contracts/spec.md` | `100644` | `a93e5cc557122596cc22508a7194ee034ffd1994` | yes |
| 25 | `specs/006-openxwallet-contracts/tasks.md` | `100644` | `4d834e88caeb4ea5055d404f40c48e1e06b0cb53` | yes |
| 26 | `specs/006-openxwallet-contracts/traceability.yaml` | `100644` | `000764e42d3897637a450a306c798c95b43f449a` | yes |
| 27 | `specs/010-wallet-validator-ci/checklists/requirements.md` | `100644` | `611718fc2654a7a0c8ad372d42b93b86492728be` | yes |
| 28 | `specs/010-wallet-validator-ci/clarify-questions.md` | `100644` | `391c23497403918866cdf76d0790822a095e90ee` | yes |
| 29 | `specs/010-wallet-validator-ci/data-model.md` | `100644` | `623fe605ac774169f4c73543356a9d263c5b928c` | yes |
| 30 | `specs/010-wallet-validator-ci/implementation-notes.md` | `100644` | `90503e003fc90f7dc072c2bf213c244065cf6c2b` | yes |
| 31 | `specs/010-wallet-validator-ci/plan.md` | `100644` | `746ee1f8add6c7363f9aec28f95f999a88a4d788` | yes |
| 32 | `specs/010-wallet-validator-ci/quickstart.md` | `100644` | `1e24c71cb531340f0dfd36dcbec35354aefa8a99` | yes |
| 33 | `specs/010-wallet-validator-ci/research.md` | `100644` | `23be7bfac67ad343b800d594e1b4367f7ede6fe4` | yes |
| 34 | `specs/010-wallet-validator-ci/spec.md` | `100644` | `6342de466547e802af95064aa29ca863d9b0d42c` | yes |
| 35 | `specs/010-wallet-validator-ci/tasks.md` | `100644` | `3bee1b1c0f7d309627e5e02a22a2ace3b7d9b5fe` | yes |
| 36 | `specs/015-multi-key-wallets/plan.md` | `100644` | `c434122de2252aacd3657d24a1a48ddd4228766e` | yes |
| 37 | `specs/015-multi-key-wallets/spec.md` | `100644` | `4853fd63a1314fa11c8840d9fc86556a63176a39` | yes |
| 38 | `specs/015-multi-key-wallets/tasks.md` | `100644` | `2cf620f589713b103e3535b6c02eaa23c38c2142` | yes |

</details>

<details>
<summary><code>openwallet_root</code>: 10/10 paths, identical blob and mode</summary>

| # | path | mode | git blob (carve commit = carve layer) | sha256 = manifest |
| ---: | --- | --- | --- | --- |
| 1 | `LICENSE` | `100644` | `11742a6ab69903497f7ddd74ac2a62961623e4fb` | yes |
| 2 | `contracts/CHANGELOG.md` | `100644` | `bde8cedd18a1a5bac6b1d5fa3c51ff3ed09e29f3` | yes |
| 3 | `contracts/manifest.yaml` | `100644` | `4ece666ce85c9133531cd2bc1c19427a9aa19137` | yes |
| 4 | `contracts/releases/wallet-v1.0.digests.yaml` | `100644` | `9f380c79c2d7944df145da45c02f62e86414ee4b` | yes |
| 5 | `contracts/releases/wallet-v1.1.digests.yaml` | `100644` | `cacb7b88d606ec0155a53aefda91b88cfd766144` | yes |
| 6 | `contracts/releases/wallet-v1.2.digests.yaml` | `100644` | `5cbf104572682c91330e3db1bad75332bffa97d1` | yes |
| 7 | `contracts/releases/wallet-v1.3.digests.yaml` | `100644` | `19127ea68b9475b30331f62fff545ab44204b069` | yes |
| 8 | `contracts/releases/wallet-v1.4.digests.yaml` | `100644` | `8640d0a5cf39fbdecdb2c2cf85f5b761c29386b1` | yes |
| 9 | `contracts/releases/wallet-v1.5.digests.yaml` | `100644` | `d3972f100a058beffc24b0408b9ac5b6dd84622e` | yes |
| 10 | `docs/byte-identity-wallet-v1.0.md` | `100644` | `0671390d7eba96fe1e1990621731f3cebb1fc357` | yes |

</details>

**At each commit A, nothing but the carve layer arrived.** These were run from
inside each leg. `paths-<DEST>.txt` is `bin/carve-paths.py`'s output:

```bash
cd "$WORK/root/code" || exit 1          # and likewise in spec/, with the spec leg's A
A=32c933551b92d83122a45847215d5ebe92ae6740
git diff --stat $A^2 $A -- $(cat ../../paths-openwallet_code.txt)                  # 0 lines: EMPTY
git diff --stat $A^1 $A -- . $(sed 's/^/:!/' ../../paths-openwallet_code.txt)      # 0 lines: EMPTY
python3 ../../bin/declared-edits.py openwallet_code "$MANIFEST" $A^2 $A^1 $A
python3 ../../bin/declared-lines-exact.py openwallet_code "$MANIFEST" $A^2 $A | tail -n 1
```

```
openwallet_code: 80 carved row(s); 0 edited on declared lines only; 4 declaring edits left unapplied; 0 refusal(s)
openwallet_code: 0 refusal(s)
openwallet_spec: 38 carved row(s); 0 edited on declared lines only; 4 declaring edits left unapplied; 0 refusal(s)
openwallet_spec: 0 refusal(s)
```

Both `diff`s are empty in each leg, and every command exits 0. At the root, the
carve layer and its declared edit arrive in the one lockstep commit, so there is
no separate commit A. Its carve layer is `b48bcb2^2`, recorded above.

**Part two (a): RUN-GREEN.** 80/80, 38/38 and 10/10 paths are identical in git
blob and mode at the carve layer. Commit A of each leg is the pure carve.

---

## Part two (b) — the declared-edit layer: every difference is declared

After the carve layer, a destination may differ from it in three ways only:
- on a line its manifest row declares, under one of the five closed edit
  classes;
- by a closed declared addition: the corpus binding (Q6) and each leg's
  `LICENSE`;
- at the root, by the lockstep move of both gitlinks and both pins.

Two helpers judge it. A line or a path in no class REFUSES:
- helper 3 (`declared-edits.py`) judges paths, modes and, through `git diff
  -U0 --diff-algorithm=histogram`, lines;
- helper 5 (`declared-lines-exact.py`) judges lines with no diff algorithm, and
  is the authority where the two disagree.

`attribute.py` then breaks the changed lines down per declared edit.

### The code leg, A → B, and A → the pinned commit

```bash
cd "$WORK/root/code" || exit 1
A=32c933551b92d83122a45847215d5ebe92ae6740; B=75b990dc7ea99823626c18816b37d971f46e341b
BIND=contracts/openxwallet/examples/approval-vocabulary.binding.yaml
git diff --name-status $A $B
python3 ../../bin/declared-edits.py openwallet_code "$MANIFEST" $A^2 $A^1 $B --added LICENSE --added $BIND
python3 ../../bin/declared-lines-exact.py openwallet_code "$MANIFEST" $A^2 $B
python3 ../../bin/declared-edits.py openwallet_code "$MANIFEST" $A^2 $A^1 72313daab1f229c049cb90998931564c1904dbbc --added LICENSE --added $BIND
python3 ../../proof-bin/attribute.py openwallet_code "$MANIFEST" $A^2 $B
```

```
M	.github/workflows/wallet-validation.yml
A	LICENSE
A	contracts/openxwallet/examples/approval-vocabulary.binding.yaml
M	scripts/validate-openxwallet.py
M	tests/multi_key_wallets/test_declared_key_sets.py
M	tests/nested_repo_prune/test_prune_and_register_note.py

openwallet_code: 80 carved row(s); 4 edited on declared lines only; 0 declaring edits left unapplied; 0 refusal(s)
exit=0

ok     .github/workflows/wallet-validation.yml: 8 declared line(s) in 1 run(s); 46 undeclared line(s) preserved in order: True
ok     scripts/validate-openxwallet.py: 1621 declared line(s) in 15 run(s); 1928 undeclared line(s) preserved in order: True
ok     tests/multi_key_wallets/test_declared_key_sets.py: 6 declared line(s) in 2 run(s); 552 undeclared line(s) preserved in order: True
ok     tests/nested_repo_prune/test_prune_and_register_note.py: 172 declared line(s) in 5 run(s); 390 undeclared line(s) preserved in order: True
openwallet_code: 0 refusal(s)
exit=0

openwallet_code: 80 carved row(s); 4 edited on declared lines only; 0 declaring edits left unapplied; 0 refusal(s)
exit=0
```

Only the four declaring rows and the two declared additions changed. The other
76 carved rows stand exactly as carved at `72313daa`, the commit this root pins.

**Every changed validator line falls in hunk (a)–(e).** `attribute.py`'s
breakdown follows. Line numbers are the carve-commit blob's. "Removed or
replaced" counts the lines that the histogram diff takes out:

| Hunk | Declared lines (carve-commit numbering) | Declared | Removed or replaced |
| --- | --- | ---: | ---: |
| (a) remove the envelope | :254, :3498-3503, :3529-3530 | 9 | 6 |
| (b) the vocabulary from ONE DECLARED BINDING (Q6) | :73-78, :422-428, :3507 | 14 | 12 |
| (c) rule (t) out to the adapter | :172-181, :256-283, :323-328, :986-1032, :1789-1974 | 277 | 275 |
| (d) the register reader out to the adapter | :183-212, :2036-2558, :2561-3326, :3464-3465 | 1 321 | 1 316 |
| (e) the EMPTY extension points (Q1), at the anchors (c) and (d) vacate | :986, :1789, :2036, :3464 | 4 | 3 |
| **`scripts/validate-openxwallet.py`** | the union (the four anchors of (e) lie inside (c) or (d)) | **1 621** | **1 609**, in no declared edit: **0** |

| Other edited row | Class | Declared | Removed or replaced | In no declared edit |
| --- | --- | ---: | ---: | ---: |
| `.github/workflows/wallet-validation.yml` :44-51 | envelope-verify step | 8 | 8 | 0 |
| `tests/multi_key_wallets/test_declared_key_sets.py` :108-111, :117-118 | test split (amended) | 6 | 6 | 0 |
| `tests/nested_repo_prune/test_prune_and_register_note.py` :1, :4-7, :40-42, :47-48, :247-408 | test split | 172 | 169 | 0 |

```
openwallet_code: removed or replaced line(s) in no declared edit: 0
exit=0
```

A declared line that the diff leaves standing is permitted. A declaration
bounds the edit; it is not a quota. Helper 5 is the stricter statement: every
undeclared run of the carve blob, 1 928 lines of the validator, stands in the
new blob unchanged and in order.

### The spec leg, A → B, and A → the pinned commit

```bash
cd "$WORK/root/spec" || exit 1
A=c788cba28a81b0dc17da4cea5db1e57eceb3a193; B=5ea9539428eae850ba71e6f0ba8a38db061e809a
git diff --name-status $A $B
python3 ../../bin/declared-edits.py openwallet_spec "$MANIFEST" $A^2 $A^1 $B --added LICENSE
python3 ../../bin/declared-lines-exact.py openwallet_spec "$MANIFEST" $A^2 $B
python3 ../../bin/declared-edits.py openwallet_spec "$MANIFEST" $A^2 $A^1 15c15bbd451a803f0acdb24e5234836db829a2d3 --added LICENSE
```

```
A	LICENSE
M	openspec/changes/add-composition-drift-cascade/specs/openxwallet-agent-profile/spec.md
M	openspec/changes/add-composition-drift-cascade/specs/openxwallet/spec.md
M	openspec/specs/openxwallet-agent-profile/spec.md
M	openspec/specs/openxwallet/spec.md

openwallet_spec: 38 carved row(s); 4 edited on declared lines only; 0 declaring edits left unapplied; 0 refusal(s)
exit=0

ok     openspec/changes/add-composition-drift-cascade/specs/openxwallet-agent-profile/spec.md: 1 declared line(s) in 1 run(s); 73 undeclared line(s) preserved in order: True
ok     openspec/changes/add-composition-drift-cascade/specs/openxwallet/spec.md: 2 declared line(s) in 2 run(s); 79 undeclared line(s) preserved in order: True
ok     openspec/specs/openxwallet-agent-profile/spec.md: 3 declared line(s) in 3 run(s); 66 undeclared line(s) preserved in order: True
ok     openspec/specs/openxwallet/spec.md: 8 declared line(s) in 8 run(s); 237 undeclared line(s) preserved in order: True
openwallet_spec: 0 refusal(s)
exit=0

openwallet_spec: 38 carved row(s); 4 edited on declared lines only; 0 declaring edits left unapplied; 0 refusal(s)
exit=0
```

`attribute.py` gives 8/8, 3/3, 2/2 and 1/1 declared lines replaced, 14 in all,
and `in no declared edit: 0`. Those are the eleven requirement subjects
(`openXwallet SHALL` → `openWallet SHALL`) plus the travelling change's three
occurrences. Under the ruling "keep the prefix", no capability id, `kind:`,
finding code or file name moved.

#### After the carve: the `spec` pin follows the leg's `main` through declared changes

This is policy. Brett Heap ruled it twice on 2026-10-09, labels verbatim:
- **"Re-pin spec to 1506bbdb before the tag (Recommended)"**: the spec leg's
  4.8 merge, `1506bbdb4194a779bef63d8c4e5eecc7eac0bd68`
  (opensoft/openWallet-spec#3). It adds the birth change
  `bind-approval-posture-vocabulary`, status proposed.
- **"Re-pin to the archive merge before the tag (Recommended)"**: that
  change's archive, opensoft/openWallet-spec#4's merge.

Each moves this root's `spec` gitlink and `contracts/spec-pin.yaml` in its own
lockstep root commit, and the release record at tag time names the pinned
commit. The carve's byte-identity claims are made at the carve layer and
A → B, whose tree `15c15bbd` carries. A later spec commit is that, plus
declared post-carve changes made through the leg's own OpenSpec instance. Those
changes are outside the claims. The snapshot below records them as measured,
not as judged:

```bash
cd "$WORK/root/spec" || exit 1
git fetch -q origin main && git rev-parse origin/main
git diff --stat 15c15bbd451a803f0acdb24e5234836db829a2d3 1506bbdb4194a779bef63d8c4e5eecc7eac0bd68
git diff --stat -M 1506bbdb4194a779bef63d8c4e5eecc7eac0bd68 origin/main
git diff --name-status -M 1506bbdb4194a779bef63d8c4e5eecc7eac0bd68 origin/main
git diff --name-only 15c15bbd451a803f0acdb24e5234836db829a2d3 origin/main -- . ':!openspec/' | wc -l
A=c788cba28a81b0dc17da4cea5db1e57eceb3a193
for C in 1506bbdb4194a779bef63d8c4e5eecc7eac0bd68 origin/main; do      # the change's own new files declared as the additions
  python3 ../../bin/declared-edits.py openwallet_spec "$MANIFEST" $A^2 $A^1 $C --added LICENSE \
      $(git diff --name-only --diff-filter=A 15c15bbd451a803f0acdb24e5234836db829a2d3 $C | sed 's/^/--added /') | tail -n 2
  python3 ../../bin/declared-lines-exact.py openwallet_spec "$MANIFEST" $A^2 $C | grep -E '^REFUSE|refusal'
done
```

```
1924500354f472a6298c02db44a3ae2b21b8908e
 .../.openspec.yaml                                 |  44 +++++
 .../bind-approval-posture-vocabulary/design.md     | 183 +++++++++++++++++++++
 .../bind-approval-posture-vocabulary/proposal.md   | 134 +++++++++++++++
 .../specs/openxwallet-agent-profile/spec.md        |  31 ++++
 .../bind-approval-posture-vocabulary/tasks.md      |  89 ++++++++++
 5 files changed, 481 insertions(+)
 .../.openspec.yaml                                 | 18 +++++++-
 .../design.md                                      |  0
 .../proposal.md                                    | 48 +++++++++++++++++-----
 .../specs/openxwallet-agent-profile/spec.md        |  0
 .../tasks.md                                       | 45 ++++++++++++++++++--
 openspec/specs/openxwallet-agent-profile/spec.md   | 23 +++++++----
 6 files changed, 112 insertions(+), 22 deletions(-)
R071	openspec/changes/bind-approval-posture-vocabulary/.openspec.yaml	openspec/changes/archive/2026-10-09-bind-approval-posture-vocabulary/.openspec.yaml
R100	openspec/changes/bind-approval-posture-vocabulary/design.md	openspec/changes/archive/2026-10-09-bind-approval-posture-vocabulary/design.md
R078	openspec/changes/bind-approval-posture-vocabulary/proposal.md	openspec/changes/archive/2026-10-09-bind-approval-posture-vocabulary/proposal.md
R100	openspec/changes/bind-approval-posture-vocabulary/specs/openxwallet-agent-profile/spec.md	openspec/changes/archive/2026-10-09-bind-approval-posture-vocabulary/specs/openxwallet-agent-profile/spec.md
R062	openspec/changes/bind-approval-posture-vocabulary/tasks.md	openspec/changes/archive/2026-10-09-bind-approval-posture-vocabulary/tasks.md
M	openspec/specs/openxwallet-agent-profile/spec.md
0
openwallet_spec: 38 carved row(s); 4 edited on declared lines only; 0 declaring edits left unapplied; 0 refusal(s)
openwallet_spec: 0 refusal(s)
REFUSE undeclared line(s) in openspec/specs/openxwallet-agent-profile/spec.md: [4, 5, 53, 54, 55, 56, 67, 68, 69]
openwallet_spec: 38 carved row(s); 3 edited on declared lines only; 0 declaring edits left unapplied; 1 refusal(s)
REFUSE openspec/specs/openxwallet-agent-profile/spec.md: 3 declared line(s) in 3 run(s); 66 undeclared line(s) preserved in order: False
openwallet_spec: 1 refusal(s)
```

The spec leg's `main` had already reached the archive merge, `19245003`, when
this was run. What the snapshot shows:
- **At `1506bbdb`**, `15c15bbd` gains exactly the change's five new files
  under `openspec/changes/bind-approval-posture-vocabulary/`, and nothing else.
  Every carved row stands as commit B left it: helper 5 gives 0 refusals, and
  helper 3 gives 0 once those five files are the declared additions.
- **At the archive merge**, the change's directory is renamed under
  `openspec/changes/archive/2026-10-09-bind-approval-posture-vocabulary/`.
  Archiving also promotes the change's requirement text into the canonical
  `openspec/specs/openxwallet-agent-profile/spec.md` (+16 −7), which is a
  carved row. The carve's helpers refuse that row there, as they must: it is a
  post-carve change, not a carve edit.
- **Throughout**, nothing outside `openspec/` moved, and the code leg did not
  move.

At the run, this root's `main` was `5a444cf22c7d6bae307223010d4d2008b04e9c51`,
opensoft/openWallet#4's merge, which pins `spec` at `1506bbdb`.
opensoft/openWallet#5, which re-pins it at the archive merge `19245003`, was
open; it has since landed as `bead4bd8`. This document's branch then still
pinned `15c15bbd`, the commit parts zero to five measured.

### The root: the lockstep commit, HEAD^2 → HEAD

```bash
cd "$WORK/root" || exit 1
L=b48bcb20b31dece4d582444cf01f617a799d297d
git diff --name-status $L^2 $L -- $(cat ../paths-openwallet_root.txt)          # the declared edit
git diff --name-status $L^1 $L -- . $(sed 's/^/:!/' ../paths-openwallet_root.txt)   # the lockstep move
python3 ../bin/declared-edits.py openwallet_root "$MANIFEST" $L^2 $L^1 $L \
    --may-change spec --may-change code --may-change contracts/spec-pin.yaml --may-change contracts/code-pin.yaml
python3 ../bin/declared-lines-exact.py openwallet_root "$MANIFEST" $L^2 $L
python3 ../proof-bin/attribute.py openwallet_root "$MANIFEST" $L^2 $L
```

```
M	contracts/manifest.yaml

M	code
M	contracts/code-pin.yaml
M	contracts/spec-pin.yaml
M	spec

openwallet_root: 10 carved row(s); 1 edited on declared lines only; 0 declaring edits left unapplied; 0 refusal(s)
exit=0

ok     contracts/manifest.yaml: 67 declared line(s) in 10 run(s); 177 undeclared line(s) preserved in order: True
openwallet_root: 0 refusal(s)
exit=0

  contracts/manifest.yaml edit 1 [manifest field edits]: declared 67, removed or replaced 66
contracts/manifest.yaml: 66 line(s) removed or replaced; in no declared edit: 0
openwallet_root: removed or replaced line(s) in no declared edit: 0
exit=0
```

These are the manifest field edits:
- `carved_from:` (:52-54); its header line :52 is declared and stands
  unchanged;
- each owned row's `path:` gaining `code/`, with its `source_path:` (:76-77,
  :106-107, :119-120, :132-133, :145-146, :158-159, :171-172, :184-185);
- the consumed `hermes-job-envelope` row and its comment block removed
  (:197-244).

Nothing else differs from either parent.

**After the lockstep commit, only this root's own documentation moved.**
`git diff --name-status b48bcb2 1c68717f` lists `AGENTS.md`, `README.md` and
`docs/openwallet-cutover-runbook.md`, all modified. None is a carved row or a
pin. Helper 3 run to `1c68717f`, with those three added to `--may-change`,
prints the same `1 edited on declared lines only; 0 declaring edits left
unapplied; 0 refusal(s)`. Helper 5 run to `1c68717f` prints
`openwallet_root: 0 refusal(s)`.

**The declared additions are closed, and both kinds are accounted for.**
- The corpus binding: one file,
  `contracts/openxwallet/examples/approval-vocabulary.binding.yaml`, in the
  code leg.
- `LICENSE` in each leg. `git ls-tree HEAD LICENSE` gives blob
  `11742a6ab69903497f7ddd74ac2a62961623e4fb` at this root, in `code`, in `spec`
  and in the root's carve layer. These are the same Apache-2.0 bytes the root
  received by the carve.

**Part two (b): RUN-GREEN.** All of it is declared:
- code: 4 rows edited on declared lines only, 1 609 + 8 + 6 + 169 lines removed
  or replaced, none outside a declared edit;
- spec: 4 rows, 14 lines;
- root: 1 row, 66 lines, plus the four lockstep paths;
- additions: the corpus binding and two `LICENSE`s.

0 refusals from helper 3 and from helper 5, at every commit B, at each pinned
leg commit, at the lockstep commit and at `1c68717f`.

---

## Part three — behaviour, run from the CODE leg's own root

A wallet validator run from this root prunes both legs and scans nothing (D7,
measured in D0), so part three runs from inside the code leg. It runs at the
commit this root pins, with the invocations of the leg's own
`wallet-validation` and `pytest-suite` workflows and the packages they install.

### First half — openWallet standalone: RUN

```bash
cd "$WORK/root/code" || exit 1
git rev-parse HEAD                                   # 72313daab1f229c049cb90998931564c1904dbbc
python3 scripts/wallet-yaml-syntax-gate.py .
python3 scripts/validate-openxwallet.py .
python3 scripts/validate-openxwallet.py . --strict
python3 -m pytest tests/ -q
```

```
$ python3 scripts/wallet-yaml-syntax-gate.py .
exit=0
$ python3 scripts/validate-openxwallet.py .
note  approval-scope vocabulary: none bound; a repo scan refuses every approval_posture key, and the packaged corpus is adjudicated under its own binding, contracts/openxwallet/examples/approval-vocabulary.binding.yaml
note  wallet 'wal-agent-council-0011': 4 declared key(s) adjudicated (key-council-primary-0011, key-council-retired-0011, key-council-seat-a-0011, key-council-seat-b-0011)
note  corpus: 21 positive example(s), 42 negative confirmation(s) across 11/11 requirements
note  repo scan: 0 openxWallet artifact(s) validated, 9 document(s) skipped as another kind

validate-openxwallet: 0 error(s), 0 warning(s)
exit=0
$ python3 scripts/validate-openxwallet.py . --strict
(the same five lines)
validate-openxwallet: 0 error(s), 0 warning(s)
exit=0
$ python3 -m pytest tests/ -q
.................................s....                                   [100%]
37 passed, 1 skipped in 21.09s
exit=0
```

**21 / 42 / 11 of 11**, as the code leg prints them: `corpus: 21 positive
example(s), 42 negative confirmation(s) across 11/11 requirements`. The 42 are
the carved negatives counted in part one (a). Each one is adjudicated and must
fail with its expected code. 11/11 is the standalone requirement table, which
excludes OXWR-R1/R2 and the register rows (they move to the adapter in hunks (c)
and (d)).

The one skip is loud and expected. It is
`test_this_version_adjudicates_the_previous_corpus_identically`, and its reason
reads "no git blob for a DIFFERENT, previous scripts/validate-openxwallet.py is
reachable from this checkout". The test looks for the previous validator on
`origin/main`, `main` and the first parent. At the leg's `main`, the first parent
is the scaffold, which carried no validator. The test refuses to compare the
validator with itself, so it skips with its reason. It skipped in the leg's own
CI on the same grounds (task 4.4: 37 passed, 1 skipped).

**A posture under NO binding is refused.** The validator's caller binding is
`VOCABULARY_BINDING`. It is `None` in a standalone run, which declares no
binding. A scratch tree outside every clone holds two documents: one carved
positive grant that carries an `approval_posture`, and the wallet it names. The
tree is scanned three ways:
- (i) as it is;
- (ii) with the posture deleted, so that the posture is shown to be the only
  thing refused;
- (iii) with the posture restored and a caller binding declared, in process,
  as a composing layer would declare it.

```bash
cd "$WORK/root/code" || exit 1
T=$WORK/posture-tree; mkdir -p "$T"
cp contracts/openxwallet/examples/grant-council-act-tier.example.yaml "$T/grant.yaml"
cp contracts/openxwallet/examples/wallet-agent-council-multi-key.example.yaml "$T/wallet.yaml"
python3 scripts/validate-openxwallet.py "$T"                                   # (i)
sed -i '/approval_posture:/,/irreversible_external_effect/d' "$T/grant.yaml"
python3 scripts/validate-openxwallet.py "$T"                                   # (ii)
cp contracts/openxwallet/examples/grant-council-act-tier.example.yaml "$T/grant.yaml"
printf 'terms:\n  hermes_approval_required_before_apply: {type: boolean}\n  authority_agents_may_approve: {type: boolean}\n  human_escalation_required_for: {type: array}\n' > "$WORK/caller-binding.yaml"
python3 - "$T" "$WORK/caller-binding.yaml" <<'PY'                              # (iii)
import importlib.util, sys
target, binding = sys.argv[1:3]
spec = importlib.util.spec_from_file_location("core", "scripts/validate-openxwallet.py")
core = importlib.util.module_from_spec(spec); spec.loader.exec_module(core)
core.VOCABULARY_BINDING = {"document": binding, "pointer": ["terms"], "label": "a caller's declared binding"}
sys.argv = ["validate-openxwallet.py", target]
rc = core.main(); print(f"exit={rc}")
PY
```

```
(i)  note  approval-scope vocabulary: none bound; a repo scan refuses every approval_posture key, and the packaged corpus is adjudicated under its own binding, contracts/openxwallet/examples/approval-vocabulary.binding.yaml
     note  repo scan: 2 openxWallet artifact(s) validated, 0 document(s) skipped as another kind
     ERROR [authority-vocabulary-parallel] $WORK/posture-tree/grant.yaml: approval_posture names 'authority_agents_may_approve', which is not an `approval_policy` property of the neutral job envelope (legal terms: []). An agent's authority and a job's approval posture are one vocabulary, not two kept in agreement
     ERROR [authority-vocabulary-parallel] $WORK/posture-tree/grant.yaml: approval_posture names 'hermes_approval_required_before_apply', which is not an `approval_policy` property of the neutral job envelope (legal terms: []). An agent's authority and a job's approval posture are one vocabulary, not two kept in agreement
     ERROR [authority-vocabulary-parallel] $WORK/posture-tree/grant.yaml: approval_posture names 'human_escalation_required_for', which is not an `approval_policy` property of the neutral job envelope (legal terms: []). An agent's authority and a job's approval posture are one vocabulary, not two kept in agreement
     validate-openxwallet: 3 error(s), 0 warning(s)
     exit=1
(ii) note  repo scan: 2 openxWallet artifact(s) validated, 0 document(s) skipped as another kind
     validate-openxwallet: 0 error(s), 0 warning(s)
     exit=0
(iii) note  approval-scope vocabulary read from a caller's declared binding: ['authority_agents_may_approve', 'hermes_approval_required_before_apply', 'human_escalation_required_for']
     note  repo scan: 2 openxWallet artifact(s) validated, 0 document(s) skipped as another kind
     validate-openxwallet: 0 error(s), 0 warning(s)
     exit=0
```

Under no binding the legal terms are `[]`, and every key of the posture is
refused under the existing code `authority-vocabulary-parallel` (D4, RULED Q6).
Nothing else in the tree is refused, because without the posture the same tree
is clean. The same posture under a declared binding is admitted. The packaged
corpus, meanwhile, is adjudicated under its own corpus binding in all three
runs, and never reds (`21 / 42 / 11 of 11` in each).

**Part three, first half: RUN-GREEN.** 21 / 42 / 11 of 11, plain and
`--strict`; the syntax gate 0; pytest 37 passed, 1 skipped; a posture under no
binding refused.

### Second half — D5's neutrality gate over the composed adapter: RUN

Run 2026-10-09 (UTC), by lane `openXwallet-2`, under the ruling "Start now,
neutrality half later (Recommended)". The composed adapter is task 5.2, built by
lane `openXwallet-3` on its branch `rebuild/adapter-group-5` of
opensoft/openXwallet. The run measured that branch's head at the time,
`a02c6c7487171c110490b234643a7e586ed47153`, which sits on openXwallet `main`
`206e0d4f`. The branch could still move before its pull request opened, so the
commit that landed was to be confirmed by running this half's commands again at
it. Group 5 landed as `815b86ce`, opensoft/openXwallet#40's merge of a second
branch, `rebuild/adapter-group-5-r2` (head `36c365da`), whose history does not
contain `a02c6c74`. This half's commands, run again there on 2026-10-09,
re-confirm it (below).

**The claim** (D5; `tasks.md` 5.4) has three conditions. The carve-commit
validator and the composed adapter, run over the same tree, must:
- print byte-identical output, stdout and stderr taken together;
- exit with the same code;
- do both plain and `--strict`.

The trees are three kinds:
- (i) openXwallet's own tree, at `a02c6c74`, and again at `815b86ce`;
- (ii) an export of openxFactory's live `governance/` tree;
- (iii) every fixture tree the kept and moved test suites build.

**The adapter, and the two validators side by side.**

```bash
cd "$WORK" || exit 1
git clone -q https://github.com/opensoft/openXwallet.git oxw-adapter
git -C oxw-adapter checkout -q a02c6c7487171c110490b234643a7e586ed47153     # rebuild/adapter-group-5's head at the run
git -C oxw-adapter submodule update -q --init openWallet
git -C oxw-adapter/openWallet submodule update -q --init code
test "$(git -C oxw-adapter/openWallet rev-parse HEAD)" = 1c68717f1ae4ae132d6942f8c7f533baf292d0b6
test "$(git -C oxw-adapter/openWallet/code rev-parse HEAD)" = 72313daab1f229c049cb90998931564c1904dbbc
(cd oxw-adapter && python3 scripts/verify-openwallet-pin.py)
git -C oxw-adapter worktree add -q --detach "$WORK/oxw-carve" "$CARVE_COMMIT"   # the carve-commit validator, in its own tree
neutral() {   # usage: neutral TREE [--strict]; the composed side is $ADAPTER, by default $WORK/oxw-adapter
  ( cd "$WORK/oxw-carve"               && python3 -B scripts/validate-openxwallet.py "$@" ) > before.txt 2>&1; echo "exit=$?" >> before.txt
  ( cd "${ADAPTER:-$WORK/oxw-adapter}" && python3 -B scripts/validate-openxwallet.py "$@" ) > after.txt  2>&1; echo "exit=$?" >> after.txt
  if diff before.txt after.txt > /dev/null; then echo "EMPTY $* ($(tail -n 1 after.txt))"; else echo "DIFFERS $*"; diff before.txt after.txt; fi
}
mkdir -p "$WORK/gate"
```

```
OK openwallet-pin verified: openWallet@1c68717f1ae4ae132d6942f8c7f533baf292d0b6 (tag label <none yet>), gitlink read from HEAD, code leg @72313daab1f229c049cb90998931564c1904dbbc in lockstep (gitlink, contracts/code-pin.yaml, legs.code), 8 digest(s) recomputed, 6 path-only member(s) present
```

The adapter pins this root at `1c68717f`, the commit parts zero to five
measured, and its code leg at `72313daa`. At `815b86ce` it pins `b0af7c2c`; the
code leg is still `72313daa`. The rest of the setup works like this:
- Each side's stdout and stderr go to one file, with the exit code appended,
  so one `diff` judges all three conditions at once.
- `python3 -B` keeps the composed run from leaving a bytecode cache behind.
  The adapter path-loads the pinned core. Without `-B`, a git-ignored
  `openWallet/code/scripts/__pycache__/` appeared inside tree (i).

**(i) openXwallet's own tree and (ii) the openxFactory export.**

```bash
cd "$WORK/gate" || exit 1
git clone -q --no-checkout https://github.com/opensoft/openxFactory.git "$WORK/oxf"
git -C "$WORK/oxf" diff --quiet c8dde1315e3f4cfdbcc75872306493cb88c9cd2d origin/main -- governance && echo "governance/ unchanged to openxFactory main $(git -C "$WORK/oxf" rev-parse origin/main)"
mkdir "$WORK/oxf-export" && git -C "$WORK/oxf" archive c8dde1315e3f4cfdbcc75872306493cb88c9cd2d governance | tar -x -C "$WORK/oxf-export"
for TREE in "$WORK/oxw-adapter" "$WORK/oxf-export"; do
  neutral "$TREE"; neutral "$TREE" --strict
done
grep -E '^(note  (corpus|repo scan)|validate-openxwallet:)' after.txt     # the export's summary lines, and nothing else of it
rm -rf "$WORK/oxf" "$WORK/oxf-export"
neutral "$WORK/oxw-adapter" > /dev/null; cat after.txt                     # tree (i) as both validators print it
```

```
governance/ unchanged to openxFactory main 564f565ad092401c1bbd4be8a6d006c7f12bbda5
EMPTY $WORK/oxw-adapter (exit=0)
EMPTY $WORK/oxw-adapter --strict (exit=0)
EMPTY $WORK/oxf-export (exit=0)
EMPTY $WORK/oxf-export --strict (exit=0)
note  corpus: 21 positive example(s), 45 negative confirmation(s) across 13/13 requirements
note  repo scan: 9 openxWallet artifact(s) validated, 5 document(s) skipped as another kind
validate-openxwallet: 0 error(s), 0 warning(s)
note  approval-scope vocabulary read from contracts/schemas/hermes-job-envelope.schema.yaml: ['authority_agents_may_approve', 'hermes_approval_required_before_apply', 'human_escalation_required_for']
note  wallet 'wal-agent-council-0011': 4 declared key(s) adjudicated (key-council-primary-0011, key-council-retired-0011, key-council-seat-a-0011, key-council-seat-b-0011)
note  corpus: 21 positive example(s), 45 negative confirmation(s) across 13/13 requirements
note  nested repositories pruned (not adjudicated): openWallet
note  no intake register at this tree; nothing to read
note  repo scan: 0 openxWallet artifact(s) validated, 21 document(s) skipped as another kind

validate-openxwallet: 0 error(s), 0 warning(s)
exit=0
```

Tree (i) prints those same nine lines plain and `--strict`, from both
validators.

The export is openxFactory's `governance/` at
`c8dde1315e3f4cfdbcc75872306493cb88c9cd2d`. It is taken with `git archive` into
a directory outside every clone and deleted once measured. It carries personal
data (an operator's email and the seats' keys), so it is never committed
anywhere, and this document quotes only the validators' summary lines. Its
`governance/` is byte-unchanged from that commit to openxFactory's `main` at
the run.

**The line the first commit expected, and what was measured.** This document's
first commit expected openXwallet's own tree to differ by one declared line,
`nested repositories pruned (not adjudicated): openWallet`. It does not differ.
Both validators print that line, because the carve-commit validator carries the
same sweep prune (`wallet-v1.1`) and finds the same nested `openWallet/`. The
line is new relative to the pre-split validator's run over the pre-split tree,
as D5 declares, but it is no difference between the two validators. The same
holds for the composed corpus note, 21 / 45 / 13 of 13: both validators print
it.

**(iii) Every fixture tree the suites build.** No suite keeps a fixture tree on
disk. Each one builds its trees under pytest's `tmp_path` and hands them to
`scripts/validate-openxwallet.py` as a subprocess. So a tree has to be caught at
the moment it is handed over.

A `sitecustomize.py` outside every clone does that. Python imports it at
start-up in every process that has its directory on `PYTHONPATH`. It acts only
in a process whose script is a `validate-openxwallet.py`, and there it copies
each path argument before the validator runs. It prints nothing, and the suite
sees the real validator's run.

The suites are the ones that drive the validator. That means each test file
under `tests/` that spells the literal `"validate-openxwallet.py"`, except the
neutrality gate's own suite, which drives toy validators. This is lane
`openXwallet-3`'s selection rule (task 5.4). It selects five kept files in
openXwallet and two moved files in the code leg:

```bash
mkdir -p "$WORK/capture-site"
cat > "$WORK/capture-site/sitecustomize.py" <<'PY'
# Part three (iii): the capture hook. Python imports it at start-up in every process
# that has this directory on PYTHONPATH. In a process whose script is a
# validate-openxwallet.py, it records the invocation and COPIES each path argument
# that exists, before the validator runs, so the tree a suite hands the validator
# outlives the test. A path inside PROOF_LIVE_ROOTS is recorded, not copied: it is
# compared in place. The hook prints nothing and changes nothing the suite sees.
import json, os, shutil, sys, uuid
def _capture(out):
    live = [os.path.realpath(p) for p in os.environ.get("PROOF_LIVE_ROOTS", "").split(os.pathsep) if p]
    rid = uuid.uuid4().hex[:12]
    rec = {"id": rid, "test": os.environ.get("PYTEST_CURRENT_TEST", ""), "script": sys.argv[0],
           "cwd": os.getcwd(), "args": sys.argv[1:], "trees": []}
    for i, a in enumerate(sys.argv[1:]):
        if a.startswith("-"):
            continue
        real = os.path.realpath(a)
        t = {"arg": i, "path": real, "exists": os.path.exists(real)}
        if t["exists"] and any(real == r or real.startswith(r + os.sep) for r in live):
            t["live"] = True
        elif t["exists"]:
            dest = os.path.join(out, rid, str(i), os.path.basename(real))
            if os.path.isdir(real):
                shutil.copytree(real, dest, symlinks=True)
            else:
                os.makedirs(os.path.dirname(dest)); shutil.copy2(real, dest)
            t["snapshot"] = dest
        rec["trees"].append(t)
    with open(os.path.join(out, "records.jsonl"), "a", encoding="utf-8") as fh:
        fh.write(json.dumps(rec) + "\n")
_out = os.environ.get("PROOF_CAPTURE")
if _out and sys.argv and os.path.basename(sys.argv[0]) == "validate-openxwallet.py":
    try:
        _capture(_out)
    except Exception as exc:  # recorded, never raised into the suite
        with open(os.path.join(_out, "errors.txt"), "a", encoding="utf-8") as fh:
            fh.write(f"{sys.argv!r}: {exc!r}\n")
PY
sha256sum "$WORK/capture-site/sitecustomize.py" | cut -c1-64
cd "$WORK" || exit 1
for S in oxw-adapter oxw-adapter/openWallet/code; do
  N=$(basename "$S"); mkdir -p "$WORK/captured/$N"
  ( cd "$WORK/$S" || exit 1
    FILES=$(grep -lE "[\"']validate-openxwallet\.py[\"']" tests/*/*.py | grep -v '^tests/neutrality_gate/')
    PYTHONPATH="$WORK/capture-site" PROOF_CAPTURE="$WORK/captured/$N" PROOF_LIVE_ROOTS="$WORK/oxw-adapter" \
      PYTHONDONTWRITEBYTECODE=1 python3 -m pytest $FILES -q -p no:cacheprovider --basetemp="$WORK/pytest-$N" | tail -n 1
    echo "$N: $(echo $FILES | wc -w) file(s), $(wc -l < "$WORK/captured/$N/records.jsonl") validator invocation(s) recorded" )
done
git -C oxw-adapter status --porcelain --ignored; git -C oxw-adapter/openWallet/code status --porcelain --ignored   # both print nothing
python3 - "$WORK" <<'PY'
# what the suites handed the validator: a tree they built (copied), the live checkout, no path, or a path that does not exist
import collections, json, pathlib, sys
work = sys.argv[1]
for d in ("oxw-adapter", "code"):
    kinds, live = collections.Counter(), set()
    for line in open(pathlib.Path(work, "captured", d, "records.jsonl"), encoding="utf-8"):
        r = json.loads(line)
        if not r["trees"]:
            kinds["--help" if "--help" in r["args"] else "no path (self-test only)"] += 1
        for t in r["trees"]:
            kinds["built tree, copied" if "snapshot" in t else "the live checkout" if t.get("live") else "no such path"] += 1
            if t.get("live"):
                live.add(t["path"].replace(work, "$WORK"))
    print(d, dict(sorted(kinds.items())), sorted(live))
PY
```

```
ea9e3e3f853f95c5b7ac151b45fc87eb713eb0a414d6f08af396def5513605e9
91 passed in 421.89s (0:07:01)
oxw-adapter: 5 file(s), 96 validator invocation(s) recorded
33 passed, 1 skipped in 30.15s
code: 2 file(s), 31 validator invocation(s) recorded
oxw-adapter {'--help': 1, 'built tree, copied': 82, 'no path (self-test only)': 5, 'no such path': 1, 'the live checkout': 7} ['$WORK/oxw-adapter']
code {'--help': 1, 'built tree, copied': 28, 'the live checkout': 2} ['$WORK/oxw-adapter/openWallet/code']
```

Both suite runs pass under the hook. Lane `openXwallet-3`'s gate, running the
same code-leg suite with `-rs`, names its one skip: the previous-validator
comparison, which part three's first half explains. The hook wrote nothing
into either checkout, and neither did the suites.

**Each built tree, both validators, both modes.** The replay runs `neutral()`
over every copy, in parallel, one scratch directory per tree:

```bash
cd "$WORK" || exit 1
python3 - "$WORK/captured" > trees.tsv <<'PY'
# one line per built tree, in invocation order: n, leg, suite, test, the copy
import json, pathlib, sys
n = 0
for leg, d in (("openXwallet", "oxw-adapter"), ("code leg", "code")):
    for line in open(pathlib.Path(sys.argv[1], d, "records.jsonl"), encoding="utf-8"):
        r = json.loads(line)
        for t in r["trees"]:
            if "snapshot" in t:
                n += 1
                f, test = r["test"].rsplit(" ", 1)[0].split("::", 1)
                print("\t".join((str(n), leg, f.split("/")[1], test, t["snapshot"])))
PY
replay() {   # one trees.tsv line -> one table row
  IFS=$'\t' read -r n leg suite test tree <<< "$1"
  cd "$(mktemp -d -p "$WORK/replay")" || exit 1
  x() { echo "$(tail -n 1 before.txt | cut -d= -f2)/$(tail -n 1 after.txt | cut -d= -f2)"; }
  p=$(neutral "$tree" | head -n 1 | cut -d' ' -f1); px=$(x)
  s=$(neutral "$tree" --strict | head -n 1 | cut -d' ' -f1); sx=$(x)
  printf '| %s | %s | `%s` | `%s` | %s | %s | %s | %s |\n' "$n" "$leg" "$suite" "$test" "$p" "$px" "$s" "$sx"
}
export WORK; export -f neutral replay
mkdir -p replay && tr '\n' '\0' < trees.tsv | xargs -0 -P 8 -I{} bash -c 'replay "$1"' _ {} | sort -t'|' -k2,2n > rows.md
wc -l < rows.md; cut -d'|' -f6-9 rows.md | sort | uniq -c
```

```
110
     52  EMPTY | 0/0 | EMPTY | 0/0 
     58  EMPTY | 1/1 | EMPTY | 1/1 
```

**110 of 110 built trees: `diff` EMPTY, plain and `--strict`, and the same exit
code each time.** That is 82 trees from the kept suites and 28 from the moved
ones. 52 of them are clean (exit 0 from both validators in both modes). The
other 58 are trees a suite builds to be refused, and both validators refuse
them with exit 1 and byte-identical findings. The table is `rows.md` as printed.
The exit columns read carve-commit validator / composed adapter.

<details>
<summary>(iii): the 110 built trees, per tree</summary>

| # | leg | suite | test | plain | exit | `--strict` | exit |
| ---: | --- | --- | --- | --- | --- | --- | --- |
| 1 | openXwallet | `nested_repo_prune` | `test_the_composed_entrypoint_prunes_both_nested_shapes` | EMPTY | 0/0 | EMPTY | 0/0 |
| 2 | openXwallet | `nested_repo_prune` | `test_a_successful_register_read_says_so_exactly_once` | EMPTY | 0/0 | EMPTY | 0/0 |
| 3 | openXwallet | `nested_repo_prune` | `test_the_register_note_leaves_a_strict_run_green` | EMPTY | 0/0 | EMPTY | 0/0 |
| 4 | openXwallet | `nested_repo_prune` | `test_the_register_note_leaves_a_strict_run_green` | EMPTY | 0/0 | EMPTY | 0/0 |
| 5 | openXwallet | `nested_repo_prune` | `test_the_register_path_is_relative_to_the_scan_root` | EMPTY | 0/0 | EMPTY | 0/0 |
| 6 | openXwallet | `nested_repo_prune` | `test_no_register_keeps_the_ratified_absent_behaviour` | EMPTY | 0/0 | EMPTY | 0/0 |
| 7 | openXwallet | `nested_repo_prune` | `test_a_register_inside_a_nested_repo_is_not_read` | EMPTY | 0/0 | EMPTY | 0/0 |
| 8 | openXwallet | `nested_repo_prune` | `test_the_composed_adapter_adjudicates_as_the_pre_split_validator_did` | EMPTY | 1/1 | EMPTY | 1/1 |
| 9 | openXwallet | `nested_repo_prune` | `test_the_composed_adapter_adjudicates_as_the_pre_split_validator_did` | EMPTY | 1/1 | EMPTY | 1/1 |
| 10 | openXwallet | `openwallet_pin` | `test_an_uninitialized_root_refuses_with_its_own_remediation[validator]` | EMPTY | 0/0 | EMPTY | 0/0 |
| 11 | openXwallet | `openwallet_pin` | `test_an_uninitialized_leg_refuses_with_its_own_remediation[validator]` | EMPTY | 0/0 | EMPTY | 0/0 |
| 12 | openXwallet | `openwallet_pin` | `test_a_core_that_does_not_load_refuses[validator]` | EMPTY | 0/0 | EMPTY | 0/0 |
| 13 | openXwallet | `openwallet_pin` | `test_a_core_file_that_is_absent_refuses[validator]` | EMPTY | 0/0 | EMPTY | 0/0 |
| 14 | openXwallet | `openwallet_pin` | `test_a_core_without_the_composition_contract_refuses` | EMPTY | 0/0 | EMPTY | 0/0 |
| 15 | openXwallet | `openwallet_pin` | `test_a_requirement_id_the_core_already_declares_refuses` | EMPTY | 0/0 | EMPTY | 0/0 |
| 16 | openXwallet | `openwallet_pin` | `test_an_absent_envelope_is_the_hard_exit_it_always_was` | EMPTY | 0/0 | EMPTY | 0/0 |
| 17 | openXwallet | `per_seat_register_entries` | `test_the_four_real_seat_keys_validate` | EMPTY | 0/0 | EMPTY | 0/0 |
| 18 | openXwallet | `per_seat_register_entries` | `test_the_note_counts_adjudicated_keys_not_parsed_ones` | EMPTY | 1/1 | EMPTY | 1/1 |
| 19 | openXwallet | `per_seat_register_entries` | `test_an_absent_seat_surface_is_accepted_and_visible` | EMPTY | 0/0 | EMPTY | 0/0 |
| 20 | openXwallet | `per_seat_register_entries` | `test_a_strict_run_stays_green` | EMPTY | 0/0 | EMPTY | 0/0 |
| 21 | openXwallet | `per_seat_register_entries` | `test_a_strict_run_stays_green` | EMPTY | 0/0 | EMPTY | 0/0 |
| 22 | openXwallet | `per_seat_register_entries` | `test_an_unread_top_level_declaration_is_refused` | EMPTY | 1/1 | EMPTY | 1/1 |
| 23 | openXwallet | `per_seat_register_entries` | `test_the_staleness_bound_is_required` | EMPTY | 1/1 | EMPTY | 1/1 |
| 24 | openXwallet | `per_seat_register_entries` | `test_a_malformed_or_zero_bound_is_refused[P1Y]` | EMPTY | 1/1 | EMPTY | 1/1 |
| 25 | openXwallet | `per_seat_register_entries` | `test_a_malformed_or_zero_bound_is_refused[P1M]` | EMPTY | 1/1 | EMPTY | 1/1 |
| 26 | openXwallet | `per_seat_register_entries` | `test_a_malformed_or_zero_bound_is_refused[7 days]` | EMPTY | 1/1 | EMPTY | 1/1 |
| 27 | openXwallet | `per_seat_register_entries` | `test_a_malformed_or_zero_bound_is_refused[P]` | EMPTY | 1/1 | EMPTY | 1/1 |
| 28 | openXwallet | `per_seat_register_entries` | `test_a_malformed_or_zero_bound_is_refused[PT]` | EMPTY | 1/1 | EMPTY | 1/1 |
| 29 | openXwallet | `per_seat_register_entries` | `test_a_malformed_or_zero_bound_is_refused[P0D]` | EMPTY | 1/1 | EMPTY | 1/1 |
| 30 | openXwallet | `per_seat_register_entries` | `test_a_malformed_or_zero_bound_is_refused[PT0S]` | EMPTY | 1/1 | EMPTY | 1/1 |
| 31 | openXwallet | `per_seat_register_entries` | `test_a_malformed_or_zero_bound_is_refused[]` | EMPTY | 1/1 | EMPTY | 1/1 |
| 32 | openXwallet | `per_seat_register_entries` | `test_a_malformed_or_zero_bound_is_refused[P1DT]` | EMPTY | 1/1 | EMPTY | 1/1 |
| 33 | openXwallet | `per_seat_register_entries` | `test_a_well_formed_bound_is_accepted[P7D]` | EMPTY | 0/0 | EMPTY | 0/0 |
| 34 | openXwallet | `per_seat_register_entries` | `test_a_well_formed_bound_is_accepted[P1D]` | EMPTY | 0/0 | EMPTY | 0/0 |
| 35 | openXwallet | `per_seat_register_entries` | `test_a_well_formed_bound_is_accepted[P1W]` | EMPTY | 0/0 | EMPTY | 0/0 |
| 36 | openXwallet | `per_seat_register_entries` | `test_a_well_formed_bound_is_accepted[PT12H]` | EMPTY | 0/0 | EMPTY | 0/0 |
| 37 | openXwallet | `per_seat_register_entries` | `test_a_well_formed_bound_is_accepted[P1DT6H30M]` | EMPTY | 0/0 | EMPTY | 0/0 |
| 38 | openXwallet | `per_seat_register_entries` | `test_a_well_formed_bound_is_accepted[PT30S]` | EMPTY | 0/0 | EMPTY | 0/0 |
| 39 | openXwallet | `per_seat_register_entries` | `test_a_malformed_seat_surface_is_refused[shape0]` | EMPTY | 1/1 | EMPTY | 1/1 |
| 40 | openXwallet | `per_seat_register_entries` | `test_a_malformed_seat_surface_is_refused[P7D]` | EMPTY | 1/1 | EMPTY | 1/1 |
| 41 | openXwallet | `per_seat_register_entries` | `test_a_malformed_seat_surface_is_refused[shape2]` | EMPTY | 1/1 | EMPTY | 1/1 |
| 42 | openXwallet | `per_seat_register_entries` | `test_a_malformed_seat_surface_is_refused[4]` | EMPTY | 1/1 | EMPTY | 1/1 |
| 43 | openXwallet | `per_seat_register_entries` | `test_an_unknown_field_on_an_entry_is_refused` | EMPTY | 1/1 | EMPTY | 1/1 |
| 44 | openXwallet | `per_seat_register_entries` | `test_a_missing_field_on_an_entry_is_refused[authorizing_row]` | EMPTY | 1/1 | EMPTY | 1/1 |
| 45 | openXwallet | `per_seat_register_entries` | `test_a_missing_field_on_an_entry_is_refused[council_id]` | EMPTY | 1/1 | EMPTY | 1/1 |
| 46 | openXwallet | `per_seat_register_entries` | `test_a_missing_field_on_an_entry_is_refused[council_ref]` | EMPTY | 1/1 | EMPTY | 1/1 |
| 47 | openXwallet | `per_seat_register_entries` | `test_a_missing_field_on_an_entry_is_refused[key_fingerprint]` | EMPTY | 1/1 | EMPTY | 1/1 |
| 48 | openXwallet | `per_seat_register_entries` | `test_a_missing_field_on_an_entry_is_refused[key_id]` | EMPTY | 1/1 | EMPTY | 1/1 |
| 49 | openXwallet | `per_seat_register_entries` | `test_a_missing_field_on_an_entry_is_refused[public_key]` | EMPTY | 1/1 | EMPTY | 1/1 |
| 50 | openXwallet | `per_seat_register_entries` | `test_a_missing_field_on_an_entry_is_refused[seat_id]` | EMPTY | 1/1 | EMPTY | 1/1 |
| 51 | openXwallet | `per_seat_register_entries` | `test_a_private_seed_pasted_where_a_public_half_belongs_is_refused` | EMPTY | 1/1 | EMPTY | 1/1 |
| 52 | openXwallet | `per_seat_register_entries` | `test_a_non_canonical_public_key_is_refused` | EMPTY | 1/1 | EMPTY | 1/1 |
| 53 | openXwallet | `per_seat_register_entries` | `test_a_malformed_fingerprint_is_refused` | EMPTY | 1/1 | EMPTY | 1/1 |
| 54 | openXwallet | `per_seat_register_entries` | `test_a_fingerprint_that_does_not_recompute_is_refused` | EMPTY | 1/1 | EMPTY | 1/1 |
| 55 | openXwallet | `per_seat_register_entries` | `test_a_duplicate_entry_is_refused[seat_id]` | EMPTY | 1/1 | EMPTY | 1/1 |
| 56 | openXwallet | `per_seat_register_entries` | `test_a_duplicate_entry_is_refused[key_id]` | EMPTY | 1/1 | EMPTY | 1/1 |
| 57 | openXwallet | `per_seat_register_entries` | `test_a_duplicate_entry_is_refused[key_fingerprint]` | EMPTY | 1/1 | EMPTY | 1/1 |
| 58 | openXwallet | `per_seat_register_entries` | `test_an_entry_naming_no_row_is_refused` | EMPTY | 1/1 | EMPTY | 1/1 |
| 59 | openXwallet | `per_seat_register_entries` | `test_an_entry_on_an_expired_row_is_refused` | EMPTY | 1/1 | EMPTY | 1/1 |
| 60 | openXwallet | `per_seat_register_entries` | `test_an_entry_naming_an_uncommissioned_body_is_refused` | EMPTY | 1/1 | EMPTY | 1/1 |
| 61 | openXwallet | `per_seat_register_entries` | `test_two_spellings_naming_different_bodies_are_refused` | EMPTY | 1/1 | EMPTY | 1/1 |
| 62 | openXwallet | `per_seat_register_entries` | `test_a_second_authority_row_is_not_refused_on_count` | EMPTY | 0/0 | EMPTY | 0/0 |
| 63 | openXwallet | `per_seat_register_entries` | `test_a_second_authority_row_is_not_refused_on_count` | EMPTY | 1/1 | EMPTY | 1/1 |
| 64 | openXwallet | `per_seat_register_entries` | `test_the_consumer_gate_conjunction_still_holds` | EMPTY | 0/0 | EMPTY | 0/0 |
| 65 | openXwallet | `register_reissuance` | `test_a_revoked_predecessor_beside_its_successor_is_clean` | EMPTY | 0/0 | EMPTY | 0/0 |
| 66 | openXwallet | `register_reissuance` | `test_a_strict_run_of_the_re_issuance_stays_green` | EMPTY | 0/0 | EMPTY | 0/0 |
| 67 | openXwallet | `register_reissuance` | `test_an_active_review_grant_with_no_row_still_refuses` | EMPTY | 1/1 | EMPTY | 1/1 |
| 68 | openXwallet | `register_reissuance` | `test_a_row_pointing_at_the_revoked_grant_is_still_refused` | EMPTY | 1/1 | EMPTY | 1/1 |
| 69 | openXwallet | `register_reissuance` | `test_an_absent_register_with_only_a_revoked_grant_is_clean` | EMPTY | 0/0 | EMPTY | 0/0 |
| 70 | openXwallet | `register_reissuance` | `test_an_absent_register_with_an_active_review_grant_still_refuses` | EMPTY | 1/1 | EMPTY | 1/1 |
| 71 | openXwallet | `widen_register_reader` | `test_the_live_one_row_register_stays_clean` | EMPTY | 0/0 | EMPTY | 0/0 |
| 72 | openXwallet | `widen_register_reader` | `test_the_live_one_row_register_stays_clean` | EMPTY | 0/0 | EMPTY | 0/0 |
| 73 | openXwallet | `widen_register_reader` | `test_the_retired_row_count_refusal_is_emitted_by_nothing` | EMPTY | 0/0 | EMPTY | 0/0 |
| 74 | openXwallet | `widen_register_reader` | `test_the_retired_row_count_refusal_is_emitted_by_nothing` | EMPTY | 0/0 | EMPTY | 0/0 |
| 75 | openXwallet | `widen_register_reader` | `test_a_second_commissioned_body_resolving_end_to_end_is_admitted` | EMPTY | 0/0 | EMPTY | 0/0 |
| 76 | openXwallet | `widen_register_reader` | `test_a_per_council_duplicate_still_refuses_and_names_the_council` | EMPTY | 1/1 | EMPTY | 1/1 |
| 77 | openXwallet | `widen_register_reader` | `test_two_councils_may_seat_the_same_role_name` | EMPTY | 0/0 | EMPTY | 0/0 |
| 78 | openXwallet | `widen_register_reader` | `test_one_council_naming_a_seat_twice_is_refused` | EMPTY | 1/1 | EMPTY | 1/1 |
| 79 | openXwallet | `widen_register_reader` | `test_key_id_and_fingerprint_stay_globally_unique[key_id]` | EMPTY | 1/1 | EMPTY | 1/1 |
| 80 | openXwallet | `widen_register_reader` | `test_key_id_and_fingerprint_stay_globally_unique[key_fingerprint]` | EMPTY | 1/1 | EMPTY | 1/1 |
| 81 | openXwallet | `widen_register_reader` | `test_a_seat_entry_attached_to_another_bodys_row_is_refused` | EMPTY | 1/1 | EMPTY | 1/1 |
| 82 | openXwallet | `widen_register_reader` | `test_a_second_row_that_does_not_resolve_is_refused` | EMPTY | 1/1 | EMPTY | 1/1 |
| 83 | code leg | `multi_key_wallets` | `test_a_single_key_wallet_is_unchanged` | EMPTY | 0/0 | EMPTY | 0/0 |
| 84 | code leg | `multi_key_wallets` | `test_a_multi_key_wallet_validates_and_is_noted` | EMPTY | 0/0 | EMPTY | 0/0 |
| 85 | code leg | `multi_key_wallets` | `test_an_additional_key_may_present_the_grant` | EMPTY | 0/0 | EMPTY | 0/0 |
| 86 | code leg | `multi_key_wallets` | `test_a_weaker_key_is_admitted` | EMPTY | 0/0 | EMPTY | 0/0 |
| 87 | code leg | `multi_key_wallets` | `test_a_truthful_refusal_over_the_key_ceiling_is_valid` | EMPTY | 0/0 | EMPTY | 0/0 |
| 88 | code leg | `multi_key_wallets` | `test_retiring_one_key_leaves_the_others_working` | EMPTY | 0/0 | EMPTY | 0/0 |
| 89 | code leg | `multi_key_wallets` | `test_an_act_already_attributed_to_a_retired_key_stays_readable` | EMPTY | 0/0 | EMPTY | 0/0 |
| 90 | code leg | `multi_key_wallets` | `test_a_presenting_key_outside_the_declared_set_is_refused` | EMPTY | 1/1 | EMPTY | 1/1 |
| 91 | code leg | `multi_key_wallets` | `test_a_duplicated_key_identifier_is_refused` | EMPTY | 1/1 | EMPTY | 1/1 |
| 92 | code leg | `multi_key_wallets` | `test_a_duplicated_key_identifier_is_refused` | EMPTY | 1/1 | EMPTY | 1/1 |
| 93 | code leg | `multi_key_wallets` | `test_a_key_may_not_outrank_its_wallet` | EMPTY | 1/1 | EMPTY | 1/1 |
| 94 | code leg | `multi_key_wallets` | `test_a_declared_key_custody_outside_the_closed_set_is_refused` | EMPTY | 1/1 | EMPTY | 1/1 |
| 95 | code leg | `multi_key_wallets` | `test_a_fingerprint_that_does_not_recompute_is_refused` | EMPTY | 1/1 | EMPTY | 1/1 |
| 96 | code leg | `multi_key_wallets` | `test_a_public_half_that_does_not_decode_is_refused` | EMPTY | 1/1 | EMPTY | 1/1 |
| 97 | code leg | `multi_key_wallets` | `test_the_custody_in_force_is_the_presenting_keys` | EMPTY | 1/1 | EMPTY | 1/1 |
| 98 | code leg | `multi_key_wallets` | `test_the_single_key_basis_still_fires` | EMPTY | 1/1 | EMPTY | 1/1 |
| 99 | code leg | `multi_key_wallets` | `test_a_grant_above_the_presenting_keys_ceiling_is_refused` | EMPTY | 1/1 | EMPTY | 1/1 |
| 100 | code leg | `multi_key_wallets` | `test_an_exercise_under_a_retired_key_is_refused` | EMPTY | 1/1 | EMPTY | 1/1 |
| 101 | code leg | `multi_key_wallets` | `test_an_unverified_signature_does_not_establish_a_key` | EMPTY | 0/0 | EMPTY | 0/0 |
| 102 | code leg | `nested_repo_prune` | `test_nested_repo_with_a_dot_git_FILE_is_not_adjudicated` | EMPTY | 0/0 | EMPTY | 0/0 |
| 103 | code leg | `nested_repo_prune` | `test_nested_repo_with_a_dot_git_DIRECTORY_is_not_adjudicated` | EMPTY | 0/0 | EMPTY | 0/0 |
| 104 | code leg | `nested_repo_prune` | `test_the_control_same_record_outside_any_nested_repo_IS_adjudicated` | EMPTY | 0/0 | EMPTY | 0/0 |
| 105 | code leg | `nested_repo_prune` | `test_one_tree_both_cases_at_once` | EMPTY | 0/0 | EMPTY | 0/0 |
| 106 | code leg | `nested_repo_prune` | `test_the_scan_root_is_never_pruned_by_its_own_dot_git` | EMPTY | 0/0 | EMPTY | 0/0 |
| 107 | code leg | `nested_repo_prune` | `test_a_nested_repo_inside_a_pruned_one_is_not_reported_twice` | EMPTY | 0/0 | EMPTY | 0/0 |
| 108 | code leg | `nested_repo_prune` | `test_no_prune_note_when_there_is_nothing_to_prune` | EMPTY | 0/0 | EMPTY | 0/0 |
| 109 | code leg | `nested_repo_prune` | `test_skip_dir_names_still_behaves_as_it_did` | EMPTY | 0/0 | EMPTY | 0/0 |
| 110 | code leg | `nested_repo_prune` | `test_the_packaged_corpus_exclusion_still_keys_on_path_parts` | EMPTY | 0/0 | EMPTY | 0/0 |

</details>

**What else the suites hand the validator.** Seventeen invocations hand it no
built tree:

```bash
cd "$WORK/gate" || exit 1
neutral; neutral --strict                         # no path: the self-test alone
neutral --help | head -n 2                        # not a tree
neutral "$WORK/no-such-tree"                      # a path that does not exist
for TREE in "$WORK/oxw-adapter/openWallet/code" "$WORK/oxw-carve"; do neutral "$TREE"; neutral "$TREE" --strict; done
mkdir "$WORK/code-copy" && git -C "$WORK/oxw-adapter/openWallet/code" archive HEAD | tar -x -C "$WORK/code-copy"
neutral "$WORK/code-copy"; neutral "$WORK/code-copy" --strict
```

```
EMPTY  (exit=0)
EMPTY --strict (exit=0)
DIFFERS --help
75,79c75,79
EMPTY $WORK/no-such-tree (exit=2)
DIFFERS $WORK/oxw-adapter/openWallet/code
5c5
< note  repo scan: 1 openxWallet artifact(s) validated, 9 document(s) skipped as another kind
---
> note  repo scan: 0 openxWallet artifact(s) validated, 9 document(s) skipped as another kind
DIFFERS $WORK/oxw-adapter/openWallet/code --strict
5c5
< note  repo scan: 1 openxWallet artifact(s) validated, 9 document(s) skipped as another kind
---
> note  repo scan: 0 openxWallet artifact(s) validated, 9 document(s) skipped as another kind
DIFFERS $WORK/oxw-carve
5c5
< note  repo scan: 0 openxWallet artifact(s) validated, 32 document(s) skipped as another kind
---
> note  repo scan: 1 openxWallet artifact(s) validated, 32 document(s) skipped as another kind
DIFFERS $WORK/oxw-carve --strict
5c5
< note  repo scan: 0 openxWallet artifact(s) validated, 32 document(s) skipped as another kind
---
> note  repo scan: 1 openxWallet artifact(s) validated, 32 document(s) skipped as another kind
EMPTY $WORK/code-copy (exit=0)
EMPTY $WORK/code-copy --strict (exit=0)
```

| Invocations | What they hand the validator | Measured |
| ---: | --- | --- |
| 5 (kept suites) | no path: the self-test alone | EMPTY, plain and `--strict`, exit 0 |
| 7 (kept suites) | openXwallet's own checkout, in place | tree (i), above: EMPTY |
| 1 (kept suites) | `some/tree`, a path that does not exist, inside a synthesized root | not a tree. The same kind of path given to both validators: EMPTY, exit 2 |
| 2 (one in each) | `--help` | not a tree. 70 lines of the module docstring differ, because D3 splits the docstring between core and adapter. Outside the verdict, as lane `openXwallet-3`'s gate keeps it |
| 2 (moved suites) | the code leg's own checkout, in place | **differs by one count line**, in both modes, with 0 errors and exit 0 on both sides. This tree is none of D5's three kinds. See Finding 4 |

The last block's other trees are Finding 4's controls. Scanned in place, the
carve-commit tree differs the other way round. The code leg's own bytes,
exported elsewhere, are EMPTY.

**Lane `openXwallet-3`'s own gate agrees.** That is `scripts/neutrality-gate.py`
at `a02c6c74`, run with `--openxfactory-export` over the same export from a
second fresh clone. It printed `neutrality-gate: IDENTICAL: 4 target run(s)
over 2 tree(s) and 117 suite invocation(s) over 7 suite(s); every stdout
byte-identical, every exit code equal` and exited 0. At `815b86ce`, run the
same way, it printed `neutrality-gate: IDENTICAL: 2 tree(s) × 2 modes = 4
target run(s), and 122 suite invocation(s) × 2 modes = 244 suite record(s) over
7 suite(s); every stdout byte-identical, every exit code equal` and exited 0.
It judges stdout and the exit code, and it compares each suite invocation at
the moment that invocation is made. This document's commands, above, are the
authority. Finding 4 records what that gate's suite mirrors do not reach.

**Part three, second half: RUN-GREEN** over D5's three kinds of tree, at
opensoft/openXwallet `a02c6c74`:
- (i) openXwallet's own tree, and (ii) the openxFactory `governance/` export:
  EMPTY, plain and `--strict`, exit 0;
- (iii) 110 of 110 trees the kept and moved suites build: EMPTY in both modes,
  with equal exit codes;
- the self-test alone: EMPTY.

Re-confirmed at `815b86ce` on 2026-10-09: the same, with 111 of 111 built
trees, 53 at 0/0 and 58 at 1/1. They are the 110 above, in the same order,
plus `openwallet_pin`'s
`test_a_core_that_exits_zero_while_loading_refuses[validator]` inserted as #13,
so the table's #13 to #110 are #14 to #111 there.

`neutral()` itself was observed refusing a one-byte change (part four, 4.9).

The adapter pins this root at `1c68717f`, and its `code` gitlink is `72313daa`,
the code-leg commit every part above measured. At `815b86ce` it pins
`b0af7c2c`; the code leg is still `72313daa`. The gate reads only
`openWallet/code`, so the spec re-pins of part two (b) move no byte it reads.
Had the code pin moved before the tag, this half would have run again against
the new pin, and so would parts zero to five. It did not: the tagged commit
`b0af7c2c` pins code at `72313daa`.

---

## Part four — every verifier observed REFUSING, before it is trusted

**Re-run, not cited.** A refusal observed in the runbook's rehearsal proves that
the helper refused then. It does not prove that this proof's run used a helper
that refuses. So every verifier that parts zero to five rely on was fed a
mutated input in this run. Every mutation was made in a scratch clone or on a
throwaway `neg/*` branch under `$WORK`, never in a leg or in this root. Each
scratch clone was discarded afterwards.

| # | Verifier | Mutated input | Decisive line | Exit |
| --- | --- | --- | --- | ---: |
| 4.1 | `bin/control.py` (helper 4) | one byte appended to `openxwallet-grant.schema.yaml` in a commit on the carve commit | `MISMATCH openxwallet-grant b79d11b8…`, `control: 7/8 owned digest(s) recomputed equal` | 1 |
| 4.2 | openXwallet `validate-carve-manifest.py` | one hex digit of the grant row's `sha256:` | `FAIL …: carve-digest-mismatch — contracts/openxwallet/openxwallet-grant.schema.yaml: DIGEST DRIFT` | 2 |
| 4.2 | the same | the grant row deleted | `carve-file-undeclared — the carve commit 90111df262d6 tracks 1 path(s) that NO row declares` | 2 |
| 4.2 | the same | the grant row duplicated | `carve-file-duplicated — … appears in rows[126] AND rows[127]` | 2 |
| 4.2 | the same | the grant row's `destination_path` renamed | `carve-path-remapped — rows[126] … arrives at contracts/grant.schema.yaml` | 2 |
| 4.2 | `proof-bin/mapping.py` | the three manifests above, without the digest flip | `IN-NO-ROW`, `DUPLICATE`, `RENAMED`, each with `mapping: REFUSED` | 1 |
| 4.2 | `bin/carve-paths.py` (helper 1) | the renamed manifest | `AssertionError: contracts/openxwallet/openxwallet-grant.schema.yaml` | 1 |
| 4.3 | `bin/carve-layer.py` (helper 2) | a carve layer with one byte appended to the grant schema | `blob/mode mismatch 1`, `MISMATCH contracts/openxwallet/openxwallet-grant.schema.yaml` | 1 |
| 4.3 | the same | a carve layer with a stray file | `extra 1`, `EXTRA stray.txt` | 1 |
| 4.3 | the same | a carve layer missing one negative | `missing 1`, `MISSING contracts/openxwallet/examples/negative/custody-registry-collapsed-ceilings.yaml` | 1 |
| 4.3 | the same | a carve layer with the syntax gate made executable | `MISMATCH scripts/wallet-yaml-syntax-gate.py` | 1 |
| 4.3 | `proof-bin/per-path.py` | each of the four layers above | `identical git blob and mode: 79/80` (byte, missing, mode); `sorted listing … equals the 80 row(s): False` (extra, missing) | 1 |
| 4.4 | `bin/declared-edits.py` (helper 3) | on B: a trailing space on validator line 1, which no hunk declares | `REFUSE undeclared line(s) in scripts/validate-openxwallet.py: [1]` | 2 |
| 4.4 | `bin/declared-lines-exact.py` (helper 5) | the same | `REFUSE scripts/validate-openxwallet.py: … undeclared line(s) preserved in order: False` | 2 |
| 4.4 | `proof-bin/attribute.py` | the same | `removed or replaced line(s) in no declared edit: 1` | 1 |
| 4.4 | helper 3 | on B: a stray file | `REFUSE added, not declared: stray.txt` | 2 |
| 4.4 | helpers 3 and 5 | on B: one byte appended to a `moved_verbatim` row | `REFUSE verbatim row changed: contracts/openxwallet/openxwallet-grant.schema.yaml` (both) | 2 |
| 4.4 | helper 3 | on B: the leg's own `README.md` changed | `REFUSE changed outside the carve, not declared: README.md` | 2 |
| 4.4 | helpers 3 and 5 | on B: a carved path deleted | `REFUSE carved path deleted: scripts/wallet-yaml-syntax-gate.py` (helper 3); `REFUSE verbatim row changed: …` (helper 5) | 2 |
| 4.4 | helper 3 | on B: the validator's executable bit dropped (`100755` → `100644`) | `REFUSE mode changed: scripts/validate-openxwallet.py` | 2 |
| 4.4 | helper 3 | B itself, without `--added` | `REFUSE added, not declared: LICENSE`, `REFUSE added, not declared: contracts/openxwallet/examples/approval-vocabulary.binding.yaml` | 2 |
| 4.5 | `scripts/validate-pins.py` (`make validate`) | **the `code` gitlink moved ALONE**, to B | `FINDING pin-gitlink-mismatch: code: gitlink 75b990dc7ea99823626c18816b37d971f46e341b != contracts/code-pin.yaml commit 72313daab1f229c049cb90998931564c1904dbbc` | 1 (`make`: 2) |
| 4.5 | the same | `contracts/code-pin.yaml` `commit:` moved ALONE | `FINDING pin-gitlink-mismatch: code: gitlink 72313daab1f229c049cb90998931564c1904dbbc != contracts/code-pin.yaml commit 75b990dc7ea99823626c18816b37d971f46e341b` | 1 |
| 4.5 | the same | the `spec` gitlink moved ALONE, to B | `FINDING pin-gitlink-mismatch: spec: gitlink 5ea9539428eae850ba71e6f0ba8a38db061e809a != contracts/spec-pin.yaml commit 15c15bbd451a803f0acdb24e5234836db829a2d3` | 1 |
| 4.5 | the same | one digit of the code pin's `tree_sha256` | `FINDING pin-digest-mismatch: contracts/code-pin.yaml: digests.tree_sha256 0e05d60d…` | 1 |
| 4.5 | the same | a digest-pinned shape copy (`.gitignore`) edited | `FINDING shape-copy-drift: .gitignore: sha256 b8287f42…` | 1 |
| 4.5 | `make validate` (naming) | the code leg's repository misnamed in `project.yaml` | `FINDING naming-unclassified: openwallet-code-leg` | `make`: 2 |
| 4.6 | `proof-bin/three-way-full.py` | one digit of this root's manifest `openxwallet-grant` `sha256:` | `DISAGREE openxwallet-grant: …`, `three-way: 7/8 agree …` | 1 |
| 4.6 | the runbook's 3c three-way check, verbatim | the same | `three-way: 7/8 root-manifest digest(s) equal the code leg's bytes; consumed rows left: 0` | **0**, see "Findings" |
| 4.6 | helpers 3 and 5, at the root | the same | `REFUSE undeclared line(s) in contracts/manifest.yaml: [136]`; `REFUSE contracts/manifest.yaml: 67 declared line(s) in 10 run(s); 177 undeclared line(s) preserved in order: False` | 2 |
| 4.7 | the spec leg's gate, `scripts/validate-openspec-cli-pin.py` | the committed tarball with one byte appended | `REFUSE pin-integrity-mismatch: fission-ai-openspec-1.12.0-c844543999f673cdd72445879b86a4abea4c07ef.tgz: INTEGRITY DRIFT` | 2 |
| 4.8 | the code leg's `validate-openxwallet.py` | the corpus binding with `authority_agents_may_approve` removed | five `ERROR [authority-vocabulary-parallel]` on the five posture-carrying positives; `validate-openxwallet: 5 error(s), 0 warning(s)` | 1 |
| 4.8 | the same | part three (i): a live posture under no binding | three `ERROR [authority-vocabulary-parallel] … (legal terms: [])` | 1 |
| 4.8 | the code leg's `wallet-yaml-syntax-gate.py` | a tab-indented line appended to the grant schema | `ERROR contracts/openxwallet/openxwallet-grant.schema.yaml: while scanning for the next token` | 1 |
| 4.9 | part three's `neutral()` | in a scratch copy of the adapter, its pinned core with one byte appended to the `repo scan:` note; over tree (i) | `DIFFERS $WORK/oxw-adapter`, `6c6`, `> note  repo scan: 0 openxWallet artifact(s) validated, 21 document(s) skipped as another kind.` | prints `DIFFERS` |

The commit in 4.1 is a scratch commit, so the short id that `control.py` prints
for it varies from run to run. The 4.4 mutations sit on commit B
(`75b990dc`) and are judged against A's parents, exactly as part two (b) judges
B. The 4.5 and 4.6 mutations sit on `1c68717f` in a scratch clone of this root.
The 4.9 mutation sits in `$WORK/neg-adapter`, a scratch copy of the adapter
checkout, which is discarded afterwards. It ran with part three's second half.

**The commands**, in the order of the table:

```bash
# 4.1 the control
cd "$WORK" || exit 1
git clone -q oxw.git neg-oxw && git -C neg-oxw switch -q -c neg/control "$CARVE_COMMIT"
printf '#' >> neg-oxw/contracts/openxwallet/openxwallet-grant.schema.yaml
git -C neg-oxw commit -q -am 'NEGATIVE: one byte appended to the grant schema'
python3 bin/control.py "$(git -C neg-oxw rev-parse HEAD)" neg-oxw

# 4.2 the manifest: four mutated copies
mkdir -p negm && python3 - "$MANIFEST" <<'PY'
import sys
src = open(sys.argv[1], encoding="utf-8").read()
row = "  - source_path: contracts/openxwallet/openxwallet-grant.schema.yaml\n"
i = src.index(row); end = src.index("\n  - source_path:", i + 1) + 1
k = src.index('    sha256: "', i) + len('    sha256: "')
open("negm/digest.yaml", "w").write(src[:k] + ("0" if src[k] != "0" else "1") + src[k + 1:])
open("negm/row-deleted.yaml", "w").write(src[:i] + src[end:])
open("negm/row-twice.yaml", "w").write(src[:end] + src[i:end] + src[end:])
seg = src[i:end].replace("    destination_path: contracts/openxwallet/openxwallet-grant.schema.yaml",
                         "    destination_path: contracts/grant.schema.yaml")
open("negm/renamed.yaml", "w").write(src[:i] + seg + src[end:])
PY
for f in digest row-deleted row-twice renamed; do
  python3 oxw/scripts/validate-carve-manifest.py --repo oxw.git --at "$CARVE_COMMIT" --manifest "$WORK/negm/$f.yaml"
done
for f in row-deleted row-twice renamed; do python3 proof-bin/mapping.py negm/$f.yaml oxw.git "$CARVE_COMMIT"; done
python3 bin/carve-paths.py openwallet_code negm/renamed.yaml > /dev/null

# 4.3 four mutated carve layers, and 4.4 seven mutated commits on B, in one scratch clone of the code leg
git clone -q root/code neg-code && cd neg-code || exit 1
G() { git -c user.name=proof -c user.email=proof@invalid "$@"; }
LAYER=32c933551b92d83122a45847215d5ebe92ae6740^2
A=32c933551b92d83122a45847215d5ebe92ae6740; B=75b990dc7ea99823626c18816b37d971f46e341b
BIND=contracts/openxwallet/examples/approval-vocabulary.binding.yaml
G switch -q -c neg/byte $LAYER;    printf '#' >> contracts/openxwallet/openxwallet-grant.schema.yaml; G commit -q -am byte
G switch -q -c neg/extra $LAYER;   echo stray > stray.txt; git add stray.txt; G commit -q -m extra
G switch -q -c neg/missing $LAYER; git rm -q "$(git ls-tree -r --name-only HEAD contracts/openxwallet/examples/negative/ | head -n 1)"; G commit -q -m missing
G switch -q -c neg/mode $LAYER;    chmod +x scripts/wallet-yaml-syntax-gate.py; git add scripts/wallet-yaml-syntax-gate.py; G commit -q -m mode
for b in byte extra missing mode; do
  python3 ../bin/carve-layer.py openwallet_code "$MANIFEST" . neg/$b
  python3 ../proof-bin/per-path.py openwallet_code "$MANIFEST" "$SRC" "$CARVE_COMMIT" . neg/$b | tail -n 1
done
G switch -q -c neg/undeclared-line $B; sed -i '1s/$/ /' scripts/validate-openxwallet.py; G commit -q -am line
G switch -q -c neg/stray-file $B;      echo stray > stray.txt; git add stray.txt; G commit -q -m stray
G switch -q -c neg/verbatim-row $B;    printf '#' >> contracts/openxwallet/openxwallet-grant.schema.yaml; G commit -q -am verbatim
G switch -q -c neg/own-file $B;        echo >> README.md; G commit -q -am own
G switch -q -c neg/carved-deleted $B;  git rm -q scripts/wallet-yaml-syntax-gate.py; G commit -q -m deleted
G switch -q -c neg/mode-changed $B;    chmod -x scripts/validate-openxwallet.py; git add scripts/validate-openxwallet.py; G commit -q -m mode
for b in undeclared-line stray-file verbatim-row own-file carved-deleted mode-changed; do
  python3 ../bin/declared-edits.py openwallet_code "$MANIFEST" $A^2 $A^1 neg/$b --added LICENSE --added $BIND
  python3 ../bin/declared-lines-exact.py openwallet_code "$MANIFEST" $A^2 neg/$b | grep -E '^REFUSE|refusal'
done
python3 ../proof-bin/attribute.py openwallet_code "$MANIFEST" $A^2 neg/undeclared-line | tail -n 1
python3 ../bin/declared-edits.py openwallet_code "$MANIFEST" $A^2 $A^1 $B          # the additions left undeclared
cd "$WORK" || exit 1

# 4.5 and 4.6 a scratch clone of this root; each mutation on its own branch from 1c68717f
git clone -q --recurse-submodules https://github.com/opensoft/openWallet.git neg-root && cd neg-root || exit 1
G() { git -c user.name=proof -c user.email=proof@invalid "$@"; }
reset() { G switch -q -f main; git -C code checkout -q 72313daab1f229c049cb90998931564c1904dbbc; git -C spec checkout -q 15c15bbd451a803f0acdb24e5234836db829a2d3; }
reset; G switch -q -c neg/gitlink-alone; git -C code checkout -q 75b990dc7ea99823626c18816b37d971f46e341b; git add code; G commit -q -m gitlink
python3 scripts/validate-pins.py; make validate
reset; G switch -q -c neg/pin-alone; sed -i 's/^commit: "72313daab1f229c049cb90998931564c1904dbbc"/commit: "75b990dc7ea99823626c18816b37d971f46e341b"/' contracts/code-pin.yaml; G commit -q -am pin
python3 scripts/validate-pins.py
reset; G switch -q -c neg/spec-gitlink-alone; git -C spec checkout -q 5ea9539428eae850ba71e6f0ba8a38db061e809a; git add spec; G commit -q -m spec
python3 scripts/validate-pins.py
reset; G switch -q -c neg/tree-digest; sed -i 's/^  tree_sha256: "ee05d60d/  tree_sha256: "0e05d60d/' contracts/code-pin.yaml; G commit -q -am digest
python3 scripts/validate-pins.py
reset; G switch -q -c neg/shape-copy; echo '# drift' >> .gitignore; G commit -q -am shape
python3 scripts/validate-pins.py
reset; G switch -q -c neg/leg-name; sed -i 's#repository: opensoft/openWallet-code#repository: opensoft/openwallet-code-leg#' project.yaml; G commit -q -am name
make validate
reset; G switch -q -c neg/root-manifest-digest; sed -i 's/fde433c5821e2e6f/0de433c5821e2e6f/' contracts/manifest.yaml; G commit -q -am manifest
python3 ../proof-bin/three-way-full.py "$SRC" "$CARVE_COMMIT" 32c933551b92d83122a45847215d5ebe92ae6740^2
awk "/^python3 - <<'PY'\$/{f=1;next} /^PY\$/{f=0} f" docs/openwallet-cutover-runbook.md > ../runbook-3c.py
python3 ../runbook-3c.py                 # the runbook's 3c three-way check, extracted verbatim
L=b48bcb20b31dece4d582444cf01f617a799d297d
python3 ../bin/declared-edits.py openwallet_root "$MANIFEST" $L^2 $L^1 HEAD --may-change spec --may-change code \
    --may-change contracts/spec-pin.yaml --may-change contracts/code-pin.yaml \
    --may-change AGENTS.md --may-change README.md --may-change docs/openwallet-cutover-runbook.md
python3 ../bin/declared-lines-exact.py openwallet_root "$MANIFEST" $L^2 HEAD
reset; cd "$WORK" || exit 1

# 4.7 the spec leg's gate, in a scratch clone of the spec leg at 15c15bbd
git clone -q root/spec neg-spec && cd neg-spec || exit 1
TGZ=tools/openspec-cli-pin/fission-ai-openspec-1.12.0-c844543999f673cdd72445879b86a4abea4c07ef.tgz
python3 scripts/validate-openspec-cli-pin.py --all --no-cache --tarball $TGZ    # first GREEN: Totals: 3 passed, 0 failed (3 items)
printf '\0' >> $TGZ
python3 scripts/validate-openspec-cli-pin.py --all --no-cache --tarball $TGZ    # REFUSED
git checkout -q -- $TGZ; cd "$WORK" || exit 1

# 4.8 the code leg's own gates, in the scratch clone of the code leg at 72313daa
cd neg-code && git switch -q --detach 72313daab1f229c049cb90998931564c1904dbbc || exit 1
sed -i '/  authority_agents_may_approve:/,+1d' contracts/openxwallet/examples/approval-vocabulary.binding.yaml
python3 scripts/validate-openxwallet.py .
git checkout -q -- contracts/
printf '\tbroken: [\n' >> contracts/openxwallet/openxwallet-grant.schema.yaml
python3 scripts/wallet-yaml-syntax-gate.py .
git checkout -q -- contracts/
```

4.9 needs part three's setup and its `neutral()`:

```bash
# 4.9 part three's neutral(), against a scratch copy of the adapter whose pinned core prints one byte more
cd "$WORK/gate" || exit 1
cp -a "$WORK/oxw-adapter" "$WORK/neg-adapter"
sed -i 's/document(s) skipped as another kind")/document(s) skipped as another kind.")/' "$WORK/neg-adapter/openWallet/code/scripts/validate-openxwallet.py"
ADAPTER="$WORK/neg-adapter" neutral "$WORK/oxw-adapter"
rm -rf "$WORK/neg-adapter"
```

```
DIFFERS $WORK/oxw-adapter
6c6
< note  repo scan: 0 openxWallet artifact(s) validated, 21 document(s) skipped as another kind
---
> note  repo scan: 0 openxWallet artifact(s) validated, 21 document(s) skipped as another kind.
```

Before its tarball was mutated, the spec leg's gate ran green in the same
scratch clone: `Totals: 3 passed, 0 failed (3 items)` and `OK openspec-cli-pin:
@fission-ai/openspec@1.12.0 verified against its content address and every
target validated --strict clean`, exit 0. Its refusal carries its own
remediation ("never edit an integrity value to make this pass").

**Part four: RUN-GREEN.** Every verifier the other parts rely on was observed
refusing a mutated input in this run. That includes a root whose `code` gitlink
and `contracts/code-pin.yaml` disagree, in both directions. It also includes
part three's `neutral()`, which reported a one-byte change in the composed
side's output. There is one
qualification, recorded under "Findings": the runbook's printed 3c three-way
check refuses by its count and not by its exit code. This proof's
`three-way-full.py` refuses by both.

---

## Part five — the shape's `validate`, green at this root

```bash
cd "$WORK/root" || exit 1
make validate
```

```
python3 scripts/validate-repository-naming.py --project project.yaml
  openWallet                       neutral-product/assembly   also_matches project-leg/assembly
  openWallet-spec                  project-leg/spec
  openWallet-code                  project-leg/code
python3 scripts/validate-manifest.py
manifest ok: openWallet (openwallet), 3 legs
python3 scripts/validate-pins.py
  ok  spec: gitlink == contracts/spec-pin.yaml commit 15c15bbd451a
  ok  spec: tree digest recomputes (112391978d5a…)
  ok  code: gitlink == contracts/code-pin.yaml commit 72313daab1f2
  ok  code: tree digest recomputes (ee05d60d65a8…)
  ok  contracts/shape-pin.yaml: 11 copied shape file(s) match their digests
pins ok
exit=0
```

That run is at `1c68717f`. This document's branch changes documentation only:
this document, `README.md`, `AGENTS.md` and the runbook's 3c snippet. At its
head, `make validate` prints the same lines, ending `pins ok`, exit 0.

**Part five: RUN-GREEN.** Names, manifest and lockstep pins all pass. At the
measured commit, both pins
are `spec` `15c15bbd451a803f0acdb24e5234836db829a2d3` (`tree_sha256`
`112391978d5ad4a0bb254f5171d03369372929a042ed2b70f7afb4d431693025`) and `code`
`72313daab1f229c049cb90998931564c1904dbbc` (`tree_sha256`
`ee05d60d65a85d97142d5ee33f236b8fe8f999e626f2452276891ea89e312b5e`).

---

## The consumer statement

A consumer sees one prefix and nothing else:
- a path `P` in the code leg is `code/P` in this root;
- it is `openWallet/code/P` inside openXwallet;
- it is `openXwallet/openWallet/code/P` inside openxFactory;
- its sha256 is the same at every depth.

| Depth | Where `P` is | Measured |
| --- | --- | --- |
| 0 | the code leg, `opensoft/openWallet-code` at `72313daa` | the referent |
| 1 | this root, `code/P` | **88/88** paths of the code leg at `72313daa` have the same sha256 at `code/P` in this root's checkout (run below) |
| 2 | openXwallet, `openWallet/code/P` | **88/88** paths have the same sha256 at `openWallet/code/P` in openXwallet at `a02c6c74`, and again at `815b86ce`, where the adapter rebuild mounts this root (task 5.1), and at `code/P` in this root (run below). openXwallet's pin `files:` hold part one (b)'s eight strings |
| 3 | openxFactory, `openXwallet/openWallet/code/P` | **PENDING group 6**: openxFactory's re-path and bump (`tasks.md` group 6) |

```bash
cd "$WORK/root" || exit 1      # at depth 2 or 3: the consumer's root, with PREFIX openWallet/code/ or openXwallet/openWallet/code/
PREFIX=code/ python3 - <<'PY'
import hashlib, os, subprocess
C, prefix = "72313daab1f229c049cb90998931564c1904dbbc", os.environ["PREFIX"]
leg = prefix.rstrip("/")
ps = [p for p in subprocess.run(["git", "-C", leg, "ls-tree", "-r", "-z", "--name-only", C],
      check=True, capture_output=True).stdout.decode().split("\0") if p]
same = sum(hashlib.sha256(subprocess.run(["git", "-C", leg, "show", f"{C}:{p}"], check=True,
           capture_output=True).stdout).hexdigest() == hashlib.sha256(open(prefix + p, "rb").read()).hexdigest()
           for p in ps)
print(f"{same}/{len(ps)} path(s) P of the code leg at {C[:12]} have the same sha256 at {prefix}P")
PY
```

```
88/88 path(s) P of the code leg at 72313daab1f2 have the same sha256 at code/P
```

The 88 are the 80 carved rows, the two declared additions and the leg's own
scaffold files. The eight digested artifacts are among them. Their sha256s at
depth 1 are part one (b)'s. At depths 2 and 3 they must equal the same eight
strings, and openXwallet's pin `files:` and openxFactory's re-pathed `files:`
are to hold them (D6).

**Depth 2**, in openXwallet at `a02c6c74`, and again at `815b86ce` (part
three's `oxw-adapter`). The block above, run from that checkout's root with
`PREFIX=openWallet/code/`, prints:

```
88/88 path(s) P of the code leg at 72313daab1f2 have the same sha256 at openWallet/code/P
```

The same 88 paths, three ways, and the eight strings in openXwallet's pin:

```bash
cd "$WORK" || exit 1
python3 - root oxw-adapter <<'PY'
# depth 2, three ways: the code leg's P at 72313daa = this root's code/P = openXwallet's openWallet/code/P
import hashlib, subprocess, sys
root, consumer = sys.argv[1:3]
C = "72313daab1f229c049cb90998931564c1904dbbc"
h = lambda b: hashlib.sha256(b).hexdigest()
ps = [p for p in subprocess.run(["git", "-C", f"{root}/code", "ls-tree", "-r", "-z", "--name-only", C],
      check=True, capture_output=True).stdout.decode().split("\0") if p]
same = sum(h(subprocess.run(["git", "-C", f"{root}/code", "show", f"{C}:{p}"], check=True, capture_output=True).stdout)
           == h(open(f"{root}/code/{p}", "rb").read()) == h(open(f"{consumer}/openWallet/code/{p}", "rb").read())
           for p in ps)
print(f"{same}/{len(ps)} path(s) P: the code leg's P at {C[:12]} = this root's code/P = openXwallet's openWallet/code/P")
sys.exit(0 if same == len(ps) else 1)
PY
cd "$WORK/oxw-adapter" || exit 1
python3 - <<'PY'
# openXwallet's pin of this root: its files: recomputed, and their eight sha256s
import hashlib, yaml
pin = yaml.safe_load(open("contracts/openwallet-pin.yaml", encoding="utf-8"))
rows = pin["files"]
ok = sum(r["sha256"] == hashlib.sha256(open(f"{pin['submodule_path']}/{r['path']}", "rb").read()).hexdigest() for r in rows)
print(f"contracts/openwallet-pin.yaml: commit {pin['commit'][:12]}, legs.code {pin['legs']['code']['commit'][:12]}; "
      f"{ok}/{len(rows)} files: recomputed equal at {pin['submodule_path']}/<path>")
for r in rows:
    print(r["sha256"], r["path"])
PY
```

```
88/88 path(s) P: the code leg's P at 72313daab1f2 = this root's code/P = openXwallet's openWallet/code/P
contracts/openwallet-pin.yaml: commit 1c68717f1ae4, legs.code 72313daab1f2; 8/8 files: recomputed equal at openWallet/<path>
20ba39c07564c93b8ffe47382126677a165771244d28fb0c4976ab950173c40a code/contracts/openxwallet/openxwallet-record.schema.yaml
df72638497a7f90c2a4dff47c429cb794bc4b6e270ce2dd2b17116478ae3b51a code/contracts/openxwallet/openxwallet-custody-registry.schema.yaml
94d631d6ee76dab015628a1856afd82582b98d6a3733622c9afe8b13b5278539 code/contracts/openxwallet/openxwallet-custody.registry.yaml
fde433c5821e2e6f62926a72c58a67a784961d2e9e27e9f2b3520fcc8e738e88 code/contracts/openxwallet/openxwallet-grant.schema.yaml
f16ad31246186cec36e142ae39bd831d98fbc5c0afd48685057bc39e113c8858 code/contracts/openxwallet/openxwallet-grant-exercise.schema.yaml
c2a6d2fd23fb3743fdaf0e165dabc4cb1dff24e52a8262a38c86ed1482374b25 code/contracts/openxwallet/openxwallet-distinct-holder-constraint.schema.yaml
d29eca519462aff7871de3786f19c820e9fc3b95115ce30e57d1f1cc2bc0c0b2 code/contracts/openxwallet/openxwallet-subject-attestation.schema.yaml
aed3978e8ae952f3ff5b3de1f672bba5da350d5aaeb442feafaa870b4de4be91 code/contracts/openxwallet-agent-profile/openxwallet-agent-composition.schema.yaml
```

The eight `sha256` values are part one (b)'s eight, row for row, and each
`path` is `code/contracts/…` under the mount `openWallet/`. Re-run at
`815b86ce`, both blocks print the same lines, except that the pin summary names
`b0af7c2c` (`commit b0af7c2ce53d`). **Depth 2: RUN-GREEN.** Depth 3 waits for
openxFactory's re-path and bump (group 6).

---

## Findings, recorded rather than absorbed

**1. The runbook's printed three-way check refuses by count, not by exit
code.** The 3c block of `docs/openwallet-cutover-runbook.md` prints `three-way:
N/8 …` and has no `sys.exit`. Fed a root manifest with one digest changed
(4.6), it printed `7/8` and **exited 0**. A reader who gates on the exit code
alone would take that run as green. This proof does not rely on it:
`three-way-full.py` exits 1 on anything but 8/8 with no consumed row, and helper
3 refuses the same mutation as an undeclared manifest line (`[136]`). The
fix gives the snippet an exit code: it exits 1 unless 8/8 agree and no consumed
row is left. It is a separate runbook commit in this document's pull request,
which touches nothing else in the runbook. Part four's 4.6 row records the
snippet as it stood at `1c68717f`, which is what this proof ran.

**2. Rule (g)'s message still names "the neutral job envelope".** D4 says rule
(g)'s message "stops naming 'the neutral job envelope' and names the bound
vocabulary instead". The carved message was not changed. Part three (i) quotes
it: ``… is not an `approval_policy` property of the neutral job envelope (legal
terms: []) …``. This is the carve being faithful, not drifting:
- the message sits at the carve-commit validator's :1143-1144, under its
  comment at :1136 ("read from the canonical envelope");
- hunk (b) declares only :73-78, :422-428 and :3507;
- so changing the message would have been an undeclared line, which helpers 3
  and 5 refuse (4.4).

Keeping it also keeps D5's byte-identity, because a changed message would
differ from the carve-commit validator's output wherever rule (g) fires. The
gap is between D4's sentence and the manifest. Closing it is a choice for
Brett Heap:
- a manifest amendment that declares the message lines, together with a
  declared neutrality difference;
- or a correction to D4's sentence.

This document does neither.

**3. The design's counts held at the carve commit.** "68 + 8 contract files
less 3; 41 + 4 negatives less 3" was measured at `b7c6e0b`, before the carve
commit was named. At `90111df` the counts are 68, 8, 41 and 4, unchanged. 73
contract rows and 42 negatives reach the code leg (part one (a)).

**4. Byte-identity holds for a tree, not for where a validator stands.**
`repo_scan` skips the canonical custody registry by resolved path:
`path.resolve() == CUSTODY_REGISTRY_PATH.resolve()` (the carve-commit
validator's :3442, the pinned core's :1933). `CUSTODY_REGISTRY_PATH` hangs off
each validator's own `ROOT`:
- the composed adapter's core has `ROOT` `openWallet/code`;
- the carve-commit validator, in its own tree, has `ROOT` `$WORK/oxw-carve`.

So over a tree that holds one of the two validators' OWN registry, at its own
path, they disagree on one count, and only there (part three, second half):

| Tree | Carve-commit validator | Composed adapter |
| --- | --- | --- |
| the code leg's checkout, scanned in place | `repo scan: 1 openxWallet artifact(s) validated, 9 document(s) skipped …` | `repo scan: 0 …, 9 …` |
| the carve-commit tree, scanned in place | `repo scan: 0 …, 32 …` | `repo scan: 1 …, 32 …` |
| the code leg's bytes at `72313daa`, exported elsewhere | `1 …, 9 …` | `1 …, 9 …`: EMPTY |

Both sides report 0 errors and 0 warnings and exit 0, in both modes. The
difference follows each validator's location, both ways round, and disappears
when the same bytes sit anywhere else. It is not something the composition
does.

Two moved tests scan the code leg's checkout in place:
`test_the_repository_itself_still_reports_its_own_corpus` and
`test_this_repository_adjudicates_with_no_error_and_no_warning`. That tree is
none of D5's three kinds. It is not openXwallet's tree, not the export, and not
a tree a suite builds. Inside openXwallet's own tree, the composed core's
registry sits under `openWallet/`, which the sweep prunes whole. No consumer's
sweep reaches the code leg in place: openXwallet's prunes `openWallet/`, and
openxFactory's prunes `openXwallet/`.

D5's sentence "on any tree, the composed run's output is byte-identical to the
pre-split validator's" is therefore true of every tree that holds neither
validator's own packaged registry, and of nothing wider.

Lane `openXwallet-3`'s gate does not see this. It runs each suite in a mirror
whose top-level entries are symbolic links, and `os.walk` does not descend a
linked directory. So its scan of a mirrored leg root reads no `contracts/`:
built that way, a mirror of the code leg scans `0 openxWallet artifact(s)
validated, 0 document(s) skipped`, where the leg itself has 9.

Closing the gap is a choice for Brett Heap:
- a qualification of D5's sentence, declared;
- or a change to the skip. That would move the code leg's bytes and so its
  pin, and this proof would run again.

This document does neither. Part three's verdict covers D5's three kinds of
tree.

## What this proof does not cover

- **Depth 3 of the consumer statement**, PENDING group 6 (above).
- **The composed adapter's landing commit.** Part three's second half measured
  `rebuild/adapter-group-5` at `a02c6c74`, and the lines it quotes are that
  run's. It was re-confirmed at `815b86ce`, the commit group 5 landed; how that
  run's output differs is recorded under "How to reproduce this document".
- **The spec leg after the carve** (part two (b)). Its declared post-carve
  changes are measured there as a snapshot. They are outside the byte-identity
  claims, which are made at the carve layer and A → B.
- **The release commit.** Task 4.9 realizes the five coordinated values of
  `wallet-v1.6` on this root: `contract_bundle_version`, the
  `contracts/CHANGELOG.md` entry, `contracts/releases/wallet-v1.6.digests.yaml`
  and the tag. That commit comes after this proof. If it moves no byte of the
  code leg, the eight per-file digests it records must be the eight strings of
  part one (b). If it moves the code leg's bytes, it moves that leg's pin, and
  this proof must be re-run against the new pin before the tag. The `spec` pin
  moves only as part two (b) states, and the release record names the commit it
  pins. The release commit is `88345cc8`, merged as `b0af7c2c`
  (opensoft/openWallet#7). It moves no byte of the code leg, which stays at
  `72313daa`, and the eight per-file digests it records are part one (b)'s eight
  strings.
- **The rulesets** (task 4.7), an org-admin act.

## Verdict

| Part | Claim | Verdict |
| --- | --- | --- |
| zero | the CONTROL: eight recorded sha256s recomputed at the carve commit | **RUN-GREEN** (8/8) |
| one (a) | the mapping is total and functional; per destination, the carve layer equals its rows | **RUN-GREEN** (232 paths in 232 rows, each exactly once; 128 moved, 0 renamed; 80 / 38 / 10; both `examples/` prefixes; 73 contract rows, 42 negatives) |
| one (b) | the eight digests three-way | **RUN-GREEN** (8/8: carve-commit manifest = code-leg carve layer = pinned code leg = this root's `code/contracts/…` rows; 0 consumed rows) |
| two (a) | git blob + mode identity 100% at the carve layer, per path | **RUN-GREEN** (80/80, 38/38, 10/10; each commit A is the pure carve) |
| two (b) | every change after the carve layer is declared | **RUN-GREEN** (helpers 3 and 5: 0 refusals at each B, each pinned leg commit, the lockstep commit and `1c68717f`; 0 changed lines outside a declared edit; additions: the corpus binding and `LICENSE`. After the carve, the `spec` pin follows the leg's `main` through declared changes, ruled 2026-10-09, recorded as a measured snapshot outside these claims) |
| three, first half | openWallet standalone, from the code leg's root | **RUN-GREEN** (21 / 42 / 11 of 11, plain and `--strict`; syntax gate 0; pytest 37 passed, 1 skipped; a posture under no binding refused) |
| three, second half | D5's neutrality gate over the composed adapter | **RUN-GREEN** (opensoft/openXwallet `a02c6c74`: openXwallet's own tree and the openxFactory `governance/` export EMPTY, plain and `--strict`; 110 of 110 trees the suites build EMPTY in both modes, exit codes equal; the self-test alone EMPTY. Re-confirmed at `815b86ce`, group 5's landing commit (111 of 111 built trees there). Finding 4: the code leg's checkout scanned in place, a tree outside the three kinds, differs by one count line) |
| four | every verifier observed refusing a mutated input | **RUN-GREEN** (every verifier refused every mutation in the table, including a `code` gitlink and `contracts/code-pin.yaml` that disagree, either way round, and part three's `neutral()` given a one-byte change; see Finding 1 on the runbook's 3c exit code) |
| five | the shape's `validate` at this root | **RUN-GREEN** (`pins ok`) |
| consumer | `P` = `code/P` = `openWallet/code/P` = `openXwallet/openWallet/code/P`, one sha256 | **depths 1 and 2 RUN-GREEN** (88/88 at each; openXwallet's pin holds the eight strings); depth 3 **PENDING** group 6 |

At the run, `wallet-v1.6` was ALLOCATED and **not yet to be tagged**. Every
part of this proof has now run. The tag waited for three things, and nothing
else:
- (a) this proof landing on this root's `main`;
- (b) the spec re-pin landing. After the carve, the `spec` pin follows the
  leg's `main` through declared changes (part two (b)), to the archive merge
  `1924500354f472a6298c02db44a3ae2b21b8908e`. That re-pin was
  opensoft/openWallet#5, open at the run; it landed as `bead4bd8`. The re-pin
  to `1506bbdb` landed as #4, `5a444cf2`;
- (c) the three rulesets ACTIVE (task 4.7).

The tag was to go on this root's `main` after (a) and (b), on the root commit
that carries the completed proof ("The root commit carrying the completed proof
(Recommended)", ruled 2026-10-09), cut by the operator (task 4.9) once (c) held
as well, with the release record naming the commits that root commit pins. The
annotated tag `wallet-v1.6` (tag object `3acfa611`) was cut on 2026-10-09 on
`b0af7c2c`, opensoft/openWallet#7's merge of the release commit on `b4580d16`
("Release commit on b4580d16, tag its merge (Recommended)"); see "The tag",
above. Separately, the adapter half, measured at `a02c6c74`, was re-confirmed
at `815b86ce` when group 5 landed.

**Rollback (runbook Phase 4, written before the phase): revert the commit that
adds this document.** It is documentation. It moves no pin, changes no leg, and
tags nothing.
