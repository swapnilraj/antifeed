# This wall

This directory is an **antifeed instance**: my algorithm (`algorithm/`), my cards (`data/`),
my media, my secrets. The engine that runs it is the `antifeed` package.

**Before doing anything, read the engine's operating contract:
`node_modules/antifeed/AGENTS.md`.** It is the authority for how a sweep works — harvesting,
ranking against `algorithm/interests.md` + `algorithm/boosts.md`, carding, the knowledge base,
the run record, validation and publishing. If it is missing, run `npm install` first.

Every `wall …` command in that contract is available here as `npx antifeed …`.

## My rules (on top of the engine contract)

<!-- Add owner-specific rules here as they accumulate: which social feeds to include, how
     hard to explore, house standards the ± feedback has established. Keep the engine
     contract itself untouched so `npm update` keeps working. -->
