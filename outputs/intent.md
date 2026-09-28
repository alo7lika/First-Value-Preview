# intent.md — Why this problem?

## Decision

I chose the first-value failure in a fictional team-notes product: a newly invited teammate lands on a blank workspace, cannot tell what they can do, and has no guided route to create a useful first summary. This is the highest-priority blocker because it prevents the product’s first promised outcome before the user can judge its value.

## User and problem

**Target user:** a teammate invited to an existing workspace who is not its administrator. They may be unfamiliar with the product and should not need an administrator to explain access or get started.

**Problem statement:** After accepting an invite, a teammate sees an empty workspace and ambiguous access/version cues. They do not know whether they can add notes, what to do first, or how to recover if importing notes fails. The result is stalled activation and avoidable support/admin help.

**Evidence basis:** the supplied Quest brief describes invite-only access, unclear permissions, two confusing live-version labels, an unclear free-plan limit, a blank first screen and no recovery after failed import. These are scenario facts supplied in the brief, not research findings. No user interviews, product telemetry, support tickets or live product access were provided. The severity ordering and value estimates below are reasoned hypotheses, not measured impact.

## Alternatives and prioritization

Scored 1–5 (5 is strongest) against first-value impact (35%), frequency/reach (20%), severity of user blockage (20%), and ability to scope and verify within this Quest (25%). Weighted total is out of 5. Scores are judgment calls from the fictional brief, not observed data.

| Candidate blocker | First value 35% | Reach 20% | Severity 20% | Verifiable scope 25% | Weighted score |
|---|---:|---:|---:|---:|---:|
| Blank first-run experience; unclear teammate permissions and no useful first action | 5 | 5 | 5 | 5 | **5.00** |
| Failed import has no recovery path | 4 | 3 | 4 | 4 | 3.80 |
| Free-plan limit is unclear | 3 | 4 | 3 | 4 | 3.45 |
| Two live-version labels are confusing | 2 | 4 | 3 | 4 | 3.10 |
| Invite-only access/login friction | 4 | 3 | 4 | 2 | 3.25 |

**Why this ranks first:** it combines the blank state and the permission uncertainty at the exact moment a new teammate needs to act. It also gives a narrow, demonstrable journey with clear outcomes. The failed-import problem remains in scope as a recovery branch, but it is not the primary problem being solved. The other items require separate policy, naming or access decisions.

## Intended value

A teammate should understand their role, take a permitted first action, and reach a useful summary without manual administrator help. The demo makes that outcome inspectable. For a real release, success would be measured by the share of eligible invitees who create a first note and generate their first summary, plus elapsed time from invite acceptance to summary. No numeric lift is claimed because no baseline exists.

## Non-goals

- Real authentication, invitations, authorization enforcement, persistence, imports, AI summarization, billing or plan enforcement.
- Resolve the product’s canonical version name or redesign the free-plan policy.
- Build administrator provisioning, a complete notes product, or a production-ready security model.
- Claim user research, production analytics, support volume, conversion lift or release approval.

## Assumptions to validate before a real build

1. Invited non-admin teammates are an important first-run cohort.
2. Creating a note and generating a summary represents meaningful first value.
3. A teammate is allowed to create notes and summaries in the target workspace.
4. Failed imports can be retried without corrupting existing content.
5. The actual product has a support owner and an operational feature flag or equivalent disable path.
