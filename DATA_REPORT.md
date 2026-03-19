# GCAT Data Report — Jonathan's Space Archives

**Generated:** 2026-03-19  
**Source:** Jonathan McDowell's GCAT v1.8.0 (planet4589.org)  
**Data as of:** 2026-03-17

---

## Summary of Downloaded Datasets

| File | Size | Data Rows | Columns | Description |
|------|------|-----------|---------|-------------|
| `launchlog.tsv` | 4.4 MB | 29,193 | 20 | Master orbital launch log (1957–2026) |
| `active.tsv` | 1.7 MB | 15,050 | 16 | Currently active satellites |
| `geotab.tsv` | 316 KB | 1,939 | 19 | Geostationary satellite log |
| `satcat.tsv` | 18 MB | 68,260 | 42 | Full satellite catalog (all time) |
| `currentcat.tsv` | 13 MB | 80,257 | 23 | Current objects in orbit (incl. debris) |
| `psatcat.tsv` | 4.5 MB | 26,271 | 28 | Payload satellite catalog |
| `ftocat.tsv` | 492 KB | 1,798 | 42 | Failed-to-orbit catalog |
| `deepcat.tsv` | 328 KB | 1,203 | 42 | Deep space catalog |

---

## Dataset-by-Dataset Analysis

### 1. launchlog.tsv — Master Launch Log

**Columns (20):** Launch_Tag, Launch_Date, Piece, Type, Name, PLName, JCAT, SatOwner, SatState, LV_Type, Flight_ID, Platform, Launch_Site, Launch_Pad, Ascent_Site, Ascent_Pad, Agency, LVState, Launch_Code, LTCite

**Date range:** 1957 Nov 3 → 2026 Mar 17 (69 years of spaceflight history)

**Key statistics:**
- **Launch outcomes:** 27,511 orbital success (OS), 897 orbital failure (OF), 431 deep space (DS)
- **Top launch states:** US (18,587), Soviet Union (4,024), Russia (2,027), China (2,009), France (1,191), India (589), Japan (321), New Zealand (265)
- **Recent launch rate explosion:**
  - 2016: 227 | 2020: 1,291 | 2023: 2,952 | 2025: 4,605 | 2026 YTD: 943
  - The 2020s show ~10-20× growth vs. the 2010s, driven by mega-constellations

**Data quality:** Clean. Well-structured TSV. Comments prefixed with `#`. Dates in human-readable format (not ISO 8601 — will need parsing for analysis).

---

### 2. active.tsv — Currently Active Satellites ⭐

**Columns (16):** JCAT, Piece, Name, LaunchDate, LState, Owner, OwnState, UNState, Mass, Class, Category, TF, Perigee, Apogee, Inc, OpOrbit

**Total active satellites: 15,050**

**Owner distribution (top 10):**
| Owner | Count | Identity |
|-------|-------|----------|
| SPXS | 10,038 | SpaceX (Starlink) |
| ONEWEBN | 523 | OneWeb (Eutelsat) |
| NROC | 260 | Northrop Grumman / US NRO |
| KUIP | 210 | Amazon Kuiper |
| ZXW | 182 | Chinese constellation |
| PLAN | 138 | Chinese military |
| ONEWEB | 109 | OneWeb (legacy code) |
| YUANX | 93 | Yuanxin (Chinese) |
| CGSTL | 85 | Chang Guang Satellite Tech |
| IRIDS | 80 | Iridium |

**Orbit distribution:**
| Orbit | Count | Description |
|-------|-------|-------------|
| LLEO/I | 9,964 | Lower LEO, inclined — Starlink's main orbit |
| LLEO/S | 2,274 | Lower LEO, sun-synchronous |
| LLEO/P | 637 | Lower LEO, polar |
| LEO/I | 453 | LEO, inclined |
| LEO/S | 412 | LEO, sun-synchronous |
| GEO/S | 278 | Geostationary, stationed |
| MEO | 198 | Medium Earth orbit (GNSS) |

**LEO satellites (perigee < 2000 km): 14,178 (94.2% of all active sats)**

**Classification by function:**
- Communications (COM): 12,284 (81.6%)
- Imaging (IMG): 914 (6.1%)
- Technology (TECH): 479 (3.2%)
- Navigation (NAV): 234 (1.6%)
- Signals intelligence (SIG): 201 (1.3%)

**Data quality:** Excellent. Mass column fully populated. Orbital parameters (perigee, apogee, inclination) present for all entries. OpOrbit well-categorized.

---

### 3. satcat.tsv — Full Satellite Catalog

