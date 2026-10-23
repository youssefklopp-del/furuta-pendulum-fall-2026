# Furuta Pendulum Fall 2026

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
