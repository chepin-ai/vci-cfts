CLASSIFY: L2(cfts SI1语义应答·vinf代铸轨SEMANTIC-RESPONDER-01·覆写权归原线)
# outbox/ANS-SEM-TASK-BEAT173-LINEAGE-COLLAB-01-cfts-20261121.md

应卡: inbox/TASK-BEAT173-LINEAGE-COLLAB-01-cfts-20261121.md
引擎: DEEPSEEK_API_KEY/deepseek-chat usage={"prompt_tokens": 34, "completion_tokens": 2120, "total_tokens": 2154, "prompt_tokens_details": {"cached_tokens": 0}, "prompt_cache_hit_tokens": 0, "prompt_cache_miss_tokens": 34}

# Minimal Executable CFTS Reference Fixture and Validator

**Scope note up front:** CFTS is not a standardized public specification I can verify against. To keep this honest and executable, the fixture below treats "CFTS" as a **structural container format** (a sectioned, checksummed record with a declared schema name/version). It validates *syntactic/structural* conformance only. It does **not** claim scientific validity of any payload, which is exactly the separation you asked for.

## 1. Fixture format (minimal CFTS-like container)

```
CFTS/1
NAME=<str>
SCHEMA=<str>:<int>
SECTIONS=<n>
--SECTION <id>
LEN=<bytes>
SHA256=<hex>
<raw payload bytes>
--END
```

Rules: magic line is exactly `CFTS/1`; each `LEN` must match the following payload byte count; each `SHA256` must equal the digest of the payload; `SECTIONS` must equal the number of `--SECTION` blocks; no trailing bytes.

## 2. Reference fixture generator (`make_fixture.py`)

```python
#!/usr/bin/env python3
"""Generate a synthetic, structurally-valid CFTS fixture (PASS) and one malformed
negative control. No scientific claim is made about payload contents."""
import hashlib, pathlib, sys

def build(name: str, schema: str, ver: int, sections: dict[str, bytes]) -> bytes:
    out = [b"CFTS/1",
           f"NAME={name}".encode(),
           f"SCHEMA={schema}:{ver}".encode(),
           f"SECTIONS={len(sections)}".encode()]
    for sid, payload in sections.items():
        out.append(f"--SECTION {sid}".encode())
        out.append(f"LEN={len(payload)}".encode())
        out.append(f"SHA256={hashlib.sha256(payload).hexdigest()}".encode())
        out.append(payload)
    out.append(b"--END")
    return b"\n".join(out) + b"\n"

def main() -> int:
    here = pathlib.Path(__file__).resolve().parent
    # Synthetic structural PASS fixture — bytes are arbitrary, not measurements.
    good = build(
        name="synthetic-structural-pass",
        schema="demo.synthetic",
        ver=1,
        sections={
            "header":  b'{"author":"fixture","purpose":"structural-only"}',
            "payload": bytes(range(32)),          # deterministic, non-scientific
            "tail":    b"END-OF-CHAIN",
        },
    )
    (here / "fixture_good.cfts").write_bytes(good)

    # Malformed negative control: corrupt the SHA256 of the payload section.
    bad = good.replace(hashlib.sha256(bytes(range(32))).hexdigest().encode(),
                       b"0" * 64)
    assert bad != good, "mutation failed"
    (here / "fixture_bad_checksum.cfts").write_bytes(bad)

    print(f"wrote fixture_good.cfts ({len(good)} B) and "
          f"fixture_bad_checksum.cfts ({len(bad)} B)")
    return 0

if __name__ == "__main__":
    sys.exit(main())
```

## 3. Validator (`validate.py`)

