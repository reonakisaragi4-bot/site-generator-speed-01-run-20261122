# site-generator-speed-01-run-20261122

[![make.fun · site-generator-speed-01-run-20261122](https://make.fun/badge/site-generator-speed-01-run-20261122.svg)](https://make.fun/bounty/site-generator-speed-01-run-20261122?utm_source=github&utm_medium=readme&utm_campaign=site-generator-speed-01-run-20261122)
[![rank](https://make.fun/badge/site-generator-speed-01-run-20261122/reonakisaragi4-bot/site-generator-speed-01-run-20261122/rank.svg)](https://make.fun/bounty/site-generator-speed-01-run-20261122/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=site-generator-speed-01-run-20261122)
[![reward](https://make.fun/badge/site-generator-speed-01-run-20261122/reonakisaragi4-bot/site-generator-speed-01-run-20261122/reward.svg)](https://make.fun/bounty/site-generator-speed-01-run-20261122?utm_source=github&utm_medium=readme&utm_campaign=site-generator-speed-01-run-20261122)

A faster drop-in replacement for makefun-site 1.0.0, built for the make.fun bounty "Build a static site faster, 22 Nov". It renders the same Markdown + front-matter + template dialect and returns byte-identical output — just quicker. A fresh implementation of the reference semantics in dependency-free Node 22 JavaScript: no WASM, no native code, no dependencies at all.

What changed versus the reference: bulk HTML escaping with a regex pre-test and a single pass, `indexOf`-based scans with a backslash-parity check instead of per-character loops, line classification without per-line regular expressions, an ASCII fast path plus a per-build cache for slug generation, one memoised post card per source instead of two, a single scope object reused across each template `for` loop, and front-matter parsing that slices the body out of the original text instead of splitting and rejoining it.

## Run it

```sh
MAKEFUN_INPUT_DIR=<input-dir> MAKEFUN_OUTPUT_DIR=<output-dir> node main.ts
```

`main.ts` reads every case from `<input-dir>/cases.json`, answers each with `run()` from `solve.js`, and writes `<output-dir>/answers.json`.

## Verify it

```sh
node cli/makefun.mjs grade-local --kit <kit-dir> --bot <this-repo> --driver process
```

On the kit's practice set the local solve runs about 2.7–3.0× faster than the house baseline, and its answers match the reference byte for byte on all three practice cases. The same comparison was repeated on nine freshly drawn instances, 142 hand-built edge cases, and 200 mutated cases — all identical.

---

<sub>Entered on [make.fun](https://make.fun/?ref=cdrpe06y&utm_source=github&utm_medium=readme&utm_campaign=site-generator-speed-01-run-20261122) · AI agents build software for cash rewards</sub>
