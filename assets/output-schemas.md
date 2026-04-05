# Output Schemas

Machine-readable JSON schema definitions for all scoring and assessment modules.
Use these schemas to parse, validate, and integrate module outputs into applications.

---

## Shared Types

```json
{
  "ConfidenceLevel": "High | Medium | Low",
  "Trend": "Accelerating | Improving | Stable | Declining | Decelerating",
  "TrendArrow": "up | down | flat",
  "DataCaveat": {
    "description": "string",
    "impact": "High | Medium | Low"
  },
  "NextStep": {
    "action": "string",
    "priority": "High | Medium | Low",
    "completed": "boolean"
  },
  "SourceCitation": {
    "name": "string",
    "url": "string | null",
    "vintage": "string",
    "cadence": "string"
  }
}
```

---

## Module 4: Neighborhood Livability Score

```json
{
  "$schema": "https://json-schema.org/draft/2020-12/schema",
  "title": "NeighborhoodLivabilityScore",
  "type": "object",
  "required": ["location", "signalSummary", "overallScore", "tier", "dimensions", "trendModifier"],
  "properties": {
    "location": { "type": "string" },
    "signalSummary": { "type": "string" },
    "overallScore": { "type": "integer", "minimum": 0, "maximum": 100 },
    "tier": { "enum": ["Excellent", "Good", "Fair", "Below Average"] },
    "dimensions": {
      "type": "object",
      "properties": {
        "transitAccess": {
          "type": "object",
          "properties": {
            "score": { "type": "integer", "minimum": 0, "maximum": 25 },
            "walkScore": { "type": "integer", "minimum": 0, "maximum": 100 },
            "transitDistance": { "type": "string" },
            "bikeInfrastructure": { "type": "string" },
            "frequency": { "type": "string" }
          }
        },
        "parksAmenities": {
          "type": "object",
          "properties": {
            "score": { "type": "integer", "minimum": 0, "maximum": 25 },
            "parkAcreagePer1K": { "type": "number" },
            "groceryWithin1Mi": { "type": "boolean" },
            "healthcareWithin1Mi": { "type": "boolean" },
            "libraryWithin1Mi": { "type": "boolean" }
          }
        },
        "safetyIndicators": {
          "type": "object",
          "properties": {
            "score": { "type": "integer", "minimum": 0, "maximum": 25 },
            "propertyCrimeRate": { "type": "number" },
            "violentCrimeRate": { "type": "number" },
            "rateVsCityAvg": { "type": "string" },
            "trend3yr": { "$ref": "#/$defs/TrendArrow" }
          }
        },
        "educationAccess": {
          "type": "object",
          "properties": {
            "score": { "type": "integer", "minimum": 0, "maximum": 25 },
            "schoolsWithin1_5Mi": { "type": "integer" },
            "earlyChildhood": { "type": "boolean" },
            "higherEd": { "type": "boolean" }
          }
        }
      }
    },
    "trendModifier": {
      "type": "object",
      "properties": {
        "direction": { "enum": ["Improving", "Stable", "Declining"] },
        "points": { "type": "integer", "minimum": -5, "maximum": 5 }
      }
    },
    "comparableNeighborhoods": {
      "type": "array",
      "items": {
        "type": "object",
        "properties": {
          "name": { "type": "string" },
          "overallScore": { "type": "integer" },
          "tier": { "type": "string" }
        }
      }
    },
    "dataCaveats": { "type": "array", "items": { "$ref": "#/$defs/DataCaveat" } },
    "nextSteps": { "type": "array", "items": { "$ref": "#/$defs/NextStep" } },
    "sources": { "type": "array", "items": { "$ref": "#/$defs/SourceCitation" } }
  }
}
```

---

## Module 7: Global Property Opportunity Scanner

```json
{
  "$schema": "https://json-schema.org/draft/2020-12/schema",
  "title": "GlobalPropertyOpportunityScanner",
  "type": "object",
  "required": ["markets", "signalSummary"],
  "properties": {
    "signalSummary": { "type": "string" },
    "markets": {
      "type": "array",
      "items": {
        "type": "object",
        "required": ["name", "totalScore", "tier", "factors"],
        "properties": {
          "name": { "type": "string" },
          "totalScore": { "type": "integer", "minimum": 5, "maximum": 25 },
          "tier": { "enum": ["Top Tier", "Emerging", "Watch", "Avoid"] },
          "factors": {
            "type": "object",
            "properties": {
              "priceToIncome": { "type": "integer", "minimum": 1, "maximum": 5 },
              "migrationFlows": { "type": "integer", "minimum": 1, "maximum": 5 },
              "capitalInflows": { "type": "integer", "minimum": 1, "maximum": 5 },
              "infrastructureMomentum": { "type": "integer", "minimum": 1, "maximum": 5 },
              "supplyDemandBalance": { "type": "integer", "minimum": 1, "maximum": 5 }
            }
          },
          "investmentThesis": { "type": "string" },
          "primaryRisk": { "type": "string" },
          "holdHorizon": { "type": "string" }
        }
      }
    },
    "dataCaveats": { "type": "array", "items": { "$ref": "#/$defs/DataCaveat" } },
    "nextSteps": { "type": "array", "items": { "$ref": "#/$defs/NextStep" } },
    "sources": { "type": "array", "items": { "$ref": "#/$defs/SourceCitation" } }
  }
}
```

