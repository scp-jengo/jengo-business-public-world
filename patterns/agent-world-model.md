# Pattern: Agent World Model

## Problem

An agent loaded with identity, knowledge, and system context knows who it is, what frameworks it uses, and how the codebase works. It still does not know what exists in the operational environment: what projects are running, what services are live, who is involved, what the current state of the work is.

Without world context, the agent operates in a vacuum. It answers questions correctly in the abstract but incorrectly in the specific. It recommends deploying to a server that was decommissioned. It asks who owns the payment service. It suggests adding a dependency on a project that was completed eight months ago. The world layer prevents all of this.

## What world context provides

When world layer files are loaded at agent startup, the agent has:

- A current list of active projects with their owners, dependencies, and blockers
- A current service map with status, URLs, health check endpoints, and deployment details
- A people registry with roles, expertise areas, and current project assignments

This is the agent's operational map. It is the difference between an agent that knows the codebase and an agent that knows the codebase and the environment it runs in.

## Loading order

Load world context last, after identity, knowledge, and system context. World context is the most variable layer — it changes as projects progress and services get deployed. Loading it last means it always reflects the current state against a stable base of identity and knowledge.

## What to load at startup

Load all `active` projects. Load all services regardless of status — knowing a service is `stopped` is as important as knowing it is `running`. Load people who are active on current projects.

Do not load `archived` projects unless specifically relevant to the query. Archived entries exist for reference, not for active context.

## When the world model is stale

A stale world model produces confident wrong answers. An agent that reads a project as `active` when it was completed three months ago will make decisions based on a false premise.

The signal that the world model may be stale is a mismatch between what the agent finds in the registry and what it observes in the environment — a service listed as `running` that does not respond, a project listed as `active` with a `target_date` six months in the past.

When the agent detects a potential staleness signal, it should flag it explicitly rather than silently proceeding on the stale data. The correct response is: "The service map shows X as running, but the health check is not responding. The entry may be stale — please verify before I proceed."

## Keeping the world model useful

The world layer is only as useful as the discipline applied to keeping it current. Treat world layer updates as a first-class engineering activity, not documentation debt. When you deploy a service, update `last_deployed`. When a project completes, update `status`. When an owner changes, update the entry.

An agent that can trust its world model is a fundamentally different tool than one that cannot.
