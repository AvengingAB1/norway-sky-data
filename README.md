# norway-sky-data

Public **data feed** for the Sunsetglow app, **North Norway** region (Bodø to Alta,
Lofoten/Vesterålen/Senja/Tromsø/Lyngen). GitHub Actions extract the latest forecasts to
compact JSON and publish them to GitHub Pages:

| File | Source | Cadence |
|---|---|---|
| `meps_latest.json` | MET Norway **MEPS 2.5 km** (HARMONIE-AROME) low/mid/high cloud + visibility (fog layer, `vis`), read numerically from thredds.met.no (OPeNDAP), resampled to 0.03° × 0.075° (~3.3 × 3.0 km), 5 % steps, +66 h, plus ~30 h of past hours carried forward | every MEPS run (3-hourly), hourly probe |
| `elements_latest.json` | MEPS 10 m wind + hourly precipitation, rendered as map overlays | with each MEPS run |
| `stations.json` | MET Norway **Locationforecast 2.0** point forecasts for ~30 photo spots/towns, ~10 days | with each MEPS run |
| `meteo_latest.json` | **Open-Meteo** best_match (= ECMWF IFS 9 km) cloud layers + visibility (fog), 14 days, 0.20° × 0.40° (2419 points) | 2×/day after ECMWF 00Z/12Z |

Same JSON schemas as `iceland-sky-data` (cloud grid adds `div`: stored value / div = cloud fraction).

Region box (edit `DEFAULT_BOX` in `extract/extract_meps.py` and `BOX` in
`extract/extract_meps_elements.py` / `extract/extract_meteo.py` to change it):
cloud grid 65.9–71.1 N, 8.1–24.45 E; Open-Meteo grid 64.6–72.5 N, 4.8–28 E.

Data © MET Norway (NLOD 2.0 / CC BY 4.0) and Open-Meteo (CC BY 4.0).

## Setup (once)
1. Create this repo as **public** on GitHub (Actions minutes are free on public repos).
2. Upload `extract/` and `.github/workflows/` (web UI: Add file → Upload files).
3. Settings → Pages → Source: **GitHub Actions**.
4. Actions → run **MEPS …** then **Open-Meteo …** once by hand (workflow_dispatch).
5. Check `https://avengingab1.github.io/norway-sky-data/meps_latest.json`.