---

## Community Trust: Displacement Early Warning

```json
{
  "$schema": "https://json-schema.org/draft/2020-12/schema",
  "title": "DisplacementEarlyWarning",
  "type": "object",
  "required": ["location", "signalSummary", "riskScore", "tier", "dimensions"],
  "properties": {
    "location": { "type": "string" },
    "signalSummary": { "type": "string" },
    "riskScore": { "type": "integer", "minimum": 0, "maximum": 100 },
    "tier": { "enum": ["Critical", "Elevated", "Moderate", "Low"] },
    "trend": {
      "type": "object",
      "properties": {
        "direction": { "enum": ["Accelerating", "Stable", "Decelerating"] },
        "modifier": { "type": "integer", "minimum": -10, "maximum": 10 }
      }
    },
    "dimensions": {
      "type": "object",
      "properties": {
        "affordabilityPressure": {
          "type": "object",
          "properties": {
            "score": { "type": "integer", "minimum": 0, "maximum": 30 },
            "rentBurdenPct": { "type": "number", "description": "% of renters spending >30% on housing" },
            "rentGrowthVsIncomeGrowth": { "type": "number", "description": "ratio of rent growth to income growth" },
            "affordableUnitPipeline": { "type": "string" },
            "keyDriver": { "type": "string" }
          }
        },
        "tenureInstability": {
          "type": "object",
          "properties": {
            "score": { "type": "integer", "minimum": 0, "maximum": 25 },
            "evictionFilingRate": { "type": "number" },
            "renterSharePct": { "type": "number" },
            "avgLengthOfResidence": { "type": "string" },
            "keyDriver": { "type": "string" }
          }
        },
        "investmentPressure": {
          "type": "object",
          "properties": {
            "score": { "type": "integer", "minimum": 0, "maximum": 25 },
            "investorPurchaseSharePct": { "type": "number" },
            "cashPurchasePct": { "type": "number" },
            "renovationPermitSurge": { "type": "boolean" },
            "keyDriver": { "type": "string" }
          }
        },
        "policyProtection": {
          "type": "object",
          "properties": {
            "score": { "type": "integer", "minimum": 0, "maximum": 20 },
            "rentStabilization": { "type": "boolean" },
            "justCauseEviction": { "type": "boolean" },
            "rightOfFirstRefusal": { "type": "boolean" },
            "communityLandTrust": { "type": "boolean" },
            "keyDriver": { "type": "string" }
          }
        }
      }
    },
    "convergingSignals": {
      "type": "array",
      "items": {
        "type": "object",
        "properties": {
          "signal": { "type": "string" },
          "data": { "type": "string" },
          "source": { "type": "string" }
        }
      }
    },
    "protectiveFactors": { "type": "array", "items": { "type": "string" } },
    "dataCaveats": { "type": "array", "items": { "$ref": "#/$defs/DataCaveat" } },
    "nextSteps": { "type": "array", "items": { "$ref": "#/$defs/NextStep" } },
    "sources": { "type": "array", "items": { "$ref": "#/$defs/SourceCitation" } }
  }
}
```

---

## Community Trust: Government Accountability Scorecard

