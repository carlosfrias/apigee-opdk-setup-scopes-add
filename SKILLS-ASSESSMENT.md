# Skills Assessment — apigee-opdk-setup-scopes-add

> **Skill domain:** Apigee analytics topology modeling — binding org/env scopes to an analytics group (OPDK). Part of the broader Apigee platform-operations portfolio; see the [`bap_coe` portfolio hub →](https://github.com/carlosfrias/apigee-hybrid-workspace/blob/main/SKILLS-ASSESSMENT.md) for the cloud-native (Hybrid/K8s) counterpart and the full corpus.

---

## Why this role is notable

- **Scope binding completes the topology.** After the axgroup has consumers (Qpid) and datastores (Postgres), scopes bind the analytics group to an org/env — making the topology live. Without scopes, the analytics pipeline is wired but not serving traffic.
- **Rescue-based local delegation.** If the direct MS call fails, the role re-runs against `127.0.0.1:8080` delegated to the MS host — the same `block/rescue` pattern used in `analytics-group-add`.
- **Composed lifecycle.** This role is the final step: `analytics-group-add` → `qpid-add` → `postgres-add` → **`scopes-add`**. The topology is built incrementally.

---

## Expertise demonstrated

> Ansible is the medium. The engineering evidence lives in the [project README →](README.md). What follows is the skills assessment for the business reader.

- **Apigee analytics topology modeling** — scopes (org, env) as the binding that makes an analytics group serve traffic for a specific org/env. The directed object graph is complete: `axgroup → consumer-group → {consumers, datastores} + {scopes}`.
- **Idempotent REST reconciliation** — `block/rescue` local-delegation fallback on every MS call, same pattern as `analytics-group-add`.
- **Composable role architecture** — the final step in the composable lifecycle. Each role owns one API interaction.

---

## How this shows the expertise

The expertise is in understanding that the analytics topology has three layers: structure (axgroup + consumer group), capacity (Qpid consumers + Postgres datastores), and binding (scopes). This role adds the binding. Without it, the analytics pipeline is wired but not routing traffic for any org/env.

The rescue-based local delegation pattern (try direct, fall back to MS host) is the same pattern used in `analytics-group-add` — consistent idempotent reconciliation across the lifecycle.

---

## Related expertise

| Skill | Repository | Assessment |
|-------|-----------|-----------|
| Analytics (axgroup) lifecycle | [`apigee-opdk-setup-analytics-group-add`](https://github.com/carlosfrias/apigee-opdk-setup-analytics-group-add) | [SKILLS-ASSESSMENT.md →](https://github.com/carlosfrias/apigee-opdk-setup-analytics-group-add/blob/main/SKILLS-ASSESSMENT.md) ✅ |
| Qpid consumer addition | [`apigee-opdk-setup-qpid-add`](https://github.com/carlosfrias/apigee-opdk-setup-qpid-add) | [SKILLS-ASSESSMENT.md →](https://github.com/carlosfrias/apigee-opdk-setup-qpid-add/blob/main/SKILLS-ASSESSMENT.md) ✅ |
| Postgres datastore addition | [`apigee-opdk-setup-postgres-add`](https://github.com/carlosfrias/apigee-opdk-setup-postgres-add) | [SKILLS-ASSESSMENT.md →](https://github.com/carlosfrias/apigee-opdk-setup-postgres-add/blob/main/SKILLS-ASSESSMENT.md) ✅ |
| Cloud-native (Hybrid/K8s) counterpart | [`apigee-hybrid-workspace`](https://github.com/carlosfrias/apigee-hybrid-workspace) | [SKILLS-ASSESSMENT.md →](https://github.com/carlosfrias/apigee-hybrid-workspace/blob/main/SKILLS-ASSESSMENT.md) ✅ portfolio hub |

---

## Provenance

Authored and maintained by **Carlos Frias** during his tenure on Apigee Edge Private Cloud. This skills assessment is the companion to the engineering [README →](README.md).

## License

See [LICENSE](./LICENSE).