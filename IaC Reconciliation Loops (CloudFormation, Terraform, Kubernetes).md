## Two Patterns: Forward Loop vs Reconciliation Loop

**Forward loop (Redux-style)** — action-driven:

```
action → reducer(currentState, action) → newState
```

**Reconciliation loop (IaC-style)** — state-driven:

```
(currentState, desiredState) → reconciler → [actions]
```

In IaC, you declare _what you want_. The reconciler figures out _what needs to happen_.

---

## Key Terminology

|Concept|Terraform|Kubernetes|General|
|---|---|---|---|
|The "reducer"|Planner|Reconciler|Reconciler|
|The output|Plan / changeset|Patch operations|Diff / actions|
|The executor|Apply|Actuator|Actuator|

---

## Edge-Triggered vs Level-Triggered

From digital electronics — what causes a circuit to react?

**Edge-triggered** — reacts to _transitions_ (something happened)

- Miss the event = miss it forever
- Redux actions, queues, webhooks, button clicks

**Level-triggered** — reacts to _current state_ (something is)

- Can never miss it — just re-examine reality on the next tick
- IaC reconcilers, thermostats, Kubernetes controllers

> Edge-triggered systems are **historians**. Level-triggered systems are **inspectors**.

---

## What If the Actions Don't Produce the Right State?

The loop runs again. Correctness comes from **continuous iteration**, not a perfect one-shot plan:

```
observe → diff → plan → apply → observe → diff → ...
```

Each cycle closes the gap further until current state matches desired state — **eventual convergence**.

### This requires idempotency

Actions must be safe to apply repeatedly. "Set replicas to 3" is idempotent. "Add one replica" is not.

### When convergence fails

If the loop can't close the gap (conflicting controllers, unreachable desired state), the system surfaces a **degraded** status for a human to intervene. It admits failure rather than looping silently.

--- 


## Reconciliation vs Transactions
 
|                       | Transaction                | Reconciliation       |
| --------------------- | -------------------------- | -------------------- |
| Correctness model     | Atomicity (all or nothing) | Eventual convergence |
| On failure            | Rolls back                 | Retries              |
| Requires perfect plan | Yes                        | No                   |
| Self-healing          | No                         | Yes                  |


---

## CloudFormation Specifically

CloudFormation is a reconciliation loop. Your template is the **desired state**. On deploy, CloudFormation diffs it against the current stack state, generates a **changeset** (the plan), and applies it. If something fails mid-apply, it can roll back or you can retry — because the desired state is always the source of truth, not the sequence of events that got you there.