---
name: check-upgrade-contract
description: Test compatibility when a released producer and consumer share an identifier, file format, route or persisted setting. Use for upgrades and mixed-version rollouts where today's happy path can pass while an existing client breaks.
license: MIT
---

# Check the upgrade contract

Name the value that crosses the boundary, who writes it, who reads it, and what must still happen after an upgrade. Two strings of the same type can refer to different things: a catalog item is not the entitlement it grants.

1. Find the contract in the released producer or a sanitized historical fixture. Record the meaning, spelling, encoding, default and version when relevant. Don't generate all “old” inputs using the new serializer.
2. Choose the combinations the deployment actually promises. Start with old producer to new consumer and new to new. Add new producer to old consumer only if they can overlap or a rollback is supported. State why any direction is out of scope.
3. Use the normal entry point with a disposable copy of state or a test service. Include a previously valid value, the new value, and an unrecognized one. For routes, exercise the released client's method, body and redirect behavior. For formats, verify meaningful decoded values, not just a successful open.
4. Check both outcome and side effects. A rejected identifier must not silently become valid or consume a limited use. For a retryable operation, compare state before, after and after retry. Don't use a real customer's key or a live purchase.

Report a small table: producer version, consumer version, case, expected, observed, state change. Mark combinations you could not exercise as untested. A candidate-only pass is not backward compatibility. Reading an old identifier with a new client does not exercise the old client binary. When a migration is needed, keep a regression from the old representation and check the rollback promise separately.
