# Tertalis Experiment Runner

**Status: experimental development application, not a stable release.**

Experiment Runner runs defined tests and experiments against managed Tertalis
model execution, records outcomes and evidence, and supports inspection,
reporting and export. This repository contains a complete, pinned Tertalis
platform working tree together with Experiment Runner's application code.
It is intended for developers and experimenters comfortable configuring
local model executables and working with evolving interfaces.

## Should you try it?

If you want to author and inspect local model experiments, and already have
the necessary compatible model files and server executable, there is
something concrete to try. This is **not** a one-click AI assistant.
The default templates contain paths that **you must configure**; setup
does not download an LLM or start a server.

See the [application README](first-party/applications/experimentRunner/README.md)
for the full feature descriptions, example definitions, configuration,
commands, limitations and evidence handling.

## Windows quick start

Clone the new standalone repository, then run two **separate** setup
scripts from the repository root:

```powershell
git clone https://github.com/Tertalis/Tertalis-Experiment-Runner.git
cd Tertalis-Experiment-Runner
.\setup.bat
.\first-party\applications\experimentRunner\setup.bat
```

The first script prepares Tertalis internals and the repository-local
`python-embedded/` runtime. The second prepares Experiment Runner's own
ignored local files, without invoking or modifying root setup.

Edit `first-party/applications/experimentRunner/local/host.basic.json`
to supply your model and llama-server paths. Then review and edit
`first-party/applications/experimentRunner/local/run.bat` and execute
that private copy. Its tracked template is at
`first-party/applications/experimentRunner/run.bat`.

Application setup preserves existing private configuration and results
rather than overwriting them. The application README explains the
basic conversation and materialization examples in detail.

For the platform setup options, including Python 3.14 fallback,
see [SETUP.md](SETUP.md).

## Development

The repository's default embedded Python is currently Python 3.15.0b4
(on Windows); the explicit fallback is Python 3.14.6. After root
setup, you can run tests with:

```powershell
.\python-embedded\python.exe -X frozen_modules=off -m pytest tests
```

This is the general repository test command, not a claim that every test
was executed for this migration. Some checks require environment-specific
prerequisites. The platform's shared Ruff/ty tools and setup verification
are documented in SETUP.md.

See [AGENTS.md](AGENTS.md) for AI work instructions. Source and application
tests are under `first-party/applications/experimentRunner/` and `tests/`.
Other reusable Tertalis source is present in the same checkout.

## Coordination and compatibility

This repository **participates in the shared Tertalis development
coordination system**. It does not maintain an independent authoritative
AI inbox. Until the planned cross-repository coordination backend has
been verified and adopted, the canonical file-based `ai-workflow`
coordination ref remains `integration` in
[EnterTheNameHere/Turnix](https://github.com/Tertalis/Tertalis/tree/integration).
Local copies in this repository are historical snapshots and must not
become separate active inboxes. Always consult the canonical index and
protocol before acquiring ownership or making coordinated changes.

Application and platform revisions must be integrated and verified
explicitly; a newer Tertalis commit is not automatically accepted.

## Future direction

Tertalis ultimately intends a proper CLI and PackageManager workflow.
Those are not available as current Experiment Runner setup commands.
