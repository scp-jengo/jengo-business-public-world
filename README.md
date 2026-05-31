# jengo-business-public-world

The world layer of the Jengo Business framework. This repo is the fourth public layer — it defines the operational environment: what projects exist, what services are running, who is involved, what tools and integrations are in play.

Think of it as the agent's map of the territory.

## What this repo is

A structured registry of everything external that a Jengo instance interacts with. It provides templates and schemas for documenting the operational environment so that AI agents have grounded, structured context about what actually exists — not just who you are or what frameworks you use, but what is currently running, being built, and by whom.

Without a world model, an agent operates without knowing the landscape. It cannot make deployment decisions, trace dependencies, or understand what projects are active. The world layer solves that.

## What this repo contains

- **templates/** — YAML templates for registering projects, services, and people
- **schemas/** — JSON Schema definitions for validating world entries
- **patterns/** — Documented patterns for maintaining a project registry, service map, and agent world model

## What this repo does NOT contain

- Actual project data for any specific organization
- Credentials, tokens, or secrets of any kind
- Private person records or contact information
- Environment-specific configuration values

Your private world repo (forked from this one) contains all of that. This repo contains only the templates, schemas, and patterns that make the private repo possible.

## Repo structure

```
jengo-business-public-world/
├── README.md
├── LICENSE
├── BOOTSTRAP.md
├── CONTRIBUTING.md
├── templates/
│   ├── project.template.yaml
│   ├── service.template.yaml
│   └── person.template.yaml
├── schemas/
│   ├── project.schema.json
│   └── service.schema.json
└── patterns/
    ├── project-registry.md
    ├── service-map.md
    └── agent-world-model.md
```

## Quick start

1. Fork this repo as your private world repo (e.g., `yourorg-world`)
2. Add your projects using `templates/project.template.yaml`
3. Add your running services using `templates/service.template.yaml`
4. Add your team using `templates/person.template.yaml` — keep this in your private fork
5. Validate entries against the schemas in `schemas/`
6. Load the world context at agent startup alongside the other three layers

## The four public layers

| Layer | Repo | Contains |
|-------|------|----------|
| identity | [jengo-business-public-identity](https://github.com/scp-jengo/jengo-business-public-identity) | Who you are — templates, protocols, agent persona |
| knowledge | [jengo-business-public-knowledge](https://github.com/scp-jengo/jengo-business-public-knowledge) | Shared frameworks and patterns |
| system | [jengo-business-public-system](https://github.com/scp-jengo/jengo-business-public-system) | Implementation code and tooling |
| world | this repo | Operational environment registry |

## Loading order

```
identity -> knowledge -> system -> world
```

World is loaded last because it is the most instance-specific layer. The other three provide the frameworks; world provides the facts on the ground.

## License

MIT. See LICENSE.
