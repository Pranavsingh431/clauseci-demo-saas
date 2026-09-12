# Northwind Platform — service configuration

Declarative configuration for the Northwind Platform (multi-tenant B2B SaaS).

Changes to files under `config/` and `api/` alter product behaviour for named
enterprise customers, and several of those behaviours are contractually
constrained per customer (retention, residency, sub-processor notice, API
deprecation notice).

`ClauseCI` runs as a status check on every pull request to this repository and
blocks merges that would breach a currently-executed customer agreement.

| Path                        | Controls                                        |
|-----------------------------|-------------------------------------------------|
| `config/retention.yaml`     | How long log data is kept, per customer         |
| `config/regions.yaml`       | Where customer data is stored and processed     |
| `config/subprocessors.yaml` | Third-party vendors that touch customer data    |
| `config/sla.yaml`           | Uptime and notice-period commitments            |
| `api/public_endpoints.yaml` | Documented public API surface and lifecycle     |
