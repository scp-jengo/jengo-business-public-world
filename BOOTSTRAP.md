# Bootstrap: World Layer

## Position in the inheritance chain

```
identity -> knowledge -> system -> world
```

The world layer is loaded fourth and last. It depends on the other three layers being present. It is the most instance-specific layer in the chain — it describes what actually exists in your operational environment, not what frameworks you use or who you are in the abstract.

## What this repo provides

Templates and schemas for registering the operational environment:

- Projects being built or maintained
- Services currently running
- People involved in the work
- Patterns for keeping the registry current and useful to AI agents

## How instances use this

You do not use this repo directly. You fork it as your private world repo — typically named something like `yourorg-world` — and populate it with your actual data.

Your private world repo:
- Contains entries for your actual projects (using project.template.yaml)
- Contains entries for your running services (using service.template.yaml)
- Contains your team members (using person.template.yaml) — keep this private
- Is validated against the schemas in this repo
- Is loaded into agent context at startup

## What the agent does with world context

When an agent starts up with world context loaded, it knows:
- What projects are currently active and what their status is
- What services are running, how to reach them, and who owns them
- What the dependencies between projects and services look like
- Who to involve for a given area of work

This allows the agent to make grounded decisions about deployment, architecture, and prioritization rather than asking about the environment constantly.

## Version

1.0.0
