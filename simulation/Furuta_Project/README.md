# Furuta Pendulum - Clean Project

## Six Core Live Scripts and Two Supplements

This project has eight Live Scripts: the six core study files and two new supplements. There are no duplicate `.m` files and no external helper script.

Run the files in this order:

1. **Furuta_Mathematical_Model.mlx** - physical parameters, coordinates, motion, energy, nonlinear equations and Simscape validation.
2. **Furuta_State_Space.mlx** - upright and downward equilibria, linearization, A/B/C/D, poles, controllability, observability and transfer functions.
3. **Furuta_PID.mlx** - PID gains, stability, Simulink implementation, simulation and results.
4. **Furuta_Pole_Placement.mlx** - response targets, pole selection, K, implementation and simulation.
5. **Furuta_LQR.mlx** - Q/R, K, the Riccati check, implementation and simulation.
6. **Furuta_Comparison.mlx** - common plots and one performance table for all three controllers.
7. **Furuta_Submission_Notes.mlx** - clear assumptions, physical parameter sources, concise design justification, explicit nominal tests for all three controllers, and phase boundaries/review limits.
8. **Furuta_Controller_Tuning.mlx** - step-by-step PID, pole-placement and LQR candidate searches, ranking, and optional nonlinear shortlist checks.

The six core files include saved results from actual MATLAB runs. The two supplements keep the existing six files and accepted gains unchanged. Historical tuning evidence is labelled separately from new candidate searches.

Submission Notes runs the actual common nominal test with explicit pulse edges, amplitudes, actuator limit, equilibrium, gains and run time. It uses a temporary saved-plant copy to preserve an open model with unsaved edits. This adds a reproducible test entry point; it does not rewrite the original three controller files.

Controller Tuning uses 12 PID candidates (9 P/D choices plus 3 integral trials), 9 pole sets and 9 nearby LQR weight choices. These are small teaching searches, not a repeat of the historical large grids. Its nonlinear option is off by default. A linear shortlist is not an accepted replacement gain. This script never overwrites Accepted_Controller_Data.mat.

Both supplements were checked in MATLAB. Submission Notes reproduced the accepted nominal responses. The tuning screen completed all 30 candidates. Its optional nonlinear path was also tested using a disposable copy with the option enabled. Results are in `results/Additional_Verification.json` and `results/Tuning_Nonlinear_Checks.csv`.

The shortlisted PID candidate passed the nominal pulse but failed the stronger-pulse arm-settling limit. It was not promoted to the accepted design. `Inf` in a settling-time column means the response did not settle within the run. The nonlinear tuning results describe shortlisted candidates, not automatic replacements for the accepted controllers. The delivered tuning file keeps `run_nonlinear_checks=false`; set it to true to repeat those six simulations.

## How to Run

Unzip the package. Set **MATLAB Current Folder to the Furuta_Clean_Project folder**, then open the files. You do not need to copy files into the old Downloads project. Run the first six in order for the original study; use the two supplements for documentation, explicit tests and tuning.

Required tools: MATLAB, Simulink, Simscape Multibody and Control System Toolbox. The first two files also need Symbolic Math Toolbox. The calculated data is already saved, so you can run the controllers without deriving the equations again if the physical parameters have not changed.

```text
Furuta_Clean_Project/
├── Furuta_Mathematical_Model.mlx
├── Furuta_State_Space.mlx
├── Furuta_PID.mlx
├── Furuta_Pole_Placement.mlx
├── Furuta_LQR.mlx
├── Furuta_Comparison.mlx
├── Furuta_Submission_Notes.mlx
├── Furuta_Controller_Tuning.mlx
├── models/
│   ├── Furuta_Study.slx
│   └── Furuta_Validation_Study.slx
├── data/
│   ├── Physical_Parameters.mat
│   ├── Nonlinear_Model.mat
│   ├── Linear_Model_Data.mat
│   └── Accepted_Controller_Data.mat
├── geometry/                       Three CAD files
└── results/                        Saved runs, plots and comparison table
```

The `.slx`, `.mat` and STEP files are required models and data. They are not extra Live Scripts. All controllers use one Linear_Model_Data.mat file.

## Main Changes

- Each file loads data directly with `load`. It does not use Furuta_Controller_Study or plant.A.
- The first two files show the derivation in seven clear steps. The energy equations and matrix calculations remain visible. The CAD model has not been replaced with a different point-mass model to shorten the code.
- CAD data was converted to SI units once and saved in Physical_Parameters.mat. These are parameters from the saved model, not measured hardware identification results.
- Each controller file includes its design, stability check, implementation and simulation. Short performance functions stay inside that Live Script.
- The PID block has one state input and five clear paths: Arm P, Arm I, Arm D, Pendulum P and Pendulum D. Integral torque is limited to +/-0.002 N m. Actuator torque is limited to +/-0.01 N m.
- Inactive integral tracking was removed. **Select the controller before each new run.** This version does not provide smooth controller switching during a run. The active PID response is preserved.
- The copied models have new names, so they do not conflict with the original Furuta_Control model. Original Downloads files and unsaved model edits were preserved.

## Verification - 15 November 2026

All six Live Scripts were run and saved in MATLAB. See results/Verification.json.

- Maximum change in A: about 1.14e-13. Maximum change in B: about 4.55e-12.
- Controllability and observability ranks are both 4. Downward-equilibrium analysis is included.
- The independent analytical/Simscape test gave maximum angle errors of about 6.80e-8 and 5.14e-7 rad, and velocity errors of 2.56e-7 and 5.32e-6 rad/s. This was a 0.5 s test using ode45 and interpolated samples. These numbers belong to this test, not the older validation method.
- All three controllers have stable local closed-loop poles. The new project produced these results:

| Controller | Peak pendulum angle | Pendulum settling | Arm settling |
|---|---:|---:|---:|
| PID + pendulum PD | 2.7646 deg | 0.934 s | 6.907 s |
| Pole Placement | 3.0541 deg | 1.307 s | 1.338 s |
| LQR | 2.6749 deg | 1.388 s | 1.373 s |

All runs use the same +0.01 N m arm-torque pulse from 1.00 to 1.05 s and a 10 s duration. Settling time starts at the end of the pulse. The bands are +/-0.1 deg for the pendulum and +/-1 deg for the arm. No actuator saturation occurred in these nominal tests.

These controllers stabilize near upright. Swing-up, Stateflow and hardware control are separate tasks. Downward-equilibrium analysis is not a swing-up controller. The project requires LQR, but the five uploaded lectures do not explain its design in detail.
