# Pattern: Project Registry

## Problem

An agent working on a codebase without a project registry has no way to know what work is active, what has been completed, what is on hold, or how projects relate to each other. It either asks repeatedly or makes assumptions. Both outcomes waste time and produce errors.

## What a project registry is

A directory of YAML files — one per project — validated against the project schema. Each file describes one unit of intentional work: what it is, who owns it, what state it is in, and what it depends on.

The registry is not a task tracker. It does not track individual tasks, bugs, or sprint items. It tracks the existence and current state of projects as persistent entities. A project stays in the registry for its entire life, from `active` through to `archived` or `completed`.

## Keeping it current

A stale registry is worse than no registry. An agent that reads outdated status information will make wrong decisions confidently.

Update a project entry when:
- Its status changes (paused, completed, archived)
- Its owner changes
- A significant blocker emerges or is resolved
- Its dependencies change
- Its target date shifts by more than a week

Do not update for routine daily progress. The registry tracks state, not activity.

## What to include in notes

The `notes` field is the most valuable field for agent context. Use it to record:
- The current main blocker, if one exists
- Recent architectural decisions that constrain future work
- What is explicitly out of scope
- Anything a new person or agent would need to know to not waste time

Keep notes under 200 words. If more context is needed, link to a document.

## When to archive

Archive when a project is no longer referenced by active work and is unlikely to resume. Archiving is not deletion — archived entries remain in the registry and continue to serve as dependency references. Do not delete project entries unless they were created in error.

## Dependency tracking

When project A depends on project B, record `b-id` in A's `dependencies` list. This allows an agent to trace impact — if project B is blocked or changes direction, the agent can identify all downstream projects.

## Agent use

At startup, an agent should load the full project registry and identify which projects are `active`. These form the scope of current work. The agent should not treat `paused` or `archived` projects as current priorities unless explicitly directed.
