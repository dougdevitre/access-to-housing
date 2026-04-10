---
layout: default
title: Example Prompts
parent: Resources
nav_order: 4
description: "Test prompts for every module with expected output structure and validation checklist."
---

# Example Prompts & Test Cases

Use these prompts to test module outputs, verify scoring frameworks, and validate
integration pipelines. Each prompt includes the expected module trigger, output structure,
and key fields to verify.

---

## Core Modules

### Module 1: Satellite Housing Detection

**Prompt**: *"Are there any new construction sites in north St. Louis County that haven't shown up in permits yet?"*

**Expected output fields**:
- Activity Level (High/Medium/Low/Dormant)
- Estimated New Units (range with confidence)
- Primary Types (SFR/MF/Mixed/ADU)
- Key Sites table (site, stage, est. units, type, flags)

**Verification**: Output should NOT reference demographics. Activity tiers should be based on sites per square mile.

---

### Module 2: Construction Permit Intelligence

**Prompt**: *"What's the permit pipeline in Austin, TX? How many units are coming to market in the next 12–24 months?"*

**Expected output fields**:
- Filing Trend (Accelerating/Stable/Declining/Volatile)
- Total Pipeline (units with confidence)
- Breakdown by type (SFR, MF 2–4, MF 5+, ADU, Mixed)
- Top Growth Zones
- Expected Deliveries (12mo, 24mo)

**Verification**: Completion lag estimates should be SFR 7–12mo, Small MF 12–18mo, Large MF 18–36mo.

---

### Module 3: Global Housing Supply Forecast

**Prompt**: *"12-month housing supply forecast for Denver metro — give me bear, base, and bull scenarios."*

**Expected output fields**:
- Three scenarios (Bear/Base/Bull) with unit projections at 12mo, 24mo, 36mo
- Explicit assumptions per scenario
- Confidence levels
- Monitoring triggers (what would shift from base to bear/bull)

**Verification**: Bear should assume financing headwinds. Bull should assume zoning reform + capital availability.

---

### Module 4: Neighborhood Livability Score

**Prompt**: *"Run a neighborhood livability score for Clayton, MO. Compare it to Maplewood and University City."*

**Expected output fields** (matches `NeighborhoodLivabilityScore` schema):
- Overall Score (0–100)
- Tier (Excellent/Good/Fair/Below Average)
- Four dimension scores (Transit 0–25, Parks 0–25, Safety 0–25, Education 0–25)
- Trend Modifier (+5/±4/-5)
- Comparable neighborhoods with side-by-side scores

**Verification**: Safety should use density-normalized rates, NOT raw counts. Education scored on proximity only, NOT test scores.

---

### Module 5: Infrastructure Growth Heatmap

**Prompt**: *"Where is infrastructure spending signaling future growth in the Nashville metro?"*

**Expected output fields**:
- Heat zone tiers (Top Growth / Emerging / Stable / Declining)
- Project inventory (type, investment amount, timeline, value lift estimate)
- Value lift timeline by infrastructure type

**Verification**: Value lift ranges should be Transit 3–7yr 10–25%, Highway 2–5yr 5–15%, Major employer 1–3yr 5–20%.

---

### Module 6: Climate Migration Housing Model

**Prompt**: *"Climate migration risk assessment for coastal Florida — who's leaving, where are they going?"*

**Expected output fields**:
- Climate Risk Profile (flood/heat/wildfire/wind with H/M/L + trajectory)
- Overall Resilience (Strong/Moderate/At Risk/High Risk)
- Migration Role (Origin/Destination/Neutral)
- Net Migration Trend (with source + vintage)
- Bear/Base/Bull scenarios

**Verification**: Migration analysis should use IRS SOI and Census ACS — never framed in demographic group terms.

---

### Module 7: Global Property Opportunity Scanner

**Prompt**: *"Score Denver vs. Nashville vs. Raleigh as investment markets."*

**Expected output fields** (matches `GlobalPropertyOpportunityScanner` schema):
- Total Score per market (5–25)
- Tier (Top Tier/Emerging/Watch/Avoid)
- Five factor scores (Price-to-Income, Migration, Capital, Infrastructure, Supply/Demand)
- Investment thesis per market
- Primary risk per market

**Verification**: Scoring should be 1–5 per factor, 5–25 total. No demographic factors.

---

## Community Trust Pod

### Civic Transparency Tracker

