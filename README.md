# Jengo Business - Public World Layer

**Shared world model: entities, relationships, ontologies**

This repository contains the public world model - shared understanding of concepts, entities, and relationships.

---

## What This Repo Contains

- ✅ Ontologies (news sources, fact-checking orgs, media types)
- ✅ Entity schemas (source, article, claim, verification)
- ✅ Relationship models (source credibility, claim evidence)
- ✅ Public registries (fact-checking APIs, verification services)

## What This Repo Does NOT Contain

- ❌ Organization-specific relationships
- ❌ Personal contacts
- ❌ Private source lists
- ❌ Competitive intelligence

---

## Structure

```
jengo-business-public-world/
├── README.md
├── ontologies/
│   ├── media-ontology.yaml          # Media types, formats
│   ├── verification-ontology.yaml   # Verification concepts
│   └── source-ontology.yaml         # Source types
├── entities/
│   ├── schemas/
│   │   ├── source.schema.json
│   │   ├── article.schema.json
│   │   ├── claim.schema.json
│   │   └── verification.schema.json
│   └── registries/
│       ├── fact-checking-orgs.yaml  # Public fact-checkers
│       ├── media-bias-chart.yaml    # Known bias ratings
│       └── verification-apis.yaml   # Public APIs
├── relationships/
│   ├── source-credibility.yaml      # How credibility is modeled
│   ├── claim-evidence.yaml          # Evidence relationships
│   └── bias-spectrum.yaml           # Bias modeling
└── LICENSE
```

---

## Example: Source Ontology

```yaml
# ontologies/source-ontology.yaml

source_types:
  - id: news_outlet
    name: News Outlet
    attributes:
      - domain
      - founding_year
      - ownership
      - bias_rating
      - credibility_score

  - id: fact_checker
    name: Fact-Checking Organization
    attributes:
      - accreditation
      - methodology
      - transparency_score

  - id: primary_source
    name: Primary Source
    attributes:
      - authenticity
      - provenance
      - verification_status
```

---

## Example: Fact-Checking Registry

```yaml
# entities/registries/fact-checking-orgs.yaml

organizations:
  - id: snopes
    name: Snopes
    url: https://www.snopes.com
    api: https://api.snopes.com
    accreditation: IFCN
    founded: 1994
    methodology_url: https://www.snopes.com/fact-check-ratings/

  - id: factcheck_org
    name: FactCheck.org
    url: https://www.factcheck.org
    accreditation: Annenberg
    founded: 2003
    methodology_url: https://www.factcheck.org/our-process/

  - id: politifact
    name: PolitiFact
    url: https://www.politifact.com
    api: null
    accreditation: IFCN
    founded: 2007
    truthometer: true
```

---

## Example: Entity Schema

```json
// entities/schemas/source.schema.json

{
  "$schema": "http://json-schema.org/draft-07/schema#",
  "type": "object",
  "title": "Source",
  "description": "A news or information source",
  "properties": {
    "id": {
      "type": "string",
      "description": "Unique identifier"
    },
    "name": {
      "type": "string",
      "description": "Source name"
    },
    "domain": {
      "type": "string",
      "format": "hostname",
      "description": "Primary domain"
    },
    "type": {
      "type": "string",
      "enum": ["news_outlet", "fact_checker", "primary_source", "aggregator"]
    },
    "credibility_score": {
      "type": "number",
      "minimum": 0,
      "maximum": 1,
      "description": "Credibility score 0-1"
    },
    "bias_rating": {
      "type": "string",
      "enum": ["left", "lean_left", "center", "lean_right", "right", "unknown"]
    }
  },
  "required": ["id", "name", "domain", "type"]
}
```

---

## Using This World Model

Jengo automatically loads this world model:

```python
from jengo.world import WorldModel

world = WorldModel()

# Check source credibility
source = world.get_entity('source', 'snopes')
print(source['credibility_score'])  # 0.95

# Get fact-checking APIs
apis = world.get_registry('fact_checking_orgs')
for org in apis:
    if org['api']:
        print(f"{org['name']}: {org['api']}")
```

---

## Contributing

To contribute to the public world model:

1. Ensure data is public (no proprietary info)
2. Provide sources for credibility ratings
3. Follow existing schemas
4. Submit PR with documentation

---

## License

MIT License + Data Attribution

Ontologies and schemas: MIT
Registry data: CC-BY-4.0 (attribution required)

---

**Status:** Production
**Version:** 1.0.0
**Maintained By:** SCP-Jengo Team
