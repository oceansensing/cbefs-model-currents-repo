# cbefs-model-currents-repo

The CBEFS **currents** — a data repository of the oceansensing ocean map system: its own
Pages site, its own schedule, its own gigabyte, holding no code of its own.

**Nothing is published yet** (2026-09-27). `PLAN.md` is the founding plan;
`CLAUDE.md` carries what must not be got wrong and the shared doc doctrine.

## What it will publish

The Chesapeake Bay Environmental Forecasting System's **surface currents**.

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
seventeen repositories, is the doctrine block at the top of `CLAUDE.md`** —
the same text in all seventeen, held equal by the site's `check:docs`.

## Structure

```
README.md       what this is
CLAUDE.md       what must not be got wrong, and the shared doc doctrine
PLAN.md         the founding plan and running record
DECISIONS.md    dated one-way decisions, D1 onward
```