**Prompt**: *"What zoning and development decisions has the St. Louis County Council made in the past year?"*

**Expected output fields**:
- Decision inventory table (Date, Body, Action, Location, Vote, Public Comments)
- Pattern analysis (geographic clustering, decision direction, participation)
- Comprehensive plan alignment

**Verification**: Beneficiary analysis should focus on "existing residents vs. outside capital" — NOT demographics.

---

### Community-Reported Conditions

**Prompt**: *"What are the top housing complaints in Chicago's South Side based on 311 data?"*

**Expected output fields** (matches `CommunityReportedConditions` schema):
- Condition dashboard (category, complaints/1K HH, trend, response time, resolution rate)
- Top issues ranked
- Response equity assessment

**Verification**: All rates normalized per 1,000 households. No demographic overlays.

---

### Displacement Early Warning

**Prompt**: *"Displacement risk assessment for East Nashville — is investment displacing residents?"*

**Expected output fields** (matches `DisplacementEarlyWarning` schema):
- Risk Score (0–100)
- Tier (Critical/Elevated/Moderate/Low)
- Four dimension scores (Affordability 0–30, Tenure 0–25, Investment 0–25, Policy 0–20)
- Trend (Accelerating/Stable/Decelerating)
- Converging signals with data and sources

**Verification**: Uses economic indicators only. Never analyzes who is displaced by demographic group.

---

### Government Accountability Scorecard

**Prompt**: *"How responsive is code enforcement in Kansas City, MO? Rate their overall government accountability."*

**Expected output fields** (matches `GovernmentAccountabilityScorecard` schema):
- Overall Score (0–100)
- Tier (Responsive/Functional/Needs Improvement/Failing)
- Four dimension scores (Code Enforcement, Permit Processing, Complaint Resolution, Public Accessibility — each 0–25)
- Peer comparison
- Equity check

**Verification**: Equity analysis compares service quality across areas — NOT resident demographics.

---

### Neighborhood Resource Directory

**Prompt**: *"What housing resources are available in the St. Louis metro area? I need legal aid and counseling."*

**Expected output fields**:
- Resource map table (Category, Organization, Contact, Services, Eligibility, Status)
- Coverage assessment (well-served, gaps, wait times)

**Verification**: Should reference HUD Housing Counseling directory, Legal Services Corporation, 211. Status should indicate active/waitlist/full.

---

### Community Engagement Guide

**Prompt**: *"How can I participate in upcoming zoning decisions in my city? I'm in Portland, OR."*

**Expected output fields**:
- Upcoming engagement opportunities table (Date, Body, Topic, How to Participate, Deadline)
- Standing engagement channels (Planning Commission, Council, Neighborhood Associations, Advisory Boards)
- Public records access (portal, timeline, key documents)

**Verification**: Should explain state-specific Open Meetings Act. Written comments should be noted as carrying equal weight to oral testimony.

---

## Multi-Module Combinations

### Full Platform Brief

**Prompt**: *"Full market brief for Boise, ID — all 7 modules."*

**Expected output** (matches `PlatformBrief` schema):
- Bottom Line (1–2 sentences)
- Conviction Level (High/Medium/Low)
- Key Signals Converging (one per module)
- Primary Risk
- Individual module sections below

---

### Investment + Community Impact

**Prompt**: *"I'm looking at investing in East Austin. Run the opportunity scanner AND the displacement early warning."*

**Expected output**: Two module outputs — Opportunity Scanner showing investment thesis, Displacement Early Warning showing community impact. Cross-reference should note where investment opportunity overlaps with displacement risk.

---

### Livability + Conditions

**Prompt**: *"Run a livability score for Bed-Stuy, Brooklyn AND pull the community-reported conditions from 311 data."*

**Expected output**: Livability Score (top-down infrastructure metrics) alongside Community-Reported Conditions (ground-level resident experience). Analysis should note where the two perspectives agree and diverge.

---

## Validation Checklist

After running any prompt, verify:

- [ ] Signal Summary is one sentence, actionable
- [ ] All data points cite source name and vintage
- [ ] Scores are within defined ranges (check schema min/max)
- [ ] No protected class characteristics or proxies appear anywhere
- [ ] Data Caveats section explicitly states what is unknown
- [ ] Next Steps are specific and actionable (not generic)
- [ ] Crime data uses density-normalized rates
- [ ] School references use proximity/access only
- [ ] Neighborhood comparisons use objective infrastructure metrics
