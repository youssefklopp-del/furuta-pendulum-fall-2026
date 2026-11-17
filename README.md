# Furuta Pendulum Fall 2026

## Current MATLAB study - November 2026

[Download the complete current project](https://github.com/youssefklopp-del/furuta-pendulum-fall-2026/releases/tag/project-study-2026-11-17) from the release Assets. Choose `furuta-pendulum-complete-2026-11-17.zip`, not the automatic Source code archive.

The package includes the nine Live Scripts, Simulink models, physical and linear model data, STEP geometry, controller results, tuning and pulse tests, original CAD, and reports.

Extract the whole ZIP. Set MATLAB Current Folder to `Furuta_Pendulum/simulation/Furuta_Project`, then open `models/Furuta_Study.slx`. Choose the controller before Run. Multibody Explorer and 1x pacing are enabled. Controller Live Scripts temporarily select their own controller; Comparison reads saved results.

Required: MATLAB R2026a, Simulink, Simscape, Simscape Multibody and Control System Toolbox. Re-deriving the model also needs Symbolic Math Toolbox.

- [Redesigned dynamics and state-space report](docs/Furuta_From_CAD_to_Control.pdf)
- [Mechanical drawing PDF](docs/modern%20conttrol.pdf)
- [Mechanical drawing DWG](docs/modern%20conttrol.dwg)

The controllers stabilize near upright. Swing-up and hardware validation are separate tasks.

## Earlier project documentation

The notes and older download below describe the previous package. Use the current release above for the latest MATLAB study.

# Furuta Pendulum Fall 2026

## Download the complete project

[Download all project files (ZIP, 237 MB)](https://github.com/youssefklopp-del/furuta-pendulum-fall-2026/releases/download/project-files-2026-10-25/furuta-pendulum-complete.zip)

The ZIP contains 634 files with the original `archive`, `cad`, `docs`, `results`, and `simulation` folders preserved. Extract the entire archive before opening CAD assemblies or MATLAB models. The folders in this repository contain download guides; the project files are in the ZIP release asset.

SHA-256: `E575138F89D5D596EF57EE72A9342849222F89D0AFA8CEDE016D6737C0A0189C`

Access follows this private repository’s permissions.

Rotary inverted pendulum project using Inventor, SolidWorks and MATLAB Simscape Multibody.

## Repository structure

| Directory | Contents |
|---|---|
| `cad/inventor/original` | Original Inventor project and available assembly dependencies, retaining internal directory layout |
| `cad/solidworks/simplified_assembly` | Simplified three-group CAD files and SolidWorks assembly |
| `cad/step_exchange/full_assembly_and_parts` | Full assembly and individual STEP exports |
| `simulation/multibody` | Saved Assem11 model, XML export, data script and associated STEP geometry |
| `results` | Existing CAD images, simulation images and videos |
| `docs` | Existing reports and component references |
| `archive/previous_week6_package` | Earlier analytical package and evidence; not the current Multibody plant |
| `archive/simulation_generated` | Preserved original caches and backups, not required for normal simulation |

## Open the current simulation

1. Use MATLAB R2026a with Simscape and Simscape Multibody.
2. Set the current folder to `simulation/multibody`.
3. Run `Assem1_DataFile.m` if the model requires its variables, then open `Assem11.slx`.
4. Check model callbacks and file references if the project was moved. Geometry and data companions are kept together.

The model represents a fixed base, rotating arm group and passive pendulum. The blue hub and rod form one rigid pendulum group. STEP exchange does not preserve Inventor constraints automatically. SolidWorks assembly portability has not been tested on a clean machine.

## Verification status

- Running Multibody plant and motor-interface model observed.
- Zero-command response reviewed in screenshots; final settling confirmed by the owner.
- Forward/reverse and pulse operation confirmed by the owner.
- Motor inductance, equivalent inertia and final friction values require identification or justification.
- Quantitative pivot-inertia/oscillation-period comparison was deferred.
- Older reports may describe earlier project states. They are preserved as history, not automatically endorsed as current results.

## File preservation

`FILE_MANIFEST.json` maps every original file to its new path and records SHA256 checksums. All files from the requested source directory are included, including historical backups and generated artifacts in the archive section. Original filenames are retained to reduce broken references. The source directory was not rearranged or deleted.
