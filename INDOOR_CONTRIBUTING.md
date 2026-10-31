# Collaborating on the indoor Smart Dust work

This project welcomes careful model, numerical and reproducibility review. It has not demonstrated a fabricated 300 µm flying robot. The target body size is not the full assembly envelope.

## Keep the two models separate

- The application is a six-agent exploration and sensing prototype with hypothetical cycle-averaged flight, material and facility-airflow assumptions.
- The research study is a reduced actuator–transmission–wing calculation under prescribed voltage and a surrogate resistive load. Its video replays saved component states, not free flight.

## Useful contributions

1. Check equations, signs, units and source locations in the math explanations. In particular, distinguish the full tendon tension difference from the source's half-difference `td`.
2. Review component constraints, energy accounting and convergence without changing the existing gates to manufacture a pass.
3. Propose or supply measured material, hinge fatigue, aerodynamic and actuator data with provenance and uncertainty. Label synthetic examples explicitly.
4. Identify portability or dependency issues with a minimal reproducible report. Application source was statically inspected, not freshly runtime-qualified by this documentation export.
5. Improve captions and scientific visualization while keeping saved samples, timing, display interpolation and physical validation distinct.

## Reproducibility expectations

Before proposing a numerical rerun, identify the exact source/data hashes, configuration, dependency versions, resource ceiling, termination criteria and expected outputs. Do not overwrite frozen evidence. Save new runs and negative/null outcomes separately. A contribution or notebook upload is not permission to launch expensive experiments, operate hardware or publish findings on behalf of the project.

A useful issue or proposed change includes: question; affected file and lines; expected versus observed behavior; units and assumptions; evidence provenance; bounded test proposal; and remaining uncertainty. No account credentials, owner/tunnel URLs, session records or private keys belong in an issue or repository.

## Open checks

Calibrated aerodynamic lift and free-flight control, complete assembly geometry, material/fatigue qualification, and endurance remain unverified. The later native API check did not establish full numerical integration: its administrative timing exception remains distinct from the narrower interface result. See `docs/STATUS.md` and the original study reports.

Preserve original third-party notices. This contribution guide grants no new license and does not change ownership or authorize public posting.
