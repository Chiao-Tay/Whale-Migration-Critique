# Data notes: whale migration page

## Sources
| Source | Used for | Version |
|---|---|---|
| Atlas of Living Australia (ALA), occurrence records for baleen whales (Mysticeti), "ALA General" quality profile | Charts 1–3, 5–12 | Downloaded 13 Oct 2026, DOI https://doi.org/10.26197/ala.df33528c-b498-46ab-ad3d-027674a40fe1 |
| DCCEEW, Biologically Important Areas for protected marine species | Chart 4 (`whale-bias.json`) | Consolidated dataset, Dec 2025 update |
| Natural Earth, Admin 1 states and provinces (1:10m) | Base map (`australia-states.json`) | Public domain |

## Cleaning rules (raw ALA file: 68,074 records)
- Kept only records inside Australian waters (latitude −45 to −9, longitude 110 to 156).
- Removed historical whaling catches (1925–1963). These are kept separately, for chart 8 only.
- Kept only records with a month and an identified species.
- Main window: **2016–2025**, the last 10 full years, 14,019 records. 2026 is excluded because it is a partial year.
- Exceptions: chart 8 uses 1925–1963 whaling catches (23,057 records). Chart 10 uses 2000–2025.

## Files
| File | Chart | Notes |
|---|---|---|
| `c1_species_by_month.csv` | 1. Radial calendar | Humpback, southern right, blue. `share_pct` = % of that species' records in each month. Blue whale has only 150 records. |
| `c2_species_totals.csv` | 2. Who we see most | All species, 2016–2025 |
| `c3_species_by_state.csv` | 3. Choropleth | Offshore records assigned to the nearest state's coast. Join on `state` = `name` in `australia-states.json`. |
| `whale-bias.json` | 4. BIA map | TopoJSON, feature `whale_bias`. Fields: `COMMON_NAME`, `BEHAVIOUR_CAT`, `SEASON` (free text, some blank). Simplified to ~1 km tolerance. |
| `c5_grid_by_period.csv` | 5. Gridded map | 1° cells (cell centre), six two-month periods |
| `c6_humpback_lat_month.csv` | 6. Heatmap | Humpbacks only. 1° latitude bands; east coast (lon ≥ 148) and west coast (lon ≤ 123). Bands with fewer than 30 records dropped. |
| `c7_eastcoast_site_month.csv` | 7. Ridgeline | Humpbacks at 7 east-coast sites, ordered south to north. `share_pct` = % of that site's records. |
| `c8_whaling_catches.csv` | 8. The Hunt | Humpback catches per year, west vs east coast |
| `c9_sources_waffle.csv` | 9. Waffle | 100 squares (10×10). Each square = 1% of 2016–2025 records. |
| `c10_sources_by_year.csv` | 10. Stacked area | Records per year by source type, 2000–2025 |
| `c11_hotspots.csv` | 11. Proportional symbols | 0.5° cells with 20+ records. `top_species` = most-reported species. |
| `c12_planner.csv` | 12. Planner | Site × species with 50+ records. Window = months holding the middle 80% of records. |

## Source categories (charts 9–10)
- **Citizen science apps:** iNaturalist, Happywhale, NatureMapr, ClimateWatch, Earth Guardians, Observation.org, ALA sightings, Entangled Wildlife Australia
- **Government wildlife atlases:** Victorian Biodiversity Atlas, NSW BioNet, SA Fauna, WildNet (QLD), NT Fauna Atlas, National Whale and Dolphin Sightings and Strandings Database. These include many reports from the public.
- **Museum collections:** OZCAM museums, Smithsonian (NMNH)
- **Scientific surveys:** everything else (research voyages, aerial surveys)

## Caveats to state on the page
- These are **reports, not population counts.** More people looking means more records.
- 2016–2025 blue whale records peak in May–June, when they pass Western Australia. Earlier summer surveys showed a different peak, so the season you see depends on where people looked.
- Sydney has two humpback peaks: June–July (heading north) and September–October (heading south).
