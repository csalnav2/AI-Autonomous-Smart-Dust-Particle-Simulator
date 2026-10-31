# Indoor component chain: equations and timing

These equations summarize the packaged reduced model, not a full piezoelectric finite-element model or an airflow simulation.

## Voltage and time

`V(t) = A(t) sin(2π f t)`, with `f ≈ 266.819 Hz` in the selected case. `A(t)` rises from 0 to 4 V over 0–40 ms, then to 4.1 V at 44 ms and remains there. The cycle period is `1000/f ≈ 3.748 ms`.

Let `s(z) = clip(z,0,1)^2 [3 − 2 clip(z,0,1)]`. The selected resistance multiplier is

`g(t) = 1 + 3 s((t−0.080)/0.010) − 3 s((t−0.140)/0.010)`.

It rises from 1 to 4 at 80–90 ms, holds at 4 for 50 ms, falls at 140–150 ms: **70 ms total**. “4×” means strength, not duration. It is a prescribed load episode, not square-wave voltage or sensed air-pressure feedback.

Refined Radau maximum step is `hmax = 1/(fref × 160) ≈ 21.0817 µs`, with `fref ≈ 296.4657 Hz`. Thus `10 ms/hmax ≈ 474.34`; spanning a 10 ms interval with steps no larger than this requires at least 475 steps if counted across that interval. Adaptive steps may be smaller. These are resolution comparisons, not recorded internal-step counts. Small steps alone do not establish convergence. Saved dense-output sample spacing is a different quantity.

## Coupled mechanics

Coordinates are actuator rotation `q`, stroke `θ`, pitch `β`, their rates, three accumulated energy/work states and two anchor coordinates: **11 states**.

Constant-curvature tip displacement and Jacobian:

`x(q) = L[1−cos(q)]/q`, `j(q) = dx/dq`, with stable series near zero.

Transmission extension is `δ = x − r θ`. Let `ΔT = T+ − T−`. The equations include:

- `Ma q̈ = H V − K q − ca q̇ − ΔT j`
- `Is θ̈ = r ΔT + Qs`
- `Ip β̈ = Qp − kp β − cp β̇`

The two compliant anchor/tendon states determine `T+` and `T−`; they are not extra independent voltage commands. The code's variable `td` is **half** the tension difference, so its `2*td` is `ΔT` here.

For the retained surrogate load:

`u = R θ̇ cos(β) + e β̇`, `F = g(t) c u |u|`,

`Qs = −R cos(β) F`, `Qp = −e F`.

Therefore `Qs θ̇ + Qp β̇ = −F u = −g c |u|³ ≤ 0`. This explains why resistance reverses with the **combined modeled motion** and dissipates energy. It is not a validated aerodynamic lifting force.

The reciprocal electrical relation is `I = C V̇ + H q̇ + G V`. Positive electrical-port work is accumulated without crediting recovered energy. The power budget also includes baseline electronics and conversion efficiency.

Reduced geometry descriptors `κ = q/L` and hinge twist `β/Lh` describe different components. They are not an extra hardware stage, a complete spatial Darboux vector or dimensionless strain. A displayed hinge-strain proxy would need its geometric factor, such as `h |β|/Lh`.

## What the video says

“Prescribed voltage drives a modeled PZT-like actuator. A compliant mechanical transmission couples it to wing stroke and passive pitch under an imposed resistive load. The figure is a synchronized replay of saved component states, not demonstrated flight.”
