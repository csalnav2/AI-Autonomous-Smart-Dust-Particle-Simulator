# Indoor mathematics: source map

This document explains source, not a new execution. Scientific evidence stays at the 00:45 UTC, 31 October 2026 snapshot. Paths below refer to the indoor GitHub package root.

## Application prototype

- `application/restored_assets/indoor_lab/self_flight.py`: lines 163–166, strain and stroke limit; 199–204 and 308–312, cycle averaging; 313–337 and 440–456, power budgets.
- `application/restored_assets/indoor_lab/room_flow.py`: lines 1–18 and 44–49, reduced two-dimensional airflow assumptions/defaults.

## Saved mechanical component study

- `research/revised_passive_pitch/run.py`: lines 7–10 load history; 14–39 selected drive, geometry, tendon tension convention and coupled equations; 42–43 constraints; 56–58 solver tolerances and dense output; 71 reported metrics.
- `research/revised_passive_pitch/sources/mechanism.py`: lines 11–21 reference frequency and stable tip mapping. The older drive inside `mechanism.run` is not the selected confirmation's drive.
- `research/revised_passive_pitch/confirm.py`: selects the separately saved L40T24/r6 confirmation cases.
- `media/chain/render_chain.py`: lines 52–55 display interpolation; 83 actuator curvature; 114 hinge twist.

Units and short derivations appear in `docs/INDOOR_APPLICATION_EXPLANATION.md`, `docs/INDOOR_RESEARCH_VIDEO_EXPLANATION.md` and `docs/MATH_AND_TIMING.md`. The application model, reduced research model and display interpolation are separate layers.
