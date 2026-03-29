# 🏠 Access to Housing

**PropTech intelligence platform for real estate professionals, investors, and researchers — market analysis, climate risk scoring, and Fair Housing-safe tooling.**

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg?style=flat-square)](LICENSE)
[![Fair Housing](https://img.shields.io/badge/Fair_Housing-Compliant-green.svg?style=flat-square)](#fair-housing-compliance)
[![Part of](https://img.shields.io/badge/Part_of-CoTrackPro_Access_Projects-purple.svg?style=flat-square)](https://github.com/CoTrackPro)

---

## The Problem

Housing decisions are some of the highest-stakes financial choices people make, yet the data that drives them is fragmented across dozens of systems — MLS, tax records, climate models, permit databases, and demographic forecasts.

Real estate professionals, first-time homebuyers, housing advocates, and community planners need intelligence tools that are comprehensive, compliant with Fair Housing regulations, and accessible without enterprise-level budgets.

## What This Project Does

Access to Housing is an open-source PropTech intelligence skill built as a [Claude Custom Skill](https://docs.claude.com). It provides structured analytical frameworks across **7 core modules** and **6 reference pods** (74 total modules) — covering everything from satellite development detection to climate migration modeling.

Every module is **Fair Housing-safe by default** — no protected-class proxies in scoring, no discriminatory pattern generation.

## Core Modules

| # | Module | Use When You Need To... |
|---|--------|------------------------|
| 1 | **Satellite Housing Detection** | Identify construction activity before it shows up in MLS or permits |
| 2 | **Construction Permit Intelligence** | Analyze the development pipeline and anticipate supply changes |
| 3 | **Global Housing Supply Forecast** | Project 12–36 month supply scenarios (bear/base/bull) |
| 4 | **Neighborhood Livability Score** | Compare neighborhoods using objective, Fair Housing-compliant metrics |
| 5 | **Infrastructure Growth Heatmap** | Find where infrastructure investment signals future appreciation |
| 6 | **Climate Migration Housing Model** | Understand climate-driven population flows and insurance risk |
| 7 | **Global Property Opportunity Scanner** | Score and rank investment opportunities across markets |

## Reference Pods (74 Modules)

| Pod | Coverage |
|-----|----------|
| **Market Intelligence** | Pricing trends, absorption rates, inventory analysis, demographic forecasting |
| **Investment & Deal** | Cap rates, NOI modeling, underwriting frameworks, syndication, REIT analysis |
| **Risk & Climate** | Flood, fire, heat, hurricane risk scoring; insurance market health; resilience planning |
| **Property Intelligence** | AVM/pricing, MLS analytics, parcel data, zoning, construction quality |
| **Brokerage Ops** | CRM health, lead generation, transaction management, recruiting |
| **Brokerage Strategy** | Market positioning, growth planning, M&A, technology adoption |

## Quick Start

### As a Claude Custom Skill

1. Download the `.skill` file from [Releases](https://github.com/CoTrackPro/access-to-housing/releases)
2. In Claude.ai, go to **Settings → Custom Skills**
3. Upload the skill file
4. Start with prompts like:
   - *"Run a neighborhood livability score for Clayton, MO"*
   - *"What's the permit pipeline in north St. Louis County?"*
   - *"Score Denver vs. Nashville as investment markets"*
   - *"Climate migration risk assessment for coastal Florida"*

### As a Reference Library

The `references/` directory contains structured analytical frameworks organized by pod. Each pod file includes scoring rubrics, data source recommendations, output templates, and methodology notes you can use independently of Claude.

## Repository Structure

```
access-to-housing/
├── README.md                   # This file
├── SKILL.md                    # Claude skill definition (main prompt)
├── LICENSE                     # MIT
├── CONTRIBUTING.md             # How to contribute
├── FAIR-HOUSING.md             # Fair Housing compliance documentation
├── assets/
│   └── data-sources.md         # Primary data sources reference with links
├── references/
│   ├── market-intelligence/    # Pricing, supply, demand, demographics
│   │   └── pod.md
│   ├── investment-deal/        # Cap rates, NOI, underwriting, syndication
│   │   └── pod.md
│   ├── risk-climate/           # Climate risk, insurance, resilience
│   │   └── pod.md
│   ├── property-intelligence/  # AVM, MLS, zoning, construction
│   │   └── pod.md
│   ├── brokerage-ops/          # CRM, leads, transactions, recruiting
│   │   └── pod.md
│   └── brokerage-strategy/     # Positioning, growth, M&A, tech
│       └── pod.md
└── .github/
    └── ISSUE_TEMPLATE/
        ├── module-request.md   # Request a new module
        └── data-source.md      # Suggest a data source
```

## Data Sources

All analyses reference primary, verifiable data sources with vintage dates. Key sources include:

- **Supply & Permits**: U.S. Census Building Permits Survey, NAHB HMI, CoStar, Dodge Construction Network
- **Pricing & Transactions**: Zillow Research, Redfin Data Center, NAR, FHFA HPI, Harvard JCHS
- **Migration & Demographics**: IRS SOI migration data, Census ACS, Redfin migration search data
- **Climate & Risk**: First Street Foundation, FEMA FIRM, NOAA Sea Level Rise Viewer, CAL FIRE WUI maps
- **Infrastructure**: MPO TIPs, FTA Capital Investment Grant tracker, USDOT RAISE grants
- **Livability**: Walk Score, Trust for Public Land ParkScore, FBI UCR/NIBRS

See [`assets/data-sources.md`](assets/data-sources.md) for the full reference with links.

## Fair Housing Compliance

Every module in this project is designed to comply with the Fair Housing Act. Analysis is based exclusively on objective infrastructure, supply/demand, and environmental metrics — never on race, color, national origin, religion, sex, familial status, disability, or proxy characteristics.

See [`FAIR-HOUSING.md`](FAIR-HOUSING.md) for the full compliance framework and checklist.

## Part of the CoTrackPro Access Projects

This repository is part of [CoTrackPro's](https://github.com/CoTrackPro) five-pillar open-source initiative:

| Pillar | Repository | Focus |
|--------|-----------|-------|
| ⚖️ Justice | [access-to](https://github.com/CoTrackPro/access-to) | Family law documentation, expungement, protection orders |
| 📚 Education | [access-to-education](https://github.com/CoTrackPro/access-to-education) | K-12 standards, IEP/504 support, educator tools |
| **🏠 Housing** | **access-to-housing** | **PropTech intelligence, Fair Housing-safe analysis** |
| 🤝 Services | [access-to-services](https://github.com/CoTrackPro/access-to-services) | Legal aid, mental health, advocacy resource navigation |
| ☮️ Peace | *coming soon* | De-escalation, communication, conflict resolution |

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines. We especially welcome:

- New data source integrations
- Module expansions for underserved markets
- Fair Housing compliance review
- Accessibility and plain-language improvements

## License

[MIT](LICENSE) — open source, use freely, attribute kindly.

## Contact

**Doug Devitre** — Founder, [CoTrackPro](https://cotrackpro.com)
- [LinkedIn](https://linkedin.com/in/dougdevitre)
- [GitHub](https://github.com/dougdevitre)

---

> *Housing intelligence should be accessible to everyone — not just those who can afford enterprise subscriptions.*
