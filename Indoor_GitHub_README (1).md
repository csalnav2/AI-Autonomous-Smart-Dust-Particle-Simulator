# Indoor Smart Dust — application vision and component research

**Review/upload package, not a publication or a flight demonstration.** This export contains editable code, saved evidence, a scientific video, an offline HTML viewer and Markdown explanations. No remote repository was changed.

## Start here

- Open **[index.html](index.html)** for an offline, self-contained scientific video viewer (the video is embedded).
- [Application explanation](docs/INDOOR_APPLICATION_EXPLANATION.md): the six-agent exploration/interface prototype and its assumptions.
- [Research/video explanation](docs/INDOOR_RESEARCH_VIDEO_EXPLANATION.md): the separately modeled voltage → piezoelectric actuator → compliant transmission → wing chain.
- [Equations and timing](docs/MATH_AND_TIMING.md), [evidence/status](docs/STATUS.md), [portability](docs/PORTABILITY.md), [rights](RIGHTS_AND_NOTICES.md).

## What the code does versus what was verified

| Package section | What it contains | Evidential limit |
|---|---|---|
| `application/` | Original uploaded Colab notebook; restored application, visualization, controller, sensing, facility/flow and test source | Static extraction/inspection only in this export. Original upload has no executed-cell outputs. Bundled historical test results are not new runtime verification. |
| `research/revised_passive_pitch/` | Saved reduced 11-state mechanical model, run/confirmation/analysis source, local input dependencies, declared cases, results, baseline data and traces | Conditional mechanical component results, including failures; imposed surrogate load. No demonstrated lift, free flight, calibrated aerodynamics or material qualification. |
| `media/chain/` | 1080p/60 fps scientific MP4, editable renderer, saved trace, data mapping, offline player, interpolation QA | Replay of saved component motion, not a new scientific run. Display interpolation does not improve physical accuracy. |

The application supplies the exploratory/cinematic-style interface code requested for GitHub. It is **not** the user's separately produced cinematic movie, which is not included here. Its hypothetical flight and facility exploration must not be presented as an experimentally verified capability of the mechanical component model.

## Research interpretation

The selected trace is `L40T24_r6_step_confirmation.npz`. It has a 40 µm hinge length, 0.24 µm hinge thickness, 6 µm drum and prescribed load episode. The 300 µm figure is a **target body size**, not a verified overall device envelope: the modeled wing span is approximately 374.4 µm, and assembly span is not established.

The frozen comparison includes failed cases as well as completed cases. The initial baseline completed 0/6 cases; the geometry-only L40T24 family completed 4/6; the separate assumed-higher-damping family completed 6/6. Those are conditional component-screen outcomes, not a universal pass or a flight result. Subsequent selected geometry-only confirmation results are saved separately in `post_screen_confirmation.json`; read them alongside the historical screen review rather than silently overwriting it.

The selected video replays simulated 0.180–0.200 s over 24 s (**nominal 1200× slow motion**). All displayed components share a timestamp. Lines grow from original samples; current geometry/readouts are linearly interpolated between saved samples. No invented free-flight path or enhanced strain is added. A repeat restarts the excerpt; it is not a claim of a physically continuous loop.

## Browse source, safely

1. Inspect the original notebook in `application/` without executing cells. Restored assets live in `application/restored_assets/`; their existing README and requirements describe the original app.
2. Read `research/revised_passive_pitch/REPORT.md`, `PROTOCOL.md`, `POST_SCREEN_VERIFICATION.md` and `SOURCES_AND_BOUNDS.md` before evaluating its code.
3. `run.py` contains a multi-case numerical experiment; `confirm.py` launches three confirmations. **Do not run either just to view this package.** Existing resource permissions do not grow because source is exported. A reproduction needs its own bounded review and isolated output copy.
4. `media/chain/render_chain.py` renders saved data only; it requires NumPy, Pillow, FFmpeg/libx264 and the documented system font. No packages were installed or renderer rerun during packaging.

`MANIFEST.json` hashes exported contents; `PROVENANCE.json` maps unchanged copies to exact source hashes. `STATIC_QA.json` records static checks, not runtime success. Original scripts and historical reports remain unchanged, including historical packaging instructions; this README defines the new export layout. There is no automatic installer, GitHub Action, external upload, tunnel or remote publication configured by this export.
