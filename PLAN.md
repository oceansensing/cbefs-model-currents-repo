# cbefs-model-currents-repo — the founding plan and running record

The CBEFS **currents**. Created on GitHub by the owner and given its documents on
2026-09-27, the day the owner asked for ECCOFS, CBEFS, Mercator's
biogeochemistry, RTOFS and GFS to be published without the map drawing them.
**Built and rehearsed 2026-09-27; not yet live.**

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

## Open, as founded

*Items 1-3 are the 2026-09-27 entry below.*

1. The fetcher, in the site's `scripts/`, and its self-test.
2. `pipeline/products.toml`, declaring only roots the site's contract
   publishes.
3. The publish workflow, its schedule offset from the siblings', and each
   product's `max_age_hours` measured from when the data really arrives.
4. The secrets only the owner can add: `PIPELINES_SSH_KEY` and the three
   `R2_*` organization secrets.

## 2026-09-27 — built and rehearsed

**Built**: the site's `scripts/fetch-cbefs.py` (standard library plus numpy;
DAP2 binary read by hand) and `scripts/regrid.py`. OPeNDAP subsetting asks
for the surface and bottom levels only, `var[t][0:19:19][...]`: 1.5 MB for
one variable of one day, 1.4 s. The first live run took 1 min 42 s for all
fourteen roots of the three repositories.

**The grid**: 336 x 564, nearly rectilinear at about 0.0068 x 0.0054 degree;
interior holes at 0.007 degree 0.18% (0.22% at 0.008, 0.28% at 0.01), so
0.007, close to the model's own spacing, keeping the tributaries.

**Two physical controls, measured before they were written** (the 09-26
run): bottom salinity median 27.6 against the surface's 25.1 — level 0 is
the bottom, and a frame where it is not is refused; and in the mainstem box
(38.0-38.8 N, 76.45-76.25 W) mean |v| 0.207 against |u| 0.090 m/s over the
run's 145 hours — the tide runs along the channel, so a u/v swap reads 0.43
and is refused. Temperature is NOT a control: in late September the surface
can be the cooler, and was.

**The first live run refused six fields for the model's own extremes**, all
in shallow water: salinity to 49.6 in 242 cells 1-2 m deep in the Virginia
coastal bays (38.0 N 75.3 W), pH to 10.75 and aragonite saturation to 12.4
in about twenty cells 2-4 m deep near Back River (39.26 N 76.45 W). The
bounds were widened to publish them and a median band per field guards the
wrong-variable fault. Spot values that run: mid-Bay surface salinity 12.6
over 19.7 at the bottom, bottom oxygen 184 against 242 at the surface, upper
Bay bottom aragonite saturation 0.50 (corrosive), shelf salinity 32.4.

**Rehearsed through the orchestrator** in a throwaway copy of the site with
the roots in its contract: every file matched, every fate `fresh`.

## Open

1. **Went live 2026-09-27** — the entry below.
2. **Re-measure `max_age_hours`** after a week of scheduled runs.
3. The owner is writing to the CBEFS group (Marjorie Friedrichs's lab) about
   the automated daily reads and the citation.

## 2026-09-27 — live

The owner added the secrets; the site's commit `d978a1b` put this
repository's roots in the contract and its origin in `MAP_ORIGINS`; the
dispatched run 36296058765 went green on its first try — build, Pages and R2 — and
`status/status.json` read, at 2026-09-27T05:04:25Z: every product `fresh`
(1 of 1), the nearest frame 0.07 h from the
reader, `contract: 1`. Each root was fetched from Pages
and served. The schedule, `47 */3 * * *`, was then uncommented (longest gap
3 h, so the watchdog's silence budget is 5.5 h); the
first scheduled run is the next reading.
