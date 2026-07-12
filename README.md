# apigee-opdk-setup-scopes-add — Bind Org/Env Scopes to an Apigee OPDK Analytics Group

> 🔄 **Evolution note:** The automation approach from this OPDK-era role has been consolidated into the `apigee-hybrid-workspace` Ansible collection. See the successor capability in the portfolio hub: [`carlosfrias/apigee-hybrid-workspace`](https://github.com/carlosfrias/apigee-hybrid-workspace) → `bap_coe/private_cloud/` and `bap_coe/apigee_hybrid/`. The collection README explains each role group’s business value and production context.


> **An Ansible role that binds an organization and environment as a scope on an Apigee analytics group** — the scope-binding step in the analytics topology lifecycle: `axgroup → consumer-group → {consumers, datastores} + {scopes (org, env)}`.

> [!NOTE]
> Engineering portfolio note — this role is part of the analytics-topology lifecycle. See the [skills assessment →](SKILLS-ASSESSMENT.md) for the expertise applied.

This role adds a scope (org + env) to an existing axgroup, completing the analytics topology: the axgroup now has consumers (Qpid), datastores (Postgres), and scopes (org/env). It is composed after `apigee-opdk-setup-qpid-add` and `apigee-opdk-setup-postgres-add`. See the [`apigee-edge-opdk`](https://github.com/carlosfrias/apigee-edge-opdk) framework for composition playbooks.

<!-- BEGIN Google Required Disclaimer -->

## Not Google Product Clause

This is not an officially supported Google product.
<!-- END Google Required Disclaimer -->

---

## What the role actually does

`tasks/main.yml`:

1. **Determine network interface and local Management Server IP** — `interface.yml` and `local_mgmt_ip.yml` (shared includes).
2. **Assert required attributes** — `org_name`, `env_name`, `local_mgmt_ip`, credentials.
3. **Add scope to the analytics group** — `POST /v1/analytics/groups/ax/{ax_group}/scopes?org={org_name}&env={env_name}`.
4. **Rescue with local delegation** — if the direct call fails, re-run against `127.0.0.1:8080` delegated to the MS host.

---

## Role variables (selected)

| Variable | Purpose |
|----------|---------|
| `ax_group` | The analytics group name (default: `axgroup001`) |
| `org_name` | The Apigee organization to bind |
| `env_name` | The Apigee environment to bind |
| `local_mgmt_ip` | Management Server IP |
| `opdk_user_email` / `opdk_user_pass` | MS API credentials |

---

## Provenance

Authored and maintained by **Carlos Frias** during his tenure on Apigee Edge Private Cloud. One of the analytics-topology roles in the `apigee-opdk-*` corpus.

Contributions welcome — see [CONTRIBUTING.md](./CONTRIBUTING.md).

## License

See [LICENSE](./LICENSE).