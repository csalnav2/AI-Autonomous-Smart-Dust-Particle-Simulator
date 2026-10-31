# Indoor actuator transmission and wing research video

Chris Salnave

The saved mechanical evidence remains the 00:45 UTC showcase snapshot of 31 October 2026. This updated explanation covers later presentation refinements and separately identifies the later native-control result; neither changes the saved wing trajectory.

### The saved calculation behind the motion

The indoor research video follows a narrower mechanical chain: prescribed voltage drives a PZT-like actuator model, which acts through a compliant tendon, drum and hinge to produce wing stroke and passive pitch. PZT means lead zirconate titanate. Here the name identifies the actuator model; the video does not establish that a complete device with these properties has been fabricated or characterized.

The displayed interval is 180 to 200 milliseconds from a saved 200-millisecond run. Those 20 milliseconds are played over 24 seconds, producing 1,200-times slow motion. The original actuation chain remains available at 1920 × 1080 and 60 frames per second. The latest expanded chain is 1920 × 2340, and the standalone geometry companion is 1920 × 1080; each contains 1,440 frames at 60 frames per second. The earlier mounted-wing preview is 720p at 30 frames per second. These variants replay the same saved data. These are presentation settings, not new simulation timesteps or increases in scientific resolution.

The indoor application’s 60 Hz flight update, the mechanical research calculation’s maximum integration step of 21 microseconds, and the chain video’s 60 display frames per second are three different timebases. They belong to different jobs and should not be treated as equivalent numerical resolution.

In the additional chain video, common linear interpolation fills the display frames between saved samples. There is no filtering, new solve or boosted angle added to make the motion more dramatic. The panels are synchronized to the same saved time, so viewers can relate voltage, actuator behavior, transmission motion and wing response without mistaking a visually smooth replay for additional numerical evidence.

### Reading the mechanical chain

The panels trace connected parts of the model, but their synchronization does not mean that every response is a one-way, zero-lag copy of the driving signal. The compliant mechanism and passive pitch are part of the modeled response. I am showing how the saved quantities move together, not reducing that response to an instantaneous animation rule.

The actuator curvature descriptor q/L and the hinge twist descriptor beta/Lh refer to different parts of the reduced mechanical description. They are separate Darboux-type descriptors, not an additional physical component or a complete strain field across the wing. Reading them as local model quantities avoids treating the diagram as a full continuum-mechanics reconstruction.

The geometry labels also refer to different extents. The project has a roughly 300-micrometre target body, while the displayed wing envelope is 374.43 micrometres. The actuator is 150 micrometres long, the drum radius is 6 micrometres and the hinge is 40 micrometres. Local zooms make the small parts legible, and the transmission view is schematic. The composite should not be read as fabrication CAD or as a verified total assembly span.

### The drive and load are prescribed

The selected trace uses an approximately 266.819 Hz sinusoidal voltage and is open-loop. Its prescribed resistive-load factor rises from 1 to 4 between 80 and 90 milliseconds, holds through 140 milliseconds, and falls back by 150 milliseconds. That load history is part of the test setup. It is not a response to measured air pressure or evidence of an air-pressure feedback controller.

This distinction explains what I can learn from the clip. A prescribed input and load let me inspect conditional component motion and mechanical checks within the chosen equations. They do not show that a complete vehicle can generate sufficient aerodynamic lift, maintain attitude, leave a surface or sustain flight. The animation also does not establish a manufactured assembly or an endurance result.

### Why I am sharing it

The value of this video is that it makes a specific model easier to inspect. A viewer can see which part is being driven, which motion is transmitted and which quantities are being compared. I would welcome scrutiny of those relationships and the numerical checks, rather than treating the visual plausibility of the mechanism as its validation.

### Implemented mathematics behind the component panels

The selected saved run integrates coupled actuator, stroke and passive-pitch coordinates. The formulas below describe that run, not the application’s cycle-averaged flight closure. The actuator coupling and stiffness use distinct symbols here so they cannot be confused with the outdoor force Jacobian.

$$
V(t)=A(t)\sin(2\pi ft),\quad f=0.9f_{\rm ref}\simeq266.819\,Hz,\quad T=1/f\simeq3.748\,ms
$$

$$
h_{\max}=\frac{1}{160f_{\rm ref}}\simeq21.0817\,\mu s,\qquad \frac{10\,ms}{h_{\max}}\simeq474.34
$$

The amplitude ramps at 100 V/s to 4 V by 40 ms, then at 25 V/s to 4.1 V by 44 ms and remains there. This defines the voltage panel. The maximum allowed integration step is about 21.0817 µs: spanning 10 ms requires at least 475 integration intervals when none exceeds that limit, potentially more under adaptation. That is a resolution comparison, not a recorded internal step count or proof of accuracy.

$$
x(q)=L(1-\cos q)/q\simeq Lq/2,\quad j=dx/dq,\quad \delta=x(q)-r\theta
$$

Actuator bend q and wing stroke θ are in radians, L = 150 µm, and the drum radius r = 6 µm. Tip displacement x and transmission mismatch δ are in metres; j is in m/rad. Expanding cos q ≈ 1 − q²/2 gives x ≈ Lq/2, with the continuous limit x(0) = 0. The tendon pair responds to mismatch and anchor motion. Its tension difference ΔT = T+ − T− is in newtons; the source variable td is half that difference, not ΔT itself.

$$
M_a\ddot q=HV-K_aq-c_a\dot q-\Delta Tj,\quad I_s\ddot\theta=r\Delta T+Q_s
$$

$$
I_p\ddot\beta=Q_p-k_p\beta-c_p\dot\beta
$$

Ma, Is and Ip are effective angular inertias [kg m²]; H is coupling [N m/V]; Ka and kp are rotational stiffnesses [N m/rad]; ca and cp are damping coefficients [N m s/rad]; and Qs and Qp are torques [N m]. These balances explain the phase differences between voltage, actuator bend, stroke and passive pitch β. Synchronizing the panels does not require proportional or zero-lag motion.

$$
g(t)=1+3s\!\left(\frac{t-0.080}{0.010}\right)-3s\!\left(\frac{t-0.140}{0.010}\right)
$$

$$
\xi=\operatorname{clip}(z,0,1),\qquad s(z)=\xi^2(3-2\xi)
$$

$$
u=R\dot\theta\cos\beta+e\dot\beta,\quad F_d=g(t)c_Du|u|,\quad Q_s=-R\cos\beta F_d,\quad Q_p=-eF_d
$$

$$
Q_s\dot\theta+Q_p\dot\beta=-F_d(R\dot\theta\cos\beta+e\dot\beta)=-g(t)c_D|u|^3\le0
$$

Here R is 0.6 times wing span, e is chord/4 [m], u is the modeled load-point speed [m/s], and cD is a prescribed coefficient [N s²/m²]. The smoothstep s clips its input to the interval from zero to one; time t in its arguments is in seconds. The load multiplier g rises smoothly from 1 to 4 over 80–90 ms and returns over 140–150 ms. Substituting the torque definitions into mechanical power gives −Fd u, then −g cD|u|³ [W], so the imposed load removes energy in either motion direction. It is not calibrated aerodynamic lift. The coefficient uses a reference peak angular speed ωref = Aref 2πfref, not just angular frequency.

$$
\kappa_a=q/L,\qquad\kappa_h=\beta/L_h
$$

These reduced curvature and hinge-twist quantities have units m⁻¹ and belong to different components. They connect the actuator curve and passive-pitch readouts without claiming a full spatial wing-strain field.

### Reading the updated geometry and comparison

The expanded chain puts a genuine normalized voltage–curvature comparison at the top. The original chain panels remain below, followed by two separate geometric views. Gold is voltage and dashed cyan is actuator curvature. Each trace is divided by its own maximum absolute saved value over the displayed 180–200 ms interval:

$$
\widetilde V(t)=\frac{V(t)}{\max |V|},\qquad
\widetilde\kappa(t)=\frac{q(t)/L}{\max |q/L|}.
$$

The shared vertical axis is dimensionless. The physical peaks are approximately 4.100 V and 757.022 m⁻¹. The actuator bend reaches approximately 0.113553 rad, or 6.51 degrees. These are different saved quantities, not two copies of a voltage trace. A fit at 266.819 Hz gives an approximately 0.796-degree actuator lag in this interval. Its equivalent 8.285 µs is shorter than the roughly 16.865 µs saved-sample spacing, so it is a descriptive sub-sample fit, not directly resolved or independently validated physical latency. A phase lag from inertia, stiffness or damping is not automatically a transmission failure. No artificial offset was inserted to make the curves look different.

For the actuator, the original reduced mode assumes constant curvature. With u a dimensionless coordinate from 0 to 1, its centreline reconstruction is

$$
\mathbf r_a(u,t)=\left(\frac{L\sin[q(t)u]}{q(t)},\frac{L\{1-\cos[q(t)u]\}}{q(t)},0\right),
\qquad \mathbf r_a(u,t)\to(Lu,0,0)\quad(q\to0).
$$

The tangent and in-plane normal arrows show frame orientation. Their lengths are display symbols, not force magnitudes. The transverse tip coordinate agrees with the original one-mode actuator displacement formula above.

The hinge is a different component. Its scalar end angle β(t) is displayed using an explicitly assumed uniform twist along its 40 µm length:

$$
\psi(u,t)=\beta(t)u,\qquad
\mathbf r_h(u,v,t)=\big(L_hu,\;v\cos[\beta(t)u],\;v\sin[\beta(t)u]\big),
\quad -1\,\mu\mathrm m\le v\le1\,\mu\mathrm m.
$$

The actual modeled width is 2 µm. The latest view magnifies the two transverse display coordinates by four while leaving length and β unchanged. This is labeled on screen. The diagonal orthographic camera uses 20-degree yaw and 50-degree pitch, with depth ordering, contrasting edges and an x/y/z orientation triad. The surface lighting is an orientation cue, not a stress or strain map. Display aspect ratio and edge slopes must not be interpreted as a physically redesigned hinge.

This ribbon changes over time with saved β(t), but its spatial shape is a kinematic interpolation. No travelling torsional wave, membrane topology change, warping field or complete wing-strain field has been solved. The actuator curvature q/L and hinge twist β/Lh cannot be assembled into a full Darboux field of a single body because they describe different components.

For an oriented material frame, the spatial Darboux rotation vector can be written as

$$
\frac{d\mathbf d_i}{ds}=\boldsymbol\Omega(s)\times\mathbf d_i(s).
$$

In three dimensions, a rotation bivector and its axial-vector dual are compatible representations once orientation and sign conventions are chosen. The limitation here is the reduced state stored in this model, not the legitimacy of a bivector derivation.

The HTML companions provide rotation, zoom, time scrubbing and a true-width versus enlarged-width selector using embedded saved data. They use native Canvas, not Plotly. Keep each MP4 beside its matching player for synchronized video; the geometric explorer can also work independently. JavaScript interaction fixtures passed, but live browser rendering and browser frame rate remain unverified. Both final MP4 files passed full decoding of all 1,440 frames. The loop boundary resets the saved segment rather than demonstrating an indefinitely periodic physical solution.

### Later component result kept separate from the replay

As reported at 15:03 UTC on 31 October, eight native control cases completed with 48 of 48 recorded gates passing. This was a bounded qualification of the Python/native calculation interface and control outputs. No retained-cell or retained-map cases were evaluated. It does not establish a full wing simulation, validated airflow, lift-off or flight, and it does not alter the earlier saved motion replayed here. The component result and its archive should be cited as later evidence rather than silently folded into the showcase snapshot.

### Suggested caption

I’m replaying 20 milliseconds of a saved actuator-to-wing calculation at 1,200-times slow motion. It shows conditional component mechanics under a prescribed drive and load; it does not show demonstrated lift-off or flight.

### Mathematical sources

Indoor component mathematics: research/revised_passive_pitch/run.py lines 7–10, 14–39, 42, 57 and 71; sources/mechanism.py lines 11–21; confirm.py selects L40T24_r6_step_confirmation. These identify the selected drive, geometry, tension convention, coupled dynamics, dissipative load, step limit and curvature descriptors.

Updated presentation evidence: `VOLTAGE_CURVATURE_AUDIT.json`, `INDEPENDENT_OVERLAY_QA.json`, `INDEPENDENT_OBLIQUE_REVIEW.md`, `EXPANDED_MANIFEST.json` and `COMPANION_MANIFEST.json`. Later computational prerequisite: `independent_COMPONENT_RESULT.md` and `native_controls.npz`. These are numerical and source-review records, not external experimental measurements.