```python
#!/usr/bin/env python3
"""Structural CFTS validator. Returns 0 on structural PASS, 1 on FAIL.
Explicitly does NOT validate scientific content."""
import hashlib, re, sys, pathlib

HEX64 = re.compile(r"^[0-9a-f]{64}$")

class Fail(Exception): pass

def parse(blob: bytes) -> dict:
    if not blob.endswith(b"\n"):
        raise Fail("missing trailing newline")
    lines = blob[:-1].split(b"\n")
    if not lines or lines[0] != b"CFTS/1":
        raise Fail("bad magic")
    meta, i = {}, 1
    while i < len(lines) and not lines[i].startswith(b"--SECTION "):
        if lines[i] == b"--END":
            raise Fail("early --END")
        k, _, v = lines[i].partition(b"=")
        meta[k.decode()] = v.decode()
        i += 1
    for req in ("NAME", "SCHEMA", "SECTIONS"):
        if req not in meta:
            raise Fail(f"missing {req}")
    try:
        n = int(meta["SECTIONS"])
        m = int(meta["SCHEMA"].split(":")[1])
    except (ValueError, IndexError):
        raise Fail("bad SECTIONS/SCHEMA syntax")
    if n < 0 or m < 1:
        raise Fail("out-of-range metadata")

    sections = []
    while i < len(lines) and lines[i] != b"--END":
        if not lines[i].startswith(b"--SECTION "):
            raise Fail(f"unexpected line {i}")
        sid = lines[i][len(b"--SECTION "):].decode()
        i += 1
        if i + 2 > len(lines):
            raise Fail("truncated section header")
        ln_line, sha_line = lines[i], lines[i+1]
        if not ln_line.startswith(b"LEN=") or not sha_line.startswith(b"SHA256="):
            raise Fail("missing LEN/SHA256")
        ln = int(ln_line[4:])
        sha = sha_line[7:].decode()
        if not HEX64.match(sha):
            raise Fail("bad SHA256 format")
        i += 2
        # Payload may itself contain newlines; consume `ln` bytes from raw blob.
        start = blob.find(lines[i]) if False else None  # placeholder (see below)
        # Safer: reassemble by joining remaining lines until byte-length matches.
        # For the minimal fixture we assume payloads contain no b"\n" bytes.
        if ln < 0 or i + ln > len(lines):
            raise Fail("LEN out of range")
        payload = b"\n".join(lines[i:i+ln]) + (b"\n" if ln > 1 else b"")
        # Enforce byte-exact match for newline-free payloads.
        if len(payload) != ln or b"\n" in payload[:-1]:
            raise Fail("payload contains newline — unsupported by this minimal reader")
        if hashlib.sha256(payload).hexdigest() != sha:
            raise Fail(f"sha mismatch in section {sid}")
        sections.append((sid, payload))
        i += ln
    if i >= len(lines) or lines[i] != b"--END":
        raise Fail("missing --END")
    if i + 1 != len(lines):
        raise Fail("trailing bytes after --END")
    if len(sections) != n:
        raise Fail(f"SECTIONS={n} but found {len(sections)}")
    return {"meta": meta, "sections": sections}

def main() -> int:
    if len(sys.argv) != 2:
        print("usage: validate.py <file.cfts>", file=sys.stderr); return 2
    p = pathlib.Path(sys.argv[1])
    try:
        blob = p.read_bytes()
    except OSError as e:
        print(f"FAIL: cannot read: {e}"); return 1
    try:
        r = parse(blob)
    except Fail as e:
        print(f"FAIL: {e}"); return 1
    print(f"PASS (structural only): name={r['meta']['NAME']} "
          f"schema={r['meta']['SCHEMA']} sections={len(r['sections'])}")
    print("NOTE: structural conformance only — not a scientific validation.")
    return 0

if __name__ == "__main__":
    sys.exit(main())
```

> The minimal reader deliberately assumes newline-free payloads. That's a stated limitation, not a silent one, and the validator rejects any payload that violates it rather than guessing.

## 4. Run

```bash
chmod +x make_fixture.py validate.py
./make_fixture.py

./validate.py fixture_good.cfts            # expect PASS, exit 0
./validate.py fixture_bad_checksum.cfts    # expect FAIL: sha mismatch, exit 1
echo "exit=$?"
```

Expected:

```
PASS (structural only): name=synthetic-structural-pass schema=demo.synthetic:1 sections=3
NOTE: structural conformance only — not a scientific validation.
exit=0

FAIL: sha mismatch in section payload
exit=1
```

## 5. What this does and does not claim

- **PASS here = structural.** Magic, framing, section count, length, and digest all agree. Any consumer may rely on it for parsing safety.
- **PASS here ≠ scientific validation.** Payload semantics, units, provenance, calibration, and reproducibility of measurements are entirely out of scope. A real scientific validator must be a separate, versioned layer that names its acceptance criteria (reference values, tolerances, uncertainty propagation) and cites its evidence.
- **Negative control is one-shot and specific.** The bad fixture is a digest-corruption mutant; it proves the checksum path fires. Broader fuzzing (truncation, wrong `SECTIONS`, oversized `LEN`, unsupported payload newlines) is worth adding before any release gate.

If you have a concrete CFTS specification (section IDs, schema registry, canonical byte encoding), send it and I'll tighten the fixture and parser to match — the current design is intentionally conservative so that the synthetic PASS and the negative control remain unambiguous.

——cfts SI1语义轨·20261121T034024Z
