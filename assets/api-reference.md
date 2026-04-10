---
layout: default
title: API Reference
parent: Resources
nav_order: 2
description: "Developer guide to programmatic access for 85+ data sources — endpoints, auth, rate limits."
---

# Data Source API Reference

Developer-focused guide to programmatic access for the 85+ data sources used by Access to Housing.
Organized by authentication type and access tier.

---

## Free, No Auth Required

| Source | Endpoint / Access | Data | Format | Rate Limit |
|--------|------------------|------|--------|------------|
| **Census ACS** | `api.census.gov/data/{year}/acs/acs1` | Demographics, income, rent burden, housing tenure | JSON | 500 req/day (no key), unlimited with free key |
| **Census Building Permits** | `api.census.gov/data/bps` | MSA-level permit counts by type | JSON | Same as above |
| **FHFA HPI** | `fhfa.gov/DataTools/Downloads` | House Price Index by MSA, state, ZIP | CSV/Excel | Bulk download, no API |
| **NOAA SLR Viewer** | `coast.noaa.gov/slr` | Sea level rise projections by scenario | GeoJSON/WMS | Open access |
| **FEMA FIRM** | `msc.fema.gov/portal` | Flood zone maps | GeoJSON/Shapefile | Open access |
| **USDA Food Access** | `ers.usda.gov/data-products/food-access-research-atlas` | Food desert mapping by census tract | CSV/Excel | Bulk download |
| **HUD AFFH** | `huduser.gov/portal/datasets` | Fair Housing assessment data | CSV | Bulk download |
| **National Zoning Atlas** | `zoningatlas.org` | Statewide zoning maps (growing coverage) | GeoJSON | Open access |
| **FBI UCR/NIBRS** | `crime-data-explorer.fr.cloud.gov/api` | Crime rates by jurisdiction | JSON | Open, no key needed |
| **Eviction Lab** | `evictionlab.org/map` | Eviction filing rates by geography | CSV | Bulk download |
| **NLIHC** | `nlihc.org/housing-needs-by-state` | Affordable housing gap analysis | PDF/CSV | Reports, no API |
| **USPS Vacancy** | `huduser.gov/portal/datasets/usps.html` | Address-level vacancy data (aggregated) | CSV | Quarterly bulk download |
| **IRS SOI Migration** | `irs.gov/statistics/soi-tax-stats-migration-data` | County-to-county migration flows | CSV | Annual bulk download |
| **EPA Smart Location** | `epa.gov/smartgrowth/smart-location-mapping` | Walkability, transit, land use by block group | CSV/Shapefile | Bulk download |

---

## Free, API Key Required

| Source | Endpoint | Auth | Data | Format | Rate Limit |
|--------|----------|------|------|--------|------------|
| **Census API** | `api.census.gov` | Free API key via `api.census.gov/data/key_signup.html` | All Census datasets | JSON | Unlimited with key |
| **Walk Score** | `api.walkscore.com/score` | Free API key (limited) | Walk/Transit/Bike scores by lat/lng | JSON/XML | 5,000 req/day (free) |
| **Zillow (ZTRAX)** | `zillowgroup.com/research` | Academic/research application | ZHVI, ZORI, home values | CSV | Bulk download after approval |
| **Redfin Data Center** | `redfin.com/news/data-center` | No key, but structured download | Market metrics, migration search | TSV | Bulk download |
| **HUD Housing Counseling** | `data.hud.gov/Housing_Counselor/` | Free API | HUD-approved counselors by ZIP | JSON/XML | Open access |
| **211 API** | Varies by region | Contact local 211 | Community resource directory | JSON | Varies |

---

## Freemium (Free Tier + Paid)

| Source | Free Tier | Paid Tier | Auth | Data |
|--------|-----------|-----------|------|------|
| **First Street Foundation** | Property-level scores at firststreet.org | API via `riskfactor.com` — enterprise pricing | API key (paid) | Flood/Fire/Heat/Wind Factor (1–10) |
| **Regrid** | Limited parcel lookup | API: `regrid.com/api` — from $49/mo | API key | Parcel data, zoning, ownership |
| **BuildZoom** | Free search | Bulk data licensing | Contact sales | Local permit aggregation |
| **Attom Data** | Limited property lookup | API: `api.gateway.attomdata.com` — from $250/mo | API key + OAuth | Transaction data, AVM, property details |

---

## Paid / Enterprise

