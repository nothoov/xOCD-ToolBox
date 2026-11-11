## Startup update check

Toolbox checks the latest published release in [nothoov/xOCD-ToolBox](https://github.com/nothoov/xOCD-ToolBox) once when the main application opens. The check runs in the background after startup and does not repeat when changing tabs. Helper processes do not perform it. An available update produces a notice and a **View update** action in Overview; no EXE is automatically downloaded or installed. Missing releases, an offline connection and API errors remain quiet status messages, without blocking the application or being reported as up to date.

The visible version stays **v0.1**. An internal build number in `data/app-release.json` distinguishes successive downloads. The same release identity is compiled into the checker and embedded in the EXE. Release preparation verifies that identity and writes `xOCD-Toolbox-update.json` with the exact EXE size and SHA-256. See `docs/github-updates.md` for the first release and later updates. This application check is separate from the existing **Check & update tools** action for bundled utilities.

## Latest fixes in v0.1

This release addresses the reported Control Panel welcome-page stall after a successful driver installation. The exact recovered `xOCD Toolbox(1).exe` GPU script is the reference. The native worker reads NVIDIA's `SysTreeView32` task labels, selects the exact preview-settings task, confirms the selected item and sends Enter to open the page. It then checks the actual Advanced 3D radio controls and Apply result. As in the reference, native button notifications support the inactive background dialog. Actions are dispatched once; read-only readiness checks cannot replay them. Profile import, fresh-session Advanced 3D verification and independent final profile readback remain required.

The background controller now recognizes its own parked main Control Panel window by its captured identity and original window style. Adding `WS_EX_TOOLWINDOW` for background presentation no longer makes that same main window fail the panel's helper-window check. Routine Back, Forward, Home and Help navigation does not surface the main panel. Real secondary dialogs, unknown actionable content and errors remain accessible. Window-destroy notifications revoke identity immediately and defer presentation cleanup to the serialized provider owner, avoiding concurrent access to the presentation maps.

Both the reference and native workflows use DDU's **Clean and do NOT restart** mode before the prepared NVIDIA installer. The bundled DDU warning explicitly identifies black screen as a possible issue with that mode. This release does not claim to eliminate display loss or to have measured the reported black interval. It records eleven bounded workflow durations, including DDU exit to successful installer launch, in `audit.driverHandoffTiming` and the copied run result. Existing cleanup, package-integrity, device-readiness and installation checks are preserved; no new wait, reset or restart is added. See `docs/gpu-display-handoff-v0.1.11.md` for the evidence and timing definitions.

During driver replacement the GPU summary labels its existing snapshot **Last checked driver**, and the progress/confirmation text explains that the display may stay black until the replacement driver loads. If a driver was already verified but setup stopped afterward, the existing **Finish GPU setup** recovery action completes the remaining settings using fresh checks, without another cleanup/install cycle.

Windows file version: **0.1.0.0**. The native interface, logo, startup without Skip intro, utility payloads and absence of xOCD activation are retained. The public version is restored to v0.1 while the new startup release check uses a separate internal build number. Validation covers portable policies, extracted production code with controlled providers, a native cross-build and package inspection. Windows GUI, WinHTTP, GPU hardware and vendor programs were not run here; `validation/build-report.json` records the actual coverage and limits. Broader reference parity limitations documented below remain outside this targeted correction.

## What changed in v0.1.10

The exact supplied `xOCD Toolbox(1).exe` (version 13.0.26.1, SHA-256 `e9fe1d168c48f6bb92e6e120bbc049d076b3f0cc98e045f5f1cd7b3a1ba23ee5`) was recovered and statically unpacked. Its package authentication, signed manifest and all 421 extracted runtime files were verified. The actual GPU, Windows, Debloat, ISLC and gateway scripts and original COD method bodies were used for this comparison. This supersedes earlier audit limitations that treated the backend as inaccessible. No reference executable or vendor utility was run during extraction.

NVCleanstall now uses the reference's rendered, off-screen, non-activating background presentation. Its HWND is not hidden or minimized while UI Automation needs its controls. Window bounds and presentation flags are restored when a real secondary prompt needs attention. The action worker and background observer share a coordinator; the observer no longer walks the entire automation-owned wizard alongside catalog enumeration.

Catalog readiness and driver/MSI choices reacquire the captured window and reread a complete snapshot after a timeout or stale peer. Reads have fixed deadlines and cancellation/process/window identity checks. The list gets the reference's expansion settling interval. Selection is issued once, with separate read-back; transient reads cannot replay a driver action. Actual NVCleanstall errors are checked during download/build waits as well as catalog selection. Failures retain the UI Automation error name and hexadecimal code.

The profile workflow now imports once, then opens a fresh Control Panel to apply and verify Advanced 3D mode. A separate read-only native worker verifies that the final panel session retained the requested OpenGL, preferred-refresh and BO7 settings. A failed or uncertain import cannot proceed into the panel or display changes.

After a single Microsoft Store installation attempt, Control Panel acquisition now allows up to 30 seconds for current-user registration to appear, with cancellation checks and no duplicate installer launch. This restores the original's readiness wait instead of treating a delayed AppX registration as an immediate failure.

COD configuration now matches the original final prepared-byte hash verification and rollback scope, including failures during the final status read. Debloat supports a selected application's registered Windows PowerShell `-File` uninstaller when the exact Windows host, unchanged registration and app-owned script can be verified. It still requires a real uninstall result. The Privacy card restores the original feedback-period deletion, and Notifications includes the original ten ContentDeliveryManager flags for loaded ordinary-user profiles. Both use first-seen backup, live read-back and undo.

Overview now exposes **Check & update tools**, connecting the existing official-vendor updater to the native application. DDU, NVCleanstall, ISLC and NVIDIA Profile Inspector get separate version/results rows; a failed check or cancellation preserves the outcomes already reported. The supplied reference's application release feed is disabled and has no URL, so this button updates bundled utilities, not the Toolbox application itself.

All 133 bundled utility files are byte-identical to the supplied reference, as are the four COD template resources. The native interface, toolbox logo, startup animation without Skip intro, and absence of xOCD activation are retained. See `docs/reference-v0.1.10/` for per-module evidence and remaining differences. Windows file version: **0.1.10.0**.

**Remaining parity limit:** the original launcher uses the managed LibreHardwareMonitor sensor tree for broader AMD/Intel GPU, motherboard and cooler coverage. The current native health backend uses its native CPU/PawnIO, NVIDIA and Windows providers; existing LHM/HWiNFO fallback is CPU-only. Those broader original sensor categories have not been ported by this release. The exact provider DLL and dependencies were recovered and inspected, but the original launcher has no supported headless health mode. This release does not claim complete sensor-provider equivalence or live Windows/hardware validation.

Portable verification is reproducible with `python tools/run_portable_checks.py`. It exercises policies and extracted production code with controlled providers; it does not install drivers or execute Windows/vendor utilities. `validation/build-report.json` records the build and verification actually performed for the delivered executable.

## What changed in v0.1.9

Removed the startup **Skip intro** button and the Enter/Space/Esc skip shortcuts. The startup animation now finishes automatically before the main window opens, together with the existing tool verification and hardware discovery. The Close button and Copy details action remain available. The source preview matches the updated screen. Windows file version: **0.1.9.0**.

## What changed in v0.1.8

This release updates background presentation and startup cache recovery. The user confirmed that the v0.1.7 GPU workflow works, requested that routine NVCleanstall preparation stay behind xOCD's progress display, and then reported that startup could not preserve its previous vendor cache.

The background controller now inspects WPF controls through read-only UI Automation as well as native child windows. Routine progress with only Cancel can remain hidden; errors and actual user choices remain accessible. NVCleanstall's automation client disables automatic focus before invoking its controls, with its existing operation settings and provider timing preserved. The driver component policy, package preparation, DDU, installation, profile setup, rollback and bundled utilities are retained.

Startup now distinguishes expected DDU settings/log changes from modified program files. If a cache genuinely needs replacement, the old directory can remain in place while a verified new generation is prepared. Isolated GPU workers use the same pinned generation as the parent app. Backups, recovery information, and existing tool copies are preserved.

See `docs/gpu-background-v0.1.8.md`, `docs/startup-cache-v0.1.8.md`, and `validation/build-report.json` for the exact scope and validation limits. Windows file version: **0.1.8.0**. No xOCD activation is required.

## What changed in v0.1.7

GPU inventory and driver-cleanup verification now use current native SetupAPI/Configuration Manager device bindings instead of joining WMI signed-driver inventory. The check captures the exact PCI devices, installed service/INF/provider/version, device status, and restart flags. A present Microsoft Basic Display binding and an explicitly unbound GPU are recognized separately. Missing hardware, unreadable properties, changing bindings, an NVIDIA driver still attached, and actual device problems remain explicit states. Two stable cleanup observations and a fresh installation-boundary check are required before installing the prepared package.

The exact bundled DDU 18.1.5.7 was inspected without executing it. Its command-line Windows driver-search option was not being activated by the native caller; it is now passed, with the previous Windows setting captured and restored by an owned recovery journal. Driver-search protection remains active even if Windows Update was already paused or disabled. Native process ownership is retained until DDU/the installer actually exits; presentation failures and expected-duration overruns cannot release the workflow or restore temporary settings while the vendor process is still running.

Current-run DDU process results, the original log bytes, and per-device observations are saved before deciding whether installation can continue. Results link the DDU report as well as package verification. Windows-required restarts are distinct from restart recommendations. A selected driver registered pending reboot is retained for **Finish GPU setup** after the reboot, and profile/display changes require an operational NVIDIA device.

The all-tabs audit also fixed lost DISM restart receipts in component cleanup, provisioned-app removal, and Windows settings. Restart evidence survives later failures without turning an unverified removal into success. Cancelling app removal prevents a further per-user fallback or the next package removal. Exact registry snapshots retain the second native read's actual byte count.

The native UI, Toolbox case logo, dark orange/cyan theme, configuration templates, profile ABI fixes, isolated NVIDIA worker, and all bundled vendor utilities are retained. Windows file version: **0.1.7.0**. No xOCD activation is required.

The specific working reference remains `xOCD Toolbox(1).exe` version 13.0.26.1. This release compares its accessible frontend contracts and bundled utilities; it does not claim that its protected backend was transplanted or that every Windows/hardware action was executed here. See `docs/reference-v0.1.7/all-tabs-reference-audit.md`, `docs/gpu-cleanup-v0.1.7.md`, and `validation/build-report.json` for scope, evidence, and remaining limits.

## What changed in v0.1.6

This release repairs a concrete crash-capable NVIDIA profile API mismatch. The native wrapper previously selected extended GetSetting/SetSetting entry points but invoked them with the shorter public-API signatures. The corrected wrapper supplies the extended read's output pointer and the extended write's two reserved arguments, and keeps the public fallback signatures separate. Text-profile import and backup now require the matching text API pair; the binary-file fallback has been removed.

Profile import, preferred-refresh changes, and NVIDIA display capture/apply now run in an isolated native child of the same EXE. The application accepts a result only after the exact child exits normally and returns the matching complete response. A native access violation, timeout, malformed result, or unverified partial mutation cannot become success or trigger the remaining display changes. The main Toolbox stays available to present the failed run and its recovery information. Standalone Apply profile also pauses and drains live telemetry during the operation.

Profile recovery records begin before the first NVIDIA call, retain the backup location, and record each pending/returned native call. Ordinary profile failures restore the saved database where possible and verify it through a fresh export; an unverified restore is reported accurately. Interrupted workers are not automatically retried. The approved profile, BO7 mappings/ReBAR sequence, preferred refresh policy, native UI, startup animation, branding, and all 133 bundled vendor files remain intact.

The latest supplied working `xOCD Toolbox(1).exe` is the exact v13.0.26.1 package recorded in the earlier frontend project. Its declared workflow was used as the reference; this release does not claim to transplant its protected backend. See `docs/nvidia-profile-crash-v0.1.6.md`, `docs/reference-v0.1.6/`, and `validation/build-report.json` for the code evidence and validation limits. Windows file version: **0.1.6.0**. No xOCD activation is required.

## What changed in v0.1.5

This revision fixes the GPU preparation windows surfacing during automatic work and replaces the brittle NVIDIA Control Panel window/readiness check. It also adds **Finish GPU setup** for a driver that Windows already verified but whose remaining setup stopped. The Windows file version is **0.1.5.0**. The application remains native C++20/Win32 and requires no xOCD product activation.

Routine NVCleanstall, DDU, installer, and automatic Control Panel windows are managed throughout the operation. Real prompts and errors remain visible, and explicit Open actions still open their tools. Control Panel verification uses the actual selected window and native or accessible task navigation, saves diagnostics, and preserves real advanced-mode selection plus fresh-session readback.

The supplied v0.1.4 report confirms successful package trust checks, DDU cleanup, and installation of 617.42. Its failure was in Control Panel initialization, before profile/display setup. Those remaining steps now have independent results. After the required restart, Finish GPU setup can complete them for the already installed driver using fresh hardware and monitor checks, without another DDU or driver installation.

See `docs/gpu-background-recovery-v0.1.5.md` for behavior, recovery steps, source references, and validation limits. The two readable older TaC9 archives contain PowerShell/WinForms and a manual GPU workflow; they are not the newer protected automatic backend. `docs/reference-v0.1.5/` records that comparison. This build does not claim an exact transplant of inaccessible TaC9 code.

## What changed in v0.1.4

This release adds the original xOCD startup animation and revises the GPU package verification and returned phase evidence. The Windows file version is **0.1.4.0**. xOCD remains its own native application with no product activation key, sign-in, or activation server.

The new 3.8-second native intro assembles orange and cyan geometric blocks into an X with silver OCD lettering. It uses the existing dark wallpaper and Toolbox emblem. Skip (or Enter, Space, or Escape from the intro) skips only the animation; the main window opens after actual bundled-tool verification and hardware discovery. Real preparation status is visible, startup errors can be copied, and closing requests cancellation at the next worker checkpoint. The main window prepares and paints its first page before the splash is dismissed. Background workers are joined on normal and exceptional application exits.

GPU package checks retain Windows signature and expected-publisher validation, with more detailed trust diagnostics. Reported GPU phases now distinguish package preparation from DDU, installation, and final verification. A failed package check does not mark the final Verify phase as failed or claim a partially installed driver merely because preflight completed. Explicit before-DDU evidence and restoration of the temporary Windows Update pause appear in the saved result.

See `docs/startup-gpu-v0.1.4.md` for changes and validation limits, and `docs/reference-v0.1.4/parity-report.md` for the feature comparison against the accessible supplied reference. The comparison cannot establish exact behavior hidden inside the reference application's protected payload. There is no new application-update or NVIDIA-preset feed in this release.

## What changed in v0.1.3

This revision reviews the settings and recovery paths behind the interface, including the complete Windows catalogue, Personal Settings, application removal, advanced controls, GPU settings, COD profiles, ISLC, and the Health and Cleanup controls. The release records distinguish source review, portable regression checks, native cross-compilation, and Windows behavior that has not been executed here. See `docs/settings-audit-v0.1.3.md` and `validation/build-report.json` for the evidence and limitations.

Personal Settings now avoids unnecessary registry writes when the exact saved state is already present, compares persistent keyboard settings without treating temporary pressed-key state as a failure, and handles already-satisfied or pending Recall changes. An incomplete same-choice retry keeps its original recovery journal. Restore tracks attempted changes and preserves recovery information across partial failures. The result identifies individual failed settings, warnings, completion counts, and saved paths.

Debloat now resolves registered uninstall commands with correct executable boundaries, preserves documented MSI patch-removal semantics, and can use the registered standard uninstaller if the quiet command cannot be prepared before launch. After a successful parent exit, it waits for removal of the same captured application registration. Restart codes or a changed registration do not prove removal. Per-app outcomes, native errors, and separate leftover-review results are saved in a run report. The original Bionic failure is not claimed reproduced without its Windows run data.

Advanced controls gain independent restore actions. IoLatencyCap is scoped to verified present Storport miniport drivers instead of a generic Storport registry key. The Core Isolation control preserves policy files, managed settings, firmware locks, unrelated security values, and inactive control sets. Its local overrides and prerequisite changes have recoverable scoped journals. Advanced descriptions no longer call Enhanced TSC synchronization the Windows default or promise an unmeasured performance gain.

Individual setting Apply and Restore actions use separate capabilities. Refreshing service, registry, GPU rollback, and COD path data disables actions that would otherwise use stale state. Completed operation dialogs provide wrapped, selectable diagnostics, Copy result, the activity view, and a validated saved-result folder action. Activity timestamps use elapsed time from the start of the run.

Catalogue recovery now keeps separate originals for each power plan and adds first-seen states for newly installed components, input devices, tasks, and network bindings. Compound changes use a frozen target list. Optional-feature inventory failures remain errors; accepted pending changes require a restart. Game Bar verification reads its actual handlers. The visual-effects card uses explicit Windows API pairs, captures values before mutation, and verifies the final state.

GPU display results use fresh provider readback. ISLC checks all configured fields, refuses impossible memory presets before writing, and separates a running configured process from internal monitoring state that it cannot independently observe. MSI uninstall commands suppress automatic restarts while preserving patch-removal arguments.

The native x64 application retains the Toolbox case logo, dark background, orange/cyan theme, original configuration payloads, and bundled vendor utilities. The Windows file version is **0.1.3.0**. This revision does not establish that every Windows or vendor operation succeeds on every machine; refused changes and unverified outcomes remain visible failures or review states.

## What changed in v0.1.2

This frontend and backend audit fixes stale query delivery across selection changes, Home/End routing on navigation tabs, Services selection and saved Windows Search preference handling, and the verification used when opening bundled utilities. Failed or paused telemetry is labeled explicitly, older inventory snapshots cannot replace newer live measurements, and incomplete Event Log evidence cannot silently appear as a clean result.

Windows repair dialogs now retain the specific phase that needs review and reconcile their final stage marks against returned command evidence. Advancing from one step to the next no longer leaves a failed or unrecognized repair phase marked as verified in the final result. A real SFC report of unrepaired files remains an unhealthy result; this update does not force a successful repair or claim to fix the Windows files identified by that report.

The native x64 release includes the same Toolbox case logo, dark background, orange/cyan theme and vendor payloads. See `docs/frontend-backend-audit-v0.1.2.md` and `validation/build-report.json` for audit coverage, regression checks and the remaining Windows integration checks. The Windows file version is **0.1.2.0**.

## What changed in v0.1.1

This repair-reporting update gives Full Windows Repair, DISM, and SFC their actual servicing stages. A completed, recognized scan that still reports unrepaired files is shown as **Scan complete — issues remain**, with an amber warning and completed scan progress. It remains an unhealthy result; the application does not convert it to a successful repair. Unverified results and commands that did not finish are shown separately.

Repair activity timestamps show elapsed time from the beginning of the run. Empty servicing output is ignored, while native percentage updates are grouped within their phase. The main **Open repair logs** button opens the actual Windows repair-log folder, and completed repair windows provide a guarded shortcut to that run's folder.

Current-run transcripts and structured results retain command details, native exit codes, completion evidence, timestamps, and log locations. SFC classification uses supported terminal messages from the current command rather than isolated CBS fragments. Interrupted commands do not silently continue the remaining repair sequence. A reported pending restart remains visible and is never performed automatically.

The xOCD Toolbox logo, dark background, existing workflows, bundled utilities, and v0.1 layout improvements are retained. The Windows file version is **0.1.1.0**. See `docs/windows-repair-results.md` and `validation/repair-reporting-v0.1.1.json` for the repair-result contract and targeted checks.

## What changed in v0.1

The supplied **xOCD Toolbox case logo** is now the application emblem and the multi-size Windows EXE icon. The existing dark orange/blue background remains unchanged. The version displayed in the UI is **v0.1**; the Windows file/product version is **0.1.0.0**.

The presentation pass covers all eight sections and the secondary Windows workspaces. Overview uses measured hardware cards and eight complete workspace rows. Repair, GPU Studio, COD configuration, Debloat, ISLC, Cleanup, Services, and Registry use consistent rounded dark cards, readable values, and aligned actions. Native inventory tables retain their keyboard and checkbox behavior with dark headers, taller rows, and matching checkbox hit targets.

Navigation keeps its header controls instead of recreating them on every selection. Selected tabs, pointer hover, and keyboard focus have distinct appearances. Arrow keys and Home/End work within navigation groups. Page rebuild requests are coalesced and wait until native callbacks finish, including nested report-save dialogs. Unrelated background-query results no longer replace the current page. Scroll targets requested by a finding or Back navigation are applied against the new layout.

Charts and their background are composed into a completed frame before presentation. Only changed readings and chart regions repaint on telemetry updates; the periodic UI timer does not invalidate the whole page. The existing elapsed-time smooth page scrolling, precision wheel input, Windows wheel settings, immediate scrollbar dragging, and reduced-animation preference remain in use.

PC Health Center restores structured Overview, Sensors, Storage, Memory, and Reliability layouts. Clickable findings select and reveal known volumes or physical disks, or open the matching reliability category. Physical device IDs distinguish identical drive models. The capacity ring uses actual counters; physical-device reliability is shown separately without inventing a volume-to-device mapping. Unknown sensors and unavailable evidence stay labeled.

The reliability reader retains up to 20 recent details in each supported event category, so a busy System log cannot consume the Application log's evidence budget. It still counts the scanned observation period, reports partial sources, and bounds retained details to 100 events. Native event record IDs preserve exact selection, and the evidence dialog can show the complete bounded provider message rather than a 220-character preview.

Operation windows use one draggable custom titlebar, buffered text, clean activity rows, smoother status animation, real timings, and actual worker progress. Single-stage operations use a compact reported-progress strip. Final success still requires the native result and a zero exit code.

The original GPU preparation options, DDU sequence, live NVCleanstall catalog selection, profile handling, ISLC workflows, power-plan integrity checks, and all bundled vendor utility bytes are retained. DDU, NVCleanstall, NVIDIA Profile Inspector, ISLC, the extractor, and the optional PawnIO installer remain their vendors' utilities. Some external utilities use .NET; the Toolbox application and its owned engines are native C++20/Win32. This build has no owned managed launcher, WebView frontend, or runtime PowerShell engine.

Community/Discord navigation, activation keys, and the former Check for updates button remain absent. A GitHub release-update feed is not configured in this revision.

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

## Build on Windows

Requirements are Visual Studio 2022 C++ Build Tools (Desktop development with C++ and the Windows SDK), CMake 3.24 or newer, and Python 3.9 or newer. Python is used only to construct the embedded resource archive at build time.

Extract the complete source ZIP, including `payload`, `assets`, `licenses`, and `third-party`. From that folder:

```bat
Build.cmd
```

To request prerequisite installation through Windows Package Manager:

```bat
Build.cmd -InstallPrerequisites
```

To also build and run the available portable policy tests on Windows:

```bat
Build.cmd -PolicyTests
```

The expected MSVC output is `build-windows\bin\Release\xOCD Toolbox.exe`. `Build.ps1` is a developer build script; the resulting Toolbox does not invoke it.

Direct CMake configuration is also available:

```bat
cmake -S . -B build-windows -G "Visual Studio 17 2022" -A x64
cmake --build build-windows --config Release --parallel
```

## Cross-build used for this deliverable

The supplied EXE was cross-compiled with the pinned GCC/MinGW-w64 x64 toolchain. It was not built with MSVC. The project also includes the MSVC build configuration for Windows, which has not been executed in this environment.

The private Linux toolchain can be restored from the package receipt without installing it system-wide:

```sh
python3 tools/cross/restore_native_tooling.py
tools/cross/bin/cmake -S . -B build-cross -G Ninja \
  -DCMAKE_TOOLCHAIN_FILE="$PWD/tools/cross/mingw-x64.cmake" \
  -DCMAKE_BUILD_TYPE=Release
tools/cross/bin/cmake --build build-cross --parallel 3
```

The restore script downloads hash-pinned official Debian packages and uses `dpkg-deb` to unpack them. It requires Linux x64, Python 3, and network access. Cross-building does not execute the Windows program. The C++ runtime is statically linked in the supplied MinGW build.

## Validation and limits

See `validation/build-report.json` in the delivered source bundle for the exact final binary hashes, PE architecture/import checks, embedded resource checks, route coverage, and policy-test results.

The source was compiled and linked, and the portable policy tests were run. The Windows application, its UI, driver installations, registry/service mutations, and hardware-specific operations were **not executed in this environment**. This revision still needs validation on Windows. The previous v6 package is preserved separately.

Sensor support depends on the CPU, GPU, firmware, installed driver, and provider access. The native CPU provider is carried forward from the supplied xOCD 2.1.0 source. NVIDIA readings use native installed driver libraries and, where supported, the signed PawnIO module. Unsupported or stale values remain unavailable. This conversion does not bundle the old managed general motherboard/RAM sensor stack; it does not guarantee every former motherboard, fan, or DIMM sensor row.

Native WinRT AppX operations, Delivery Optimization's installed CIM provider, live NVCleanstall UI automation, NVAPI display/profile changes, and first-run elevation still need Windows validation. An unavailable provider or an unverified result is reported rather than treated as success. Vendor UI changes or unsupported hardware can require an update to the corresponding adapter code.

## Source and notices

`src`, `include`, and `tests` contain the application source and policy checks. The four COD files and both power-plan files are the supplied original payloads. `data/windows_catalog.json` preserves the existing card/service/control definitions; legacy `.ps1` strings there are stable card identifiers and provenance, not executable script dependencies.

`src/telemetry/cpu.cpp`, its two included implementation files, and `include/xocd/cpu.hpp` are the supplied xOCD native CPU provider. The signed sensor module assets are retained unmodified. The PawnIO module license and corresponding module source archive are included under `licenses`.

NVIDIA's notice is in `licenses/NVIDIA-NVML-LICENSE.txt`; retain its full disclaimer and U.S. Government End Users Notice when distributing this source or documentation. Other third-party notices accompany their sources and vendor payload directories. No private signing key is included. This build does not add an Authenticode signature to the Toolbox executable.
