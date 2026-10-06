# Critical Infrastructures and Accessibility Analysis under Flood Conditions

**RisCon26 · Karlstad, Sweden · 8 October 2026**

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/sesac-sweden/riscon26-workshop/blob/main/RisCon26_SESAC_workshop.ipynb)
![License](https://img.shields.io/badge/code-MIT-blue)

A hands-on geospatial workshop exploring how flooding can disrupt road networks and access to critical services in Karlstad.

The workshop asks a practical question:

> **If Karlstad floods, who can still reach a hospital, a fire station or a school in time, and who cannot?**

Participants work with official flood-depth scenarios, road-network data, critical facilities, population and land-cover information to examine how accessibility changes as flood severity increases.

The workshop was developed by **SESAC — the Swedish Competence Centre for Satellite-Enabled Social Science Analytics** — for **RisCon26: Societal Risk Conference 2026**.

**Workshop facilitator:** Amalia Chantziara

---

## The case study

Karlstad sits on the delta where the Klarälven river meets Lake Vänern, making flooding an important local planning and resilience question.

Sweden's Civil Contingencies Agency (**MSB**) provides modelled flood-depth scenarios showing how deep the water could become, and where, under floods of different magnitudes.

Unlike an event-based analysis that asks *“what happened during a particular flood?”*, this workshop uses scenarios to ask:

> **What could happen under floods of different severities?**

Participants compare three flood scenarios:

| Scenario | File | Approximate annual exceedance probability |
|---|---|---:|
| 50-year flood | `Karlstad_50_djup.tif` | ~2% |
| 100-year flood | `Karlstad_100_djup.tif` | ~1% |
| 200-year flood | `Karlstad_200_djup.tif` | ~0.5% |

*`djup` = depth, in metres.*

---

## What the notebook does

The practical exercise follows a complete analytical workflow:

1. **Flood scenarios**  
   Loads the three MSB flood-depth rasters and compares how flood extent and depth change between scenarios.

2. **Roads and critical services**  
   Loads the road network and three categories of critical facilities — hospitals, fire stations and schools — prepared from OpenStreetMap.

3. **Depth-dependent road disruption**  
   Evaluates every road segment according to the modelled flood depth affecting it, following the depth–disruption relationship described by Pregnolato et al. (2017):

   - **≥ 0.30 m** → impassable
   - **0.10–0.30 m** → passable at reduced speed
   - **< 0.10 m** → normal

4. **Accessibility analysis**  
   Computes **5-, 10- and 15-minute drive-time isochrones** around critical facilities under normal conditions and under each flood scenario.

5. **Who is affected?**  
   Combines the accessibility results with population information from Statistics Sweden (SCB) and NMD2018 land-cover data to examine where loss of accessibility may have the greatest societal impact.

The analytical chain can be summarised as:

**Flood scenarios → road disruption → critical infrastructure → accessibility analysis → exposure and interpretation**

No previous programming experience is required. The notebook contains pre-written code cells that participants can run sequentially while focusing on understanding the workflow and interpreting the results.

---

## Workshop materials

This repository contains the materials used for the SESAC RisCon26 workshop:

| File | Description |
|---|---|
| `RisCon26_SESAC_workshop.ipynb` | Google Colab/Jupyter notebook used for the practical exercise |
| `RISCON26_SESACWorkshop.pdf` | Workshop presentation |
| `Karlstad_50_djup.tif` | MSB flood-depth raster — 50-year scenario |
| `Karlstad_100_djup.tif` | MSB flood-depth raster — 100-year scenario |
| `Karlstad_200_djup.tif` | MSB flood-depth raster — 200-year scenario |
| `Karlstad_nmd2018.tif` | NMD2018 land-cover raster, clipped to the Karlstad study area |
| `SCB_population_Karlstad_5km.gpkg` | SCB population data, clipped to the study area |
| `karlstad_drive.graphml` | Drivable road network represented as a routing graph |
| `karlstad_osm.gpkg` | Road-network geometries used for mapping and flood intersection |
| `karlstad_pois.gpkg` | Critical facilities: hospitals, fire stations and schools |
| `LICENSE` | MIT licence covering the workshop code |

---

## Data sources

| Data | Source |
|---|---|
| Flood-depth scenarios | Myndigheten för samhällsskydd och beredskap (MSB) |
| Road network | OpenStreetMap |
| Critical facilities | OpenStreetMap |
| Population | Statistics Sweden (SCB) |
| Land cover | NMD2018, Naturvårdsverket |

The OpenStreetMap layers included here are **pre-fetched snapshots**. This ensures that the workshop produces consistent results and does not depend on live OpenStreetMap services during the exercise.

Because OpenStreetMap is continuously updated, a new download performed today may differ slightly from the versions included in this repository.

---

## How to run the exercise

1. Click the **Open in Colab** badge at the top of this page.

2. Sign in with a Google account if required.

3. Run the notebook cells sequentially from top to bottom.

4. The required workshop datasets are downloaded automatically from this repository when the notebook runs.

5. Follow the explanations and interpretation prompts provided throughout the notebook.

Everything runs in the browser, so no local Python installation is required.

---

## What this method can — and cannot — tell us

Because the flood input contains **water depth**, rather than only a binary flooded/not-flooded classification, the analysis can distinguish between roads that may remain passable at reduced speed and roads that are considered impassable.

This provides a more realistic representation of how flooding may affect transport accessibility.

However, the analysis remains a simplified scenario.

The flood layers are **modelled hazard scenarios**, not observations of an actual flood event. The road-disruption thresholds are general values derived from the literature rather than vehicle-specific thresholds for Swedish emergency services.

Travel times also assume simplified traffic conditions and do not account for factors such as:

- Congestion
- Temporary barriers
- Emergency traffic management
- Local detours
- Evacuation routes
- Real-time road closures

The results should therefore be interpreted as a way to identify **where accessibility may be particularly vulnerable under flood conditions**, rather than as an operational emergency forecast.

---

## Related SESAC workshop

For an event-based version of a similar workflow, see the SESAC **Beginner Earth Observation Analysis Series 2026** exercise:

### From Flood Mapping to Critical Infrastructure Accessibility

[View the workshop materials](https://github.com/sesac-sweden/beginner-eo-analysis-series-2026/tree/main/day-2/02-flood-accessibility-workshop)

That exercise uses **Sentinel-1 radar observations of the February 2020 floods in the Viskan valley (Borås–Skene)** rather than modelled flood scenarios.

Together, the two exercises demonstrate two complementary approaches:

- **Observed flood event:** satellite-based flood detection using Sentinel-1
- **Modelled flood scenarios:** depth-based accessibility analysis using MSB flood maps

---

## Data and licensing

The workshop combines datasets from several external providers. Their original licences and terms of use continue to apply.

- **Flood-depth scenarios** — Myndigheten för samhällsskydd och beredskap (MSB), flood mapping data
- **Roads and critical facilities** — © [OpenStreetMap](https://www.openstreetmap.org/copyright) contributors, ODbL
- **Population data** — Statistics Sweden (SCB)
- **Land cover (NMD2018)** — Naturvårdsverket, CC0
- **Depth–disruption function** — Pregnolato, M., Ford, A., Wilkinson, S. M., & Dawson, R. J. (2017). *The impact of flooding on road transport: A depth-disruption function*. Transportation Research Part D, 55, 67–81.

The **code associated with this workshop is shared under the MIT License**. External datasets retain their respective original licences and terms of use.

---

## Author and acknowledgements

Workshop materials and notebook developed by:

**Amalia Chantziara**  
SESAC Project Assistant

The workshop was developed for **RisCon26: Societal Risk Conference 2026** in Karlstad.

SESAC — the **Swedish Competence Centre for Satellite-Enabled Social Science Analytics** — connects Earth Observation, social science and AI through research, training, open workflows and co-creation.

SESAC is funded by the **Swedish National Space Agency (Rymdstyrelsen)**.

🌐 [sesac.se](https://sesac.se)  
💼 [LinkedIn](https://www.linkedin.com/company/sesac-sweden)  
▶️ [YouTube](https://www.youtube.com/@SESACSweden)

---

*If you use or adapt this notebook, a link back to the SESAC repository is appreciated.*
