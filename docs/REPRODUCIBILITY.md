# Reproducibility and evidence

## Packaging changes - 18 November 2026

- Sources were collected from `modern control submession 6&9` without moving or deleting the originals.
- The repaired `Furuta_Controller_Tuning.mlx` from the active working copy is included. Its missing local functions were restored and the Live Script completed with 13 outputs in the observed MATLAB session. This does not establish that optional nonlinear trials ran.
- Live Script model references were aligned with the supplied filenames: `Furuta_StudyF` and `Furuta_Validation_Study1`. Controller equations and gains were preserved.
- MATLAB caches, CAD lock files and automatic backups were excluded.

## Saved results are snapshots

The results folder contains evidence from different runs. In particular, the observed `Pulse_Sweep_Progress.csv` contained failed runs with an invalid `Pulse starts` path, while older summary files reported completed runs. Do not combine those files as one verified experiment. Regenerate the full sweep after confirming the current disturbance paths and topology; require all 30 trials to have `Completed=true`, inspect `ErrorMessage`, and check the plotted logged signals.

After edits to CAD mass, motor limits, pulse settings, controller gains or model wiring, rerun affected simulations and the comparison. Switching the model's manual controller selector does not regenerate saved comparison data. Scripted tests explicitly set their own selector and pulse values on temporary copies of the saved model. Unsaved edits are not copied.

The provided package has not been validated on a clean second computer. Model-reference updates made during packaging were statically checked, not followed by a full simulation rerun.

## Physical limits

This is a simulation study of stabilization near upright. Swing-up, real-time embedded control, motor electrical dynamics, parameter estimation and hardware validation are not established by these results. A torque input model is not a validated motor/driver model. The motor feasibility report is conditional on confirming the exact motor variant.

CAD translation used XML/STEP exports rather than URDF. The referenced original `Assem1.xml` and `Assem1_DataFile.m` were recovered from the earlier local XML export folder and included alongside matching STEP files in `simulation/Furuta_Project/geometry`. The saved models contain embedded model-workspace data, but also retain an old absolute `WSSourceFileName` metadata value. If MATLAB requests the original data file, select the bundled `geometry/Assem1_DataFile.m` and confirm the workspace source configuration. Portability has not been validated on a clean machine.
