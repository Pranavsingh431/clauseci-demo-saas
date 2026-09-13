# Northwind Platform, service configuration

Declarative configuration for the Northwind Platform, a multi tenant B2B SaaS
product with three enterprise tenants.

Changing a value under `config/` changes product behaviour for named customers.
Some of those behaviours are constrained per customer by signed agreements that
live in Legal's document store, not in this repository.

`ClauseCI` runs against pull requests here. It resolves the effective value for
each customer, compares it against the controlling signed agreement, and
publishes a commit status recording its decision.

`main` is protected and requires the `ClauseCI / retention-compliance` status,
so a pull request cannot be merged until that check has reported.

| Path                        | Controls                                      |
|-----------------------------|-----------------------------------------------|
| `config/retention.yaml`     | How long log data is kept, per customer       |
| `config/regions.yaml`       | Where customer data is stored and processed   |
| `config/subprocessors.yaml` | Third party vendors that touch customer data  |
| `config/sla.yaml`           | Uptime and notice period commitments          |
| `api/public_endpoints.yaml` | Documented public API surface and lifecycle   |

## Retention resolution

For any (customer, field) pair the effective value is the value under
`customers.<id>` if present, otherwise the value under `defaults`. This means a
change to `defaults` silently changes every tenant that does not pin its own
override.
