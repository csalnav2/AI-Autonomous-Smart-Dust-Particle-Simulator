# Indoor exploration and incident response prototype

Chris Salnave

Scientific evidence snapshot at 00:45 UTC on 31 October 2026. This explanation adds mathematical detail without a new simulation or new validation claim.

### What the application is trying to explore

The indoor notebook is an interactive engineering prototype for a team of six miniature agents exploring a building. Its environments include four floors and an attic, with underground, cleanroom and logistics layouts. The intended experience combines exploration, sensing and control: I can follow an individual agent, compare its visible and near-infrared views, and watch measurement trends while the fleet moves through the environment.

The application also includes optional voice and AI commands, alongside tunnel health and recovery functions for the software connection. These features make the project more useful as an exploratory interface. They do not make the simulated agents autonomous physical machines, and a connection-recovery feature should not be confused with evidence that a tiny vehicle could recover from a real flight failure.

The notebook is substantial software, with a packaged application containing 501 text assets. Its scope matters: it lets me ask how exploration, sensing, control and resource limits would interact if the assumed components were achievable. The saved upload contains no execution outputs, so this explanation describes the implementation rather than claiming that the full application was run and verified in this review.

### How to read the interface

A camera view, a rising sensor trace or a completed route is an output of the prototype’s assumptions. Those outputs can help expose questions about the proposed system, but they do not independently confirm the sensor, actuator or battery that the interface depicts. I want the interface to make those relationships easier to inspect, rather than hide the assumptions behind a convincing scene.

### What moves the indoor agents

The flight model assumes a battery-powered piezoelectric mechanism and uses cycle-averaged lift and drag. It includes budgets for mass, power, temperature and geometry, with closures for lift, power and stress. In practical terms, it represents the average effect of repeated actuation cycles instead of resolving every wingbeat and every interaction between the wing and the surrounding air.

The model commands an ideal thrust direction. It is not a full six-degree-of-freedom account of wing-generated forces and torques, body attitude and coupled motion. That distinction is important when watching an agent turn or stabilize. The controller can explore a response inside the model, but the display does not establish that a physical wing and transmission could produce the required attitude control.

Airflow is represented by a separate bounded horizontal grid on each floor. The default grid has 48 cells along its longest axis and updates at 5 Hz, while the flight update runs at 60 Hz. This gives the prototype a changing flow environment without resolving three-dimensional flapping-wing aerodynamics. The independent floor grids should not be read as a complete three-dimensional account of airflow throughout the building.

### Materials sensing and endurance remain assumptions

The wing model includes a graphene-oxide-derived material hypothesis with humidity sensitivity. Wet-window behavior adds hypotheses for condensation, evaporation and image blur. These are ways to explore possible interactions between the environment and the device, not measurements of a validated wing material or optical coating.

The application’s aerosol and fluorescence responses are generic simulated measurements with uncertainty. They can illustrate how a sensing workflow might behave, but they cannot identify a pathogen or declare a cleanroom safe. An informative-looking trace is still a synthetic response unless it is tied to characterized hardware and an appropriate measurement process.

The default long_10min scenario assumes a 6 mJ battery and external ground service for repeated sorties. Its name is not evidence of ten minutes of uninterrupted flight. The resource model is useful for examining a proposed operating pattern; it is not a demonstrated endurance result.

### How this differs from the indoor research video

The application’s nominal 300-micrometre body and wingtip-span specification is distinct from the research video’s roughly 300-micrometre target body, 374.43-micrometre wing envelope and still-unknown total assembly span. These numbers describe different model boundaries and should not be substituted for one another.

The prototype asks how a mission might work under its assumptions. The focused mechanical experiment asks whether selected actuator, transmission and wing equations satisfy their numerical and component checks. A useful mission interface does not validate that mechanism, and component motion does not validate the application’s exploration or endurance claims.

### Implemented mathematics in the indoor application

I separate the application’s engineering estimates from the component experiment. The application first converts an assumed piezoelectric response into a stroke limit, then estimates average thrust and power. Its room-airflow solver supplies a changing air velocity; it does not resolve the flow around each wing.

$$
\epsilon_p=|d_{31}|V_p/t_p,\qquad \phi_{\max}=\epsilon_p L_pG/R
$$

Here d₃₁ is the magnitude of the piezo strain coefficient [m/V], Vp the peak voltage [V], tp the piezo thickness [m], Lp its active length [m], G the displacement ratio, and R the one-wing span [m]. Strain is dimensionless and the stroke limit is in radians. The steps are voltage to strain, strain to actuator displacement, and displacement through the assumed transmission to a wing angle. A larger displacement ratio carries a force and stiffness cost.

$$
\omega=2\pi f,\quad S=2Rc,\quad \overline{u^2}=(\omega\phi R)^2/6,\quad T=\tfrac12\rho S C_L\overline{u^2}
$$

Frequency f is in Hz, angular frequency ω in rad/s, stroke half-amplitude φ in radians and thrust T in newtons. Chord c and span R are in metres, S is the combined two-wing area [m²], ρ is air density [kg/m³], and CL is an assumed dimensionless lift coefficient. The factor 1/6 implements the simplified spatial and cycle averaging. Holding those assumptions fixed, doubling f multiplies this model’s thrust by four, but power, stress and stroke limits may block that change. These equations connect to the frequency, thrust and support-margin readouts, not to demonstrated lift-off.

$$
P_{\rm mech}=P_{\rm profile}+k_i T^{3/2}/\sqrt{2\rho A_s}+(1-\eta_r)I_w(\omega\phi)^2 f
$$

$$
P_{\rm profile}=\frac{\rho S C_D(\omega\phi R)^3}{6\pi},\quad A_s=2\phi R^2,\quad P_{\rm cycle}=P_{\rm base}+P_{\rm mech}/\eta_d+\pi f C_pV_p^2\tan\delta
$$

All P terms are powers [W]. CD and ki are assumed coefficients; As is swept area [m²]; Iw is wing inertia [kg m²]; ηr and ηd are recovery fraction and drive efficiency; Cp is capacitance [F]; and tan δ is dielectric loss tangent. The terms account for profile loss, induced power, unrecovered inertial work and dielectric loss. Live motion adds useful translational power and on/off and available-power limits. The battery and thermal panels therefore require more than a positive thrust estimate.

$$
\partial_t\mathbf u+(\mathbf u\cdot\nabla)\mathbf u=-\nabla p/\rho+\nu\nabla^2\mathbf u+\mathbf f,\qquad\nabla\cdot\mathbf u=0
$$

This is the reduced two-dimensional incompressible Navier–Stokes model actually discretized for each floor. Velocity u = (ux, uy) is in m/s, pressure p in Pa, kinematic viscosity ν in m²/s, and f is an imposed acceleration [m/s²]. Staggered velocities, semi-Lagrangian advection, explicit diffusion and pressure projection update the horizontal field. The flow and relative-drag displays reflect that calculation; vertical flow, cross-floor coupling and three-dimensional wing wakes remain outside it.

### Suggested caption

I built this indoor prototype to explore how a small fleet might navigate, sense and manage constraints. The software contains real model and control logic, while its flight, material and sensing assumptions remain hypotheses to test.

### Mathematical sources

Indoor application mathematics: indoor_lab/self_flight.py lines 163–166 (piezo stroke limit), 199–204 and 308–312 (cycle averaging), 313–337 and 440–456 (power budgets); indoor_lab/room_flow.py lines 1–18 and 44–49 (reduced two-dimensional airflow and defaults).
