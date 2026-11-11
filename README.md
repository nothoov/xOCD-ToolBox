## Starting the application

Open **xOCD Toolbox.exe** on 64-bit Windows 10 or Windows 11. Normal startup requests administrator access. The native title bar can be dragged, and the top-right controls minimize, maximize/restore, and close the window.

Bundled utilities are extracted to a per-user package directory under `%LOCALAPPDATA%\xOCD\Toolbox\Native\Packages`. The embedded archive and every extracted file are checked against their compiled SHA-256 manifest. No activation server, license key, machine-bound ownership marker, or separate protected launcher is required.

Users do not need separate installations of DDU, NVCleanstall, NVIDIA Profile Inspector, or ISLC. Toolbox prepares the embedded copies and launches the appropriate utility when its action is selected. A previously verified newer utility copy can also be reused. The actual NVIDIA driver package still downloads when selected, and vendor runtime requirements (for example .NET Framework for the original utilities) still apply. The native Toolbox does not require .NET for its own interface or engine code.

The shipped DDU and Profile Inspector configurations target .NET Framework 4.8. That Windows prerequisite must be present for those utilities; a .NET installer is not included. Live driver discovery and driver downloads require an internet connection. The NVIDIA Control Panel action uses an existing installation or attempts its verified WinGet installation path; if neither Control Panel nor WinGet is available, it reports that Control Panel needs to be installed.

The application does not apply optimizations at startup. Select an action in its workspace to run it. A running operation owns the mutation slot; the main window cannot be closed during it. Hiding the GPU progress window does not terminate a driver installation. The operation window reports actual stages, elapsed time, logs, and the verified result.

New session results are stored under `%LOCALAPPDATA%\xOCD\Toolbox\Native\Sessions`. Existing engine-specific backup and settings locations are preserved where their formats are compatible. The source retains the original configuration templates and vendor assets.

## Native tool modules

| Workspace | Implementation |
| --- | --- |
| Overview | Native hardware inventory and workspace navigation. |
| Windows Repair | Native registry/service/task operations, saved states and readback, personal settings, VALORANT checks, individual controls, and Windows servicing commands. |
| GPU Studio | Verified vendor preparation, live compatible driver selection, DDU/installer orchestration, NVIDIA profile and display handling, rollback state, and Control Panel launch. |
| COD Config Installer | Exact embedded templates, native CPU/topology selection, game discovery, first-seen backup, file verification, restore, and guarded shader-cache cleanup. |
| Debloat Tool | Native AppX inventory/removal and registered desktop uninstallers, with separately reviewed leftovers. |
| ISLC Setup | Native configuration, memory-based presets, startup setup, launch, and revert. |
| PC Health Center | Hardware, memory, storage and reliability evidence; native CPU and NVIDIA telemetry; optional signed sensor-support installation. |
| Cleanup | Category review, expiring per-user review tokens, file identity checks, and separate execution of the selected cleanup. |

Driver versions come from NVCleanstall's current compatible catalog when the workflow opens it. There is no frozen driver-version list. A newly published NVIDIA release becomes selectable when that upstream catalog exposes it for the detected hardware; this is not a guarantee that every release will appear within an hour.

## Notices

NVIDIA's notice is in `licenses/NVIDIA-NVML-LICENSE.txt`; retain its full disclaimer and U.S. Government End Users Notice when distributing this source or documentation. Other third-party notices accompany their sources and vendor payload directories. No private signing key is included. This build does not add an Authenticode signature to the Toolbox executable.
