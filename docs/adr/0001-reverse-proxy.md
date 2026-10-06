# ADR-0001 — Reverse proxy choice: Nginx vs Traefik

## Status

Accepted

## Context

The team hosts around 15 services in Docker containers across two servers. New services are added roughly every month. TLS certificate renewal is done manually and has already caused a production outage. The infrastructure team has strong experience with Nginx but has never used Traefik.

The reverse proxy must handle HTTP/HTTPS routing for all services, TLS termination, and accommodate frequent service additions without manual reconfiguration.

## Options considered

### Option A — Nginx

A battle-tested HTTP server and reverse proxy. The team already knows it well.

**Pros**
- Team is fully comfortable with the configuration syntax
- Very stable, widely documented
- Fine-grained control over every routing rule

**Cons**
- No automatic service discovery: each new service requires a manual config update and reload
- No built-in automatic TLS renewal — requires a separate tool (e.g. certbot + cron) and has already caused an outage when renewal was missed
- Operational overhead grows linearly with the number of services

### Option B — Traefik

A cloud-native reverse proxy designed for dynamic containerised environments.

**Pros**
- Automatic service discovery via Docker labels: adding a service requires no Nginx config change
- Built-in Let's Encrypt integration with automatic certificate renewal — eliminates the manual renewal risk
- Dashboard for real-time routing visibility
- Scales well as the number of services grows

**Cons**
- The team has no existing experience with Traefik — initial learning curve
- Configuration model (providers, routers, middlewares) is different from Nginx and requires onboarding time

## Decision

Adopt **Traefik**.

The two main pain points — manual TLS renewal causing outages and the friction of updating Nginx config for every new service — are both solved natively by Traefik. The team's unfamiliarity is a short-term cost; the ongoing operational savings justify it given the current pace of service additions (~12/year).

## Consequences

- The team must allocate time to learn Traefik configuration before the migration.
- Existing Nginx config must be migrated to Traefik router/middleware definitions.
- Manual certbot renewals and associated cron jobs can be decommissioned once Traefik manages TLS.
- A runbook for Traefik operations should be written as part of the migration.
