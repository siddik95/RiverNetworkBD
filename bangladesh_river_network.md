# River Network of Bangladesh — Strahler Order Map

Visualises the full drainage hierarchy of Bangladesh using HydroRivers stream data
clipped to the national boundary, symbolised by Strahler order (1–9).

![River Network of Bangladesh](river_bd.tif)

---

## Data Sources

| Dataset | Source | Purpose |
|---------|--------|---------|
| HydroRivers | [HydroSHEDS](https://www.hydrosheds.org/) | Global river network with Strahler order attribute |
| Bangladesh boundary | GADM / BBS / local authority | Clip extent and country outline |

---

## Processing Pipeline

```
HydroRivers (global)          Bangladesh boundary
        │                             │
        ▼                             │
  Clip to extent  ◄────────────────── ┘
        │
        ▼
  Filter / select by country
        │
        ▼
  Symbolise by Strahler order (1–9)
        │
        ▼
  Cartographic styling
        │
        ▼
  Export map
```

---

## Steps

| # | Operation | Tool / Method | Key detail |
|---|-----------|---------------|------------|
| 1 | **Load HydroRivers** | Add Data | Global polyline dataset — includes `ORD_STRA` field (Strahler order 1–9) |
| 2 | **Load boundary** | Add Data | Bangladesh admin boundary polygon |
| 3 | **Clip river network** | `Clip` (Analysis Tools) | Clip HydroRivers to Bangladesh boundary extent |
| 4 | **Filter by country** | Definition Query or `Select by Attribute` | Retain only features within Bangladesh (`MAIN_BAS` or spatial selection) |
| 5 | **Symbolise by order** | Symbology → Unique Values | Field: `ORD_STRA` · 9 classes · colour ramp light → bold teal |
| 6 | **Style line weights** | Symbol layer sizing | Higher order = thicker line (order 1 ≈ 0.1 pt → order 9 ≈ 2.0 pt) |
| 7 | **Set background** | Map properties | Dark grey canvas (`#666666`) to contrast teal network |
| 8 | **Add map elements** | Insert menu | North arrow · scale bar (1 cm = 29 km) · legend · credits text |
| 9 | **Export** | Export Map / Layout | PNG at 300 dpi |

---

## Symbology Reference

| Strahler order | Meaning | Line weight (approx) |
|:--------------:|---------|----------------------|
| 1 | Headwater / smallest tributary | 0.1 pt |
| 2–3 | Small streams | 0.2 – 0.4 pt |
| 4–6 | Tributaries | 0.5 – 0.8 pt |
| 7–8 | Major rivers (e.g. Meghna, Jamuna) | 1.0 – 1.5 pt |
| 9 | Largest trunk channels | 2.0 pt |

Colour: single teal ramp (`#00CED1` family) — lighter/thinner for low orders, bold for high orders — against a `#666666` background.

---

## Requirements

- ArcGIS Pro 2.x or later
- HydroRivers shapefile (free download from HydroSHEDS)
- Bangladesh administrative boundary (any authoritative source)

---

## Files

| File | Description |
|------|-------------|
| `HydroRIVERS_v10_as.shp` | Source HydroRivers — Asia extent |
| `bangladesh_boundary.shp` | National boundary used for clip |
| `bangladesh_rivers_clipped.shp` | Clipped river network output |
| `river_network_bangladesh.png` | Final exported map |
