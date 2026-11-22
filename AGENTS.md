# AI agent entry point — Tertalis Experiment Runner

This is an application repository with a complete imported Tertalis platform
snapshot. Human and AI contributors use the **same** setup scripts.
Do not infer that application source or local coordination snapshots own the
Tertalis platform or cross-repository coordination authority.

## Begin here

1. Read [README.md](README.md) for purpose, status and basic setup.
2. Read [SETUP.md](SETUP.md) and
   [the application README](first-party/applications/experimentRunner/README.md)
   for real prerequisites, models, application configuration and launch steps.
3. Read the **canonical** coordination index and protocol on
   [Tertalis/Tertalis `integration`](https://github.com/Tertalis/Tertalis/tree/integration/ai-workflow).
   The `ai-workflow/` copies in this checkout are inherited snapshots, **not**
   independent current inboxes. Never publish coordinated messages or claims
   here as if those copies were authoritative.
4. Read the Experiment Runner workstream's latest STATE, HANDOFF, inbox,
   assignment and baseline on the canonical coordination ref.
5. Establish authorization and ownership under that protocol before modifying
   source or adopting another platform revision. A new branch or repository
   does not imply a new Coordinator or implementation claim.

## Working boundaries

- `first-party/applications/experimentRunner/` is application-owned.
- `backend/`, reusable `first-party/` Packs and associated shared tests
  are a pinned snapshot of the Tertalis platform, not application-owned code.
- Application compatibility updates require an authorized Integrator operation
  and verified acceptance. Failed integration must not advance the accepted
  platform revision.
- Read relevant design/contracts before modifying platform-facing behavior.
  This older application snapshot may contain pre-migration naming and
  documents; do not silently rewrite semantics or historical evidence.
- Preserve history. Do not delete branches, force push, republish packages or
  perform destructive/failure tests without proper authorization.

## Setup and verification (Windows)

From the repository root:

```powershell
.\setup.bat
.\first-party\applications\experimentRunner\setup.bat
.\python-embedded\python.exe -X frozen_modules=off -m pytest tests
```

The application setup does not call root setup. Local host JSON and
`local/run.bat` must be configured by the user for real inference; model
binaries and assets are not automatically installed. The application's
tracked `run.bat` includes sample commands.

Report which tests were actually run, outcomes, skipped conditions and
exact Git refs. Follow the canonical coordination finish/handoff barrier.

## Platform documentation authority

For Tertalis platform contracts and design, consult the CURRENT
`Tertalis/Tertalis` `integration` `design/index.txt` and relevant
authoritative platform design/docs, because this Application does not carry copied root `design/`
or `docs/` trees. Retrieve only the
areas pertinent to the assigned task and its dependencies; do not load
the entire design corpus by default. Current documentation does NOT
authorize upgrading this Application's accepted Tertalis source SHA.
Some existing platform design specifications still reside in `docs/`;
their relocation to `design/` and future creator/user docs are not
yet complete. Release-version applicability annotations are future
work; use exact Git SHAs in current integration reports.

## Shared ai-workflow boundary

Every assistant, implementer, integrator, coordinator and design thread must
read the current canonical ai-workflow instructions at
[Tertalis/Tertalis integration](https://github.com/Tertalis/Tertalis/blob/integration/ai-workflow/index.txt)
before working. This repository's `ai-workflow/index.txt` is only a local
routing stub; its `integration` branch is the application's development
branch, not a coordination authority. All operational inboxes, messages,
workstream state and repository-location registry are maintained only in
`Tertalis/Tertalis` on `integration`. Do not create a local inbox or rely
on copied historical mail. For other applications, consult Tertalis's
canonical registry rather than recording their addresses here.
