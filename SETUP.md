# Repository-local Windows setup

Double-click root `setup.bat`, or run it from a terminal. It calls the adjacent
root `setup.ps1` using Windows PowerShell, works from any working directory and
returns the PowerShell exit code. Setup parameters can be passed through, for
example `setup.bat -Requirements requirements.txt`. On failure it prints the exit
code and waits for a key so a double-click console remains visible. Automation
can set `TERTALIS_SETUP_NO_PAUSE=1` to suppress that failure-only wait.

You can also run `powershell -NoProfile -ExecutionPolicy Bypass -File .\setup.ps1`.
Python 3.15.0b4 remains the primary runtime. Setup verifies the tracked vendor ZIP,
configures the embedded standard library/site-packages, installs requirements and
the Git pre-commit trampoline, then installs and verifies shared Ruff and ty.
Internet access to the configured pip package index is needed for missing packages.

`requirements-tools.txt` owns exact native-tool versions; `requirements.txt` includes
it. A custom `-Requirements` file does not disable shared tool installation.
Setup uses the selected embedded Python's pip and verifies its own `Scripts/ruff.exe`
and `Scripts/ty.exe`, their package/native versions and isolated checks on a temporary
sample. No repository-wide lint/type policy runs during setup. Failure stops setup
before its completion message. Rerunning verifies the tools again.

Use the reported absolute paths in trusted application host configurations. With
the default runtime, typical invocations are:

```powershell
.\python-embedded\python.exe -X frozen_modules=off -m pip --version
.\python-embedded\Scripts\ruff.exe --version
.\python-embedded\Scripts\ty.exe --version
.\python-embedded\python.exe -X frozen_modules=off .\scripts\verify_tools.py
```

The Windows EX-06 ty recipe is `check --config-file NUL --output-format concise FILE`.
`NUL` supplies an empty host-controlled configuration; it is not an artifact path.

For an explicitly selected Python 3.14.6 fallback, use `setup314.ps1`. It delegates
to the same installer/verifier and retains its historical default `python-embedded`
destination. To keep an existing 3.15 installation, select a separate destination:

```powershell
powershell -NoProfile -ExecutionPolicy Bypass -File .\setup314.ps1 -EmbedDir python-embedded\fallback314
```

The Git documentation hook continues to use the default `python-embedded/python.exe`;
an alternate destination does not change that hook contract. An explicit fallback
into the default destination replaces that environment as before; there is no
automatic downgrade. Applications must use the selected runtime/tool paths.

Root setup provisions only Tertalis internals. It never discovers Applications or
invokes their setup scripts. For Application-local initialization, run that
Application's own `setup.bat` or `setup.ps1` separately after root setup. Those
scripts own local templates and user-file preservation and should check existing
platform prerequisites; they do not invoke root setup. Platform checkouts need
no Application source to provision tools.

## Experiment Runner application setup

This repository contains both Tertalis internals and Experiment Runner.
The root setup scripts belong to **Tertalis** and do not initialize or
discover the application.

After successful root setup, run the separate application setup from the
repository root:

```powershell
.\first-party\applications\experimentRunner\setup.bat
```

Alternatively, call
`first-party/applications/experimentRunner/setup.ps1` directly from
PowerShell. Application setup verifies prerequisite platform files/tools,
then initializes private `local/` templates where absent; it preserves
existing user configuration, experiments and results. It never calls root
setup, downloads LLMs or takes over a model server.

To run the default example, configure approved model/server paths in
`first-party/applications/experimentRunner/local/host.basic.json`.
Then edit the private `first-party/applications/experimentRunner/local/run.bat`
to select an example and execute it. See the
[application README](first-party/applications/experimentRunner/README.md)
for exact requirements and guidance. The templates are not ready for real
model execution until external assets have been configured.

## Development test entry point

From repository root after setup:

```powershell
.\python-embedded\python.exe -X frozen_modules=off -m pytest tests
.\python-embedded\python.exe -X frozen_modules=off .\scripts\verify_tools.py
```

Run targeted test paths where applicable. Some tests need OS-specific or
external prerequisites. These are command instructions, not a claim that
the full suite has passed on the newly migrated repository.

For cross-repository AI coordination, see
[AGENTS.md](AGENTS.md). The canonical file-based inbox still lives on
`integration` in `Tertalis/Tertalis`; copied local files
are not independent active inboxes.