**Columns (42):** JCAT, Satcat, Launch_Tag, Piece, Type, Name, PLName, LDate, Parent, SDate, Primary, DDate, Status, Dest, Owner, State, Manufacturer, Bus, Motor, Mass, MassFlag, DryMass, DryFlag, TotMass, TotFlag, Length, LFlag, Diameter, DFlag, Span, SpanFlag, Shape, ODate, Perigee, PF, Apogee, AF, Inc, IF, OpOrbit, OQUAL, AltNames

**Total entries: 68,260** (all objects ever cataloged as satellites/payloads)

**Date range:** 1957 Oct 4 (Sputnik) → 2026 Mar 17

**Status distribution:**
| Status | Count | Meaning |
|--------|-------|---------|
| R | 32,543 | Re-entered |
| O | 31,205 | In orbit |
| OX | 1,204 | In orbit, extended catalog |
| L | 1,074 | Lost / unknown |
| DK | 468 | Decayed |
| DSO | 460 | Deep space orbit |

**Starlink in full catalog:** 11,864 entries (SPXS owner), including deorbited units.

**Data quality:** Most comprehensive dataset. 42 columns provide deep detail (manufacturer, bus type, physical dimensions, shape). Some fields (DryMass, Motor, Bus) are sparsely populated for older entries, as expected.

---

### 4. geotab.tsv — Geostationary Satellite Log

**Columns (19):** JCAT, Piece, Name, LDate, GDate, ODate, Period, Perigee, PF, Apogee, AF, Inc, IF, OType, Longitude, DriftRate, TDate, TF, Flags

**Total entries: 1,939** (all satellites that have occupied GEO)

**Date range:** 1963 (Syncom 1) → present

**Orbit types present:** GEO/S, GEO/T, GEO/D, GEO/I, MEO (drifted), etc.

**Data quality:** Good. Includes longitude station assignment and drift rates — valuable for GEO coordination analysis.

---

### 5. currentcat.tsv — Current Objects in Orbit

**Columns (23):** JCAT, DeepCat, Satcat, Piece, Active, Type, Name, LDate, Parent, Owner, State, SDate, ExpandedStatus, DDate, ODate, Period, Perigee, PF, Apogee, AF, Inc, IF, OpOrbit

**Total entries: 80,257** — includes debris, rocket bodies, and inactive objects

**Type distribution (top entries):**
| Type Code | Count | Likely meaning |
|-----------|-------|----------------|
| D P | 12,860 | Debris, payload-related |
| P | 8,923 | Payload (active or dead) |
| P O | 8,596 | Payload, operational |
| D W | 6,896 | Debris, fragmentation |
| R3 | 3,212 | Rocket body (3rd stage) |
| D I | 2,608 | Debris, mission-related |
| D B | 2,450 | Debris, breakup |

**Data quality:** Good. Comprehensive view of the full orbital population including space debris — essential for conjunction/collision risk analysis.

---

### 6. psatcat.tsv — Payload Satellite Catalog

**Columns (28):** JCAT, Piece, Name, LDate, TLast, TOp, TDate, TF, Program, Plane, Att, Mvr, Class, Category, Result, Control, Discipline, UNState, UNReg, UNPeriod, UNPerigee, UNApogee, UNInc, DispEpoch, DispPeri, DispApo, DispInc, Comment

**Total entries: 26,271**

**Unique columns vs satcat:** Includes `Program`, `Plane`, `Att` (attitude control), `Mvr` (maneuverability), `Class`, `Category`, `Result`, `Control`, `Discipline` — operational metadata not in satcat.

**Discipline distribution:** Mostly unpopulated (`-`), but when present includes: PL (planetary), ATM (atmospheric), GEOD (geodesy), BIO (biology), M (military), ION (ionospheric), SOL (solar), XRA (X-ray astronomy).

**Data quality:** Sparse in some metadata columns but valuable for the operational characteristics (attitude, maneuverability, program affiliation).

---

### 7. ftocat.tsv — Failed-to-Orbit Catalog

**Columns (42):** Same schema as satcat.tsv

**Total entries: 1,798 launch failures**

**Failures by decade:**
| Decade | Failures |
|--------|----------|
| 1960s | 495 |
| 1970s | 260 |
| 1980s | 243 |
| 1990s | 196 |
| 2000s | 92 |
| 2010s | 179 |
| 2020s | 248 |

Note: 2020s failures increasing in absolute numbers due to massively higher launch cadence, but failure *rate* is lower.

**Data quality:** Same as satcat. Useful for reliability analysis.

---

### 8. deepcat.tsv — Deep Space Catalog

**Columns (42):** Same schema as satcat.tsv

**Total entries: 1,203** (objects beyond Earth orbit)