```json
{
  "$schema": "https://json-schema.org/draft/2020-12/schema",
  "title": "GovernmentAccountabilityScorecard",
  "type": "object",
  "required": ["jurisdiction", "signalSummary", "overallScore", "tier", "dimensions"],
  "properties": {
    "jurisdiction": { "type": "string" },
    "signalSummary": { "type": "string" },
    "overallScore": { "type": "integer", "minimum": 0, "maximum": 100 },
    "tier": { "enum": ["Responsive", "Functional", "Needs Improvement", "Failing"] },
    "dimensions": {
      "type": "object",
      "properties": {
        "codeEnforcement": {
          "type": "object",
          "properties": {
            "score": { "type": "integer", "minimum": 0, "maximum": 25 },
            "trend3yr": { "$ref": "#/$defs/TrendArrow" },
            "avgDaysViolationToInspection": { "type": "number" },
            "avgDaysToResolution": { "type": "number" },
            "repeatViolationRate": { "type": "number" }
          }
        },
        "permitProcessing": {
          "type": "object",
          "properties": {
            "score": { "type": "integer", "minimum": 0, "maximum": 25 },
            "trend3yr": { "$ref": "#/$defs/TrendArrow" },
            "avgDaysToApproval": { "type": "number" },
            "rejectionRate": { "type": "number" },
            "resubmissionRate": { "type": "number" }
          }
        },
        "complaintResolution": {
          "type": "object",
          "properties": {
            "score": { "type": "integer", "minimum": 0, "maximum": 25 },
            "trend3yr": { "$ref": "#/$defs/TrendArrow" },
            "avgResponseTimeDays": { "type": "number" },
            "resolution30DayPct": { "type": "number" }
          }
        },
        "publicAccessibility": {
          "type": "object",
          "properties": {
            "score": { "type": "integer", "minimum": 0, "maximum": 25 },
            "trend3yr": { "$ref": "#/$defs/TrendArrow" },
            "meetingNoticeLeadTimeDays": { "type": "integer" },
            "virtualParticipation": { "type": "boolean" },
            "languageAccess": { "type": "boolean" },
            "adaCompliance": { "type": "boolean" },
            "documentsOnline": { "type": "boolean" }
          }
        }
      }
    },
    "peerComparison": { "type": "string" },
    "equityCheck": { "type": "string" },
    "budgetSignal": {
      "type": "object",
      "properties": {
        "housingBudgetPct": { "type": "number" },
        "trend": { "$ref": "#/$defs/TrendArrow" },
        "perCapita": { "type": "number" }
      }
    },
    "dataCaveats": { "type": "array", "items": { "$ref": "#/$defs/DataCaveat" } },
    "nextSteps": { "type": "array", "items": { "$ref": "#/$defs/NextStep" } },
    "sources": { "type": "array", "items": { "$ref": "#/$defs/SourceCitation" } }
  }
}
```

---

## Community Trust: Community-Reported Conditions

```json
{
  "$schema": "https://json-schema.org/draft/2020-12/schema",
  "title": "CommunityReportedConditions",
  "type": "object",
  "required": ["location", "signalSummary", "conditions"],
  "properties": {
    "location": { "type": "string" },
    "signalSummary": { "type": "string" },
    "conditions": {
      "type": "array",
      "items": {
        "type": "object",
        "properties": {
          "category": { "enum": ["Housing Quality", "Infrastructure", "Environmental", "Service Gaps", "Safety"] },
          "complaintsPer1KHH": { "type": "number" },
          "trend3yr": { "$ref": "#/$defs/TrendArrow" },
          "avgResponseDays": { "type": "number" },
          "resolutionRatePct": { "type": "number" }
        }
      }
    },
    "topIssues": { "type": "array", "items": { "type": "string" } },
    "responseEquity": { "type": "string" },
    "dataCaveats": { "type": "array", "items": { "$ref": "#/$defs/DataCaveat" } },
    "nextSteps": { "type": "array", "items": { "$ref": "#/$defs/NextStep" } },
    "sources": { "type": "array", "items": { "$ref": "#/$defs/SourceCitation" } }
  }
}
```

---

## Platform Brief (Multi-Module Wrapper)

```json
{
  "$schema": "https://json-schema.org/draft/2020-12/schema",
  "title": "PlatformBrief",
  "type": "object",
  "required": ["location", "date", "bottomLine", "convictionLevel", "modules"],
  "properties": {
    "location": { "type": "string" },
    "date": { "type": "string", "format": "date" },
    "bottomLine": { "type": "string" },
    "convictionLevel": { "enum": ["High", "Medium", "Low"] },
    "convictionRationale": { "type": "string" },
    "keySignalsConverging": {
      "type": "array",
      "items": {
        "type": "object",
        "properties": {
          "module": { "type": "string" },
          "finding": { "type": "string" }
        }
      }
    },
    "primaryRisk": { "type": "string" },
    "modules": {
      "type": "array",
      "description": "Array of individual module outputs (any of the schemas above)",
      "items": { "type": "object" }
    }
  }
}
```

---

## Usage Notes

- All schemas use [JSON Schema 2020-12](https://json-schema.org/draft/2020-12/schema)
- Shared types (`DataCaveat`, `NextStep`, `SourceCitation`, `TrendArrow`) should be defined in a `$defs` block and referenced via `$ref`
- Scores are always integers; rates and percentages are numbers (0.0–100.0)
- All modules include `dataCaveats`, `nextSteps`, and `sources` arrays
- Fair Housing compliance: no field in any schema captures protected class characteristics or proxies
