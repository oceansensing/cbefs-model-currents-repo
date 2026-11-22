# Decisions

Dated, irreversible-leaning decisions, one entry each, newest last. The
reasoning lives in `PLAN.md`.

**What counts as one-way in a data repository**: a decision that puts bytes in
readers' hands under a shape they will code against; a decision about which
repository owns a product, since moving one costs a migration in two places;
and a decision that forecloses an upstream.

## D1 — 2026-09-27 — Its own repository, published but not drawn

The CBEFS **currents**, in a repository of its own under the convention every model
follows: **a model splits along the axis that costs bytes** — currents,
fields and, where the model has them, biogeochemistry — and an atmospheric
model has one atmosphere repository. See `espc-model-repo`'s `DECISIONS.md`
D2 for the measurement behind the split.

**Published but not drawn** (the owner, 2026-09-27): the products go to Pages
and R2 on a schedule and the website's map carries no layer for them, while
its status line reports their health. Drawing one later is a change to the
map, not to this repository.

One-way in the ordinary data-repository sense: moving a product between
repositories is cheap in machinery and expensive in everything that points at
it — roots in the contract, origins in the site's config, and the union
`check:docs` holds across origins.

## D2 — 2026-09-27 — OPeNDAP subsets of the daily files, surface and bottom, 0.007 degree

**Source: VIMS's THREDDS at tds.vims.edu, by OPeNDAP**, asking for the top
and bottom s-levels only; the daily files are 2.75-12 GB and whole-file
reads are not possible on Actions. A mirror exists on the MARACOOS/RPS EDS
server and is not used: it posts later and skipped a day in the week
surveyed.

**Shape: one regional grid per root at 0.007 degree, `regional: true`**, no
tiles; bottom roots named for the bottom and carrying no depth. **Published,
not drawn** (the owner, 2026-09-27).

## D3 — 2026-11-21 — Two days ahead and one behind, `frames` kept as it was, R2 keeping what a base lists

**The window is 48 hours ahead and 24 behind**, said in
`pipeline/products.toml` (`hours_ahead`, `hours_behind`; the site pipeline's
D16, the owner's call of 2026-11-21).
**The surface current hourly, the whole-column mean and the bottom current
six-hourly, the current at depth by its daily means.** `frames` keeps exactly
what it listed before: the first three's day either side, none for the
current at depth.
Every time past that is in `moreFrames`, a list of its own; a reader taking
both lists has every time once.

**The dated files are R2's alone, kept while a base lists them**
(`memory = "r2-kept"`): they leave Pages and the `published` branch, and what
a run has published is read from its last base's listing, so VIMS is asked
for the base and the times its run had not given. The time behind is never
fetched: it is what earlier runs published, so a daily mean's fills in from
the first day after this lands.

**The branch moves only after R2 has the files it lists** (the workflow's
`remember` job): pushed beside a failed R2 publish it would name files R2
never received, and none would be made again before the model's next run. A
run that does not deploy leaves the branch where it was.

**A time added never holds what was there.** A run too short, a failed check
or a server not answering leaves out that time and those after it, said as a
warning, and times added are asked for in a run's first ten minutes alone, so
a slow server cannot take the step past its thirty minutes.

**Measured in rehearsal, nothing published.**
The first run from the branch of 2026-11-21 read 301.0 MB from VIMS in 15
requests, 142 seconds end to end: 320 files matching the contract, 150 dated
files left off the branch, 178 objects for R2 (234.3 MB), none a base lists
left out. 61 dated files of the first three leave Pages for R2 alone.

One-way in the ordinary sense: `moreFrames` is a shape readers will code
against, and `frames` stays as it was because readers already do.