| Source | Access | Auth | Data | Typical Cost |
|--------|--------|------|------|:------------:|
| **CoStar** | `costar.com` — enterprise subscription | Account login | Commercial permits, MF pipeline, comps | $$$$ |
| **AirDNA** | `airdna.co/api` | API key | STR occupancy, ADR, RevPAR | From $250/mo |
| **Dodge Construction** | `construction.com` | Account login | Project starts, pipeline | $$$$ |
| **JLL Research** | `jll.com/research` | Gated reports | Capital markets, investment sales | Reports free, data paid |
| **CBRE Research** | `cbre.com/insights` | Gated reports | Cap rates, market stats | Reports free, data paid |
| **CoreLogic** | `corelogic.com` | Enterprise API | AVM, risk analytics, MLS data | $$$$ |
| **Zoneomics** | `zoneomics.com` | API key | Zoning data by parcel | From $99/mo |
| **Mashvisor** | `mashvisor.com` | API key | STR + LTR investment metrics | From $100/mo |

---

## MLS / Brokerage (Access Restricted)

| Source | Access Method | Auth | Notes |
|--------|-------------|------|-------|
| **Local MLS** | RESO Web API via MLS vendor | OAuth 2.0 + MLS membership | Requires active real estate license or IDX agreement |
| **Bridge Interactive** | `api.bridgedataoutput.com` | OAuth 2.0 | Zillow-owned RESO-certified MLS aggregator |
| **Trestle** | `api-prod.corelogic.com/trestle` | OAuth 2.0 | CoreLogic-owned RESO-certified feed |
| **ShowingTime** | Internal API | Account login | Showing analytics, requires brokerage subscription |

---

## Municipal / Civic (Varies by Jurisdiction)

| Source Type | How to Find | Common Formats | Notes |
|-------------|-------------|----------------|-------|
| **311 / Service Requests** | Search `[city] open data portal` or `data.[city].gov` | CSV, JSON, API (Socrata/CKAN) | Most major cities publish via Socrata (`*.data.gov`) |
| **Code Enforcement** | City clerk or building department website | PDF, CSV, sometimes API | FOIA may be required if not on open data portal |
| **Council Minutes** | City clerk website, Legistar, Municode | PDF, HTML | Often searchable via `[city] legistar` |
| **Planning Commission** | Planning department website | PDF agendas, staff reports | Typically posted 72 hrs before meetings |
| **Building Permits** | Building department or open data portal | CSV, API | Many cities publish via Accela or similar platforms |
| **Municipal Budgets** | Finance department website | PDF, Excel | Look for line items: code enforcement, housing, community dev |

### Common Open Data Platforms

| Platform | URL Pattern | API Type | Examples |
|----------|-------------|----------|---------|
| **Socrata** | `data.[city].gov` | SODA API (REST) | Chicago, NYC, San Francisco, Austin |
| **CKAN** | Varies | CKAN API (REST) | Boston, Philadelphia |
| **ArcGIS Hub** | `[city].maps.arcgis.com` | ArcGIS REST API | Many smaller cities |
| **Legistar** | `[city].legistar.com` | Legistar API | Council agendas, minutes, votes |

---

## Integration Patterns

### Pattern 1: Census + Walk Score + First Street (Free Stack)

```
1. Census ACS API → demographics, income, rent burden by tract
2. Walk Score API → walkability by lat/lng
3. First Street (free lookup) → climate risk scores
4. Combine → Neighborhood Livability Score inputs
```

### Pattern 2: Open Data + Eviction Lab (Community Trust Stack)

```
1. City 311 API (Socrata) → complaint data by neighborhood
2. Eviction Lab (bulk CSV) → eviction filing rates
3. Census ACS → rent burden, tenure data
4. HUD Housing Counseling API → local resource directory
5. Combine → Displacement Early Warning + Resource Directory
```

### Pattern 3: Full Investment Analysis Stack

```
1. Census Building Permits API → permit pipeline
2. Zillow Research (bulk CSV) → pricing trends
3. Redfin Data Center (bulk TSV) → market metrics
4. FHFA HPI (bulk CSV) → price index
5. First Street → climate risk
6. Combine → Modules 1-7 Platform Brief
```

---

## Rate Limit Best Practices

- **Cache aggressively**: Most housing data updates monthly or quarterly — no need for real-time calls
- **Use bulk downloads**: For Census, FHFA, IRS, Eviction Lab — download once, process locally
- **Batch API calls**: Walk Score, Census API — batch by geography rather than individual lookups
- **Respect robots.txt**: Municipal sites may not have APIs — scraping requires checking terms of service
- **Store vintages**: Always record when data was fetched — housing data is time-sensitive