**Data quality:** Clean. Small dataset. Not relevant to LEO/NTN research.

---

## Cross-Dataset Key Findings

### The Mega-Constellation Era
- **10,038 active Starlink satellites** = 66.7% of all active spacecraft
- **OneWeb:** 632 active (ONEWEBN + ONEWEB codes combined)
- **Kuiper:** 210 active (early deployment phase)
- **94.2%** of all active satellites are in LEO
- **81.6%** of all active satellites are communications satellites
- Launch rate grew from ~200/year (2016) to ~4,600/year (2025) — a **23× increase**

### Orbital Environment
- **80,257 tracked objects** currently in orbit (currentcat)
- Only **15,050 are active** — the rest is debris, dead satellites, rocket bodies
- Active-to-total ratio: **18.8%** (orbital debris dominates)

### 5G NTN-Relevant Constellations Identified in Data
| Constellation | Active Sats | Orbit | Owner Code |
|---------------|-------------|-------|------------|
| Starlink | 10,038 | LLEO/I (~550 km) | SPXS |
| OneWeb | 632 | LLEO/P (~1200 km) | ONEWEBN/ONEWEB |
| Kuiper | 210 | LLEO/I (~590 km) | KUIP |
| Iridium NEXT | 80 | LEO (~780 km) | IRIDS |

---

## Data Quality Summary

| Dataset | Completeness | Date Format | Key Issues |
|---------|-------------|-------------|------------|
| launchlog | ★★★★★ | Non-ISO (`YYYY Mon DD`) | Date parsing needed |
| active | ★★★★★ | Non-ISO | Excellent quality |
| satcat | ★★★★☆ | Non-ISO | Sparse for older entries |
| geotab | ★★★★☆ | Non-ISO | Clean for GEO analysis |
| currentcat | ★★★★★ | Non-ISO | Includes debris context |
| psatcat | ★★★☆☆ | Non-ISO | Many empty metadata fields |
| ftocat | ★★★★☆ | Non-ISO | Same schema as satcat |
| deepcat | ★★★★☆ | Non-ISO | Small, clean |

**Common issues across all files:**
1. **Date format:** `YYYY Mon DD HHMM:SS` — needs custom parser (not ISO 8601)
2. **Comment rows:** Lines starting with `#` must be filtered
3. **Whitespace padding:** Fields are space-padded for alignment — strip on ingest
4. **Owner codes:** Use abbreviations (SPXS, ONEWEBN) — need a lookup table for human-readable names

---

## Recommendations for LEO Satellite / 5G NTN Research

### Tier 1 — Essential (use these)

1. **`active.tsv`** — The single most important dataset. Contains all 15,050 active satellites with orbital parameters, owner, classification, and mass. Filter by `OpOrbit` starting with `LLEO` or `LEO` and `Class=COM` to isolate NTN-relevant constellations.

2. **`launchlog.tsv`** — Essential for temporal analysis: launch cadence trends, deployment timelines for Starlink/OneWeb/Kuiper, future capacity projections.

3. **`satcat.tsv`** — Full lifecycle data including deorbited satellites. Critical for understanding constellation replenishment rates (Starlink has launched ~11,864 but only ~10,038 are active → ~1,826 deorbited/failed).

### Tier 2 — Valuable for Context

4. **`currentcat.tsv`** — Orbital debris context. Important if researching collision risk, spectrum interference, or orbital sustainability for NTN constellations.

5. **`psatcat.tsv`** — Operational characteristics (maneuverability, attitude control, program affiliation). Useful for distinguishing constellation generations and capabilities.

### Tier 3 — Peripheral

6. **`geotab.tsv`** — GEO satellites only. Relevant if comparing LEO NTN vs. GEO broadband (e.g., ViaSat, Hughes).
7. **`ftocat.tsv`** — Launch failure analysis. Useful for reliability/risk assessment.
8. **`deepcat.tsv`** — Not relevant to LEO/NTN research.

### Suggested Research Queries

```
# All active LEO communication satellites
active.tsv WHERE OpOrbit LIKE 'LEO%' OR OpOrbit LIKE 'LLEO%' AND Class = 'COM'

# Starlink deployment timeline
satcat.tsv WHERE Owner = 'SPXS' GROUP BY year(LDate)

# Constellation replenishment rate
satcat.tsv WHERE Owner = 'SPXS' AND Status = 'R' (re-entered Starlinks)

# Launch cadence for NTN constellations
launchlog.tsv WHERE Name LIKE '%Starlink%' OR Name LIKE '%OneWeb%' OR Name LIKE '%Kuiper%'
```

---

