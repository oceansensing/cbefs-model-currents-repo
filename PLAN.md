# cbefs-model-currents-repo — the founding plan and running record

The CBEFS **currents**. Created on GitHub by the owner and given its documents on
2026-09-27, the day the owner asked for ECCOFS, CBEFS, Mercator's
biogeochemistry, RTOFS and GFS to be published without the map drawing them.
**Nothing is published yet.**

## What it is for

The Chesapeake Bay Environmental Forecasting System's **surface currents**.

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

## Open

1. The fetcher, in the site's `scripts/`, and its self-test.
2. `pipeline/products.toml`, declaring only roots the site's contract
   publishes.
3. The publish workflow, its schedule offset from the siblings', and each
   product's `max_age_hours` measured from when the data really arrives.
4. The secrets only the owner can add: `PIPELINES_SSH_KEY` and the three
   `R2_*` organization secrets.
