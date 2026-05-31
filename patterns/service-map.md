# Pattern: Service Map

## Problem

An agent asked to deploy, debug, or reason about infrastructure has no grounded context without a service map. It cannot know what is running, where it lives, how to reach it, who owns it, or what it depends on. The result is a agent that either asks basic questions on every task or gets things wrong silently.

## What a service map is

A directory of YAML files — one per service — validated against the service schema. Each file describes one running piece of infrastructure: what it does, how to reach it, where it runs, who is responsible, and what its current status is.

A service in this context is any persistent, named piece of running software that other things depend on: APIs, databases, background workers, monitoring tools, proxies, scheduled jobs with an endpoint.

## Degraded vs stopped

The distinction between `degraded` and `stopped` matters for agent decision-making.

`stopped` means the service is not running. An agent should not attempt to reach it, should not treat its endpoints as available, and should flag any dependency on it as broken.

`degraded` means the service is running but not at full capacity — elevated error rates, reduced throughput, a known issue under investigation. An agent working in a system that depends on a degraded service should account for instability. Degraded is not an alarm state requiring immediate escalation; it is a known condition to work around.

## Services with no health check

Not every service exposes a health check endpoint. For these, omit `health_check_url` from the entry. Document in `notes` how the service status is verified manually — for example, by checking logs or querying a specific endpoint that always returns a predictable response.

An agent that cannot verify service health via health check should fall back to the `status` field in the registry and treat it as the last known state. Stale status is a problem — see below.

## Keeping the map current

Update `status` and `last_deployed` whenever a service is deployed or its operational state changes. A service map that is two weeks out of date for `status` fields is actively misleading.

If your deployment pipeline can write to the service map automatically on deploy, do it. Treating the service map as a side effect of deployment rather than a manual documentation step is the most reliable way to keep it accurate.

## Dependency tracking

Service dependencies are runtime dependencies — what does this service call at runtime in order to function? Record these in `dependencies`. This allows an agent to trace blast radius: if service A goes to `stopped`, what other services are affected?
