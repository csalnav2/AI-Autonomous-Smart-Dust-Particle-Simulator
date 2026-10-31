# Portability and verification scope

The original notebook is preserved byte for byte. Its restored source is independently browsable, but its setup/launch cells may install dependencies and open external connections; review before execution. Voice/API credentials, tunnel ownership and connected services are user-provided configuration, not included working credentials. The app may use externally hosted browser assets or service integrations and is not promised to run offline. The **scientific replay HTML is offline/self-contained**.

The original scientific capsule retains run.py, confirm.py, analyze.py, the mechanism source, nested local CSV/JSON dependencies, baseline traces, declared configurations, results and saved traces. This avoids presenting the video as if it were the only source. Parent experiment helpers/upload tools and logs are omitted. All source computations remain unexecuted during export.

Python dependencies are listed in each original requirements file. The renderer also needs FFmpeg/libx264 and `/usr/share/fonts/truetype/dejavu/DejaVuSans.ttf`; adapt that font path explicitly on another OS. Its saved-trace fallback is colocated with the renderer, so source-relative data remains available in this layout. No environment lock or cross-platform reproduction guarantee is claimed.

The copied original scientific README mentions a historical three-part archive; that is not an instruction to find missing export parts. This export contains the complete selected study directory except delivery helpers, caches and logs. It is a study-source capsule, not the entire ongoing project's native-backend environment.

Security review here is limited to text-pattern scanning and static inspection. It is not a penetration test or a guarantee that an app is safe to expose publicly. Bundled test-only owner tokens/example tunnel URLs are deliberate synthetic fixtures, not current connection records. Review licensing and security before publishing.

The original extracted app had 501 assets. This export retains 500: one historical Python-suite log is omitted as non-source logging material. The unchanged original notebook still retains its original embedded bundle. Its empty execution outputs were checked statically. No extracted connection/session files were identified.
