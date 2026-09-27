# cbefs-model-currents-repo

The CBEFS **currents** — a data repository of the oceansensing ocean map system: its own
Pages site, its own schedule, its own gigabyte, holding no code of its own.

**Live since 2026-09-27** — published to Pages and R2, not drawn on the
website's map. `PLAN.md` is the founding plan;
`CLAUDE.md` carries what must not be got wrong and the shared doc doctrine.

## What it publishes

The Chesapeake Bay Environmental Forecasting System's **surface currents**.

| root | quantity |
| --- | --- |
| `cur-cbefs.json` | surface currents, a vector pair (integers at `unitScale` 0.001) |

The hourly frame at or before now, from the SURFACE_VELOCITY file. 1.4 MB
(measured 2026-09-27).

Every root is one regional grid at 0.007 degree (336 x 438, `regional:
true`), `source: Chesapeake Bay Environmental Forecast System (CBEFS),
Virginia Institute of Marine Science` — the citation the data's license asks
for. **A bottom root is s-level 0** (ROMS counts from the seabed up), and its
header carries no depth, as Mercator's `bottomt` does not. The fetcher is the
site's `scripts/fetch-cbefs.py`, shared by the three CBEFS repositories and
scoped here with `--only=`; the workflow runs on `47 */3 * * *` since
2026-09-27, after its first dispatched run published.

These products are published **operationally but not drawn on the website's
map** — the owner's call, 2026-09-27. The map's status line still reports
them when they fall behind, which is how their health stays visible.

## Where the data comes from

**Source, read 2026-09-26/27**: VIMS publishes CBEFS output openly, with no
login, through THREDDS/OPeNDAP at
`https://tds.vims.edu/thredds/catalog/abever/ECB_FORECAST_HR/catalog.xml`,
in daily folders (`AVERAGES/`, `HISTORY/`, `SURFACE_VELOCITY/`, `STATION/`).
The model is ROMS ChesROMS-ECB on a **curvilinear** 336 × 564 grid at about
600 m with 20 terrain-following levels; it runs nightly for one nowcast day
and five forecast days, and each day's files were posted around 12:20 UTC.
The daily-average file carries `temp`, `salt`, `oxygen`, `pH`, `alkalinity`
and `Aragonite` on every level, so the surface and the bottom are the top and
bottom s-levels, fetched by OPeNDAP index subsetting; `SURFACE_VELOCITY`
carries hourly surface currents already on rho points and eastward/northward.
The files' own license: *"These data are freely available for public use.
Please cite the Chesapeake Bay Environmental Forecast System (CBEFS), Virginia
Institute of Marine Science, when using this data."* The citation is carried
in every published header's `source` and in the README.

## How it will run

The orchestrator (the site's private `pipeline/`), the fetchers and the
published-file contract all come from `oceansensing.github.io`, checked out at
run time. This repository will carry `pipeline/products.toml` and its publish
workflow, and nothing else executable. Each run publishes to GitHub Pages and
to Cloudflare R2 from one build. Sibling repositories of the same model:
`cbefs-model-fields-repo` and `cbefs-model-bgc-repo`.

**Which document gets what, and what "update docs" means across all
twenty repositories, is the doctrine block at the top of `CLAUDE.md`** —
the same text in all twenty, held equal by the site's `check:docs`.

## Structure

```
README.md       what this is
CLAUDE.md       what must not be got wrong, and the shared doc doctrine
PLAN.md         the founding plan and running record
DECISIONS.md    dated one-way decisions, D1 onward
```
