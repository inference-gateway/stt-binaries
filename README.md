# stt-binaries

Prebuilt static speech-to-text binaries (whisper-cli, ffmpeg) auto-downloaded by the [Inference Gateway CLI](https://github.com/inference-gateway/cli) into `~/.infer/bin` when `speech_to_text.auto_download` is enabled.

Assets are named `<name>-<os>-<arch>` and verified against `checksums.txt` (sha256).

Assets are reproducible `nix build nixpkgs#pkgsStatic.{whisper-cpp,ffmpeg-headless}` outputs (musl, Linux amd64/arm64), refreshed onto the `stt-v1` release by dispatching the [Release workflow](.github/workflows/release.yml). macOS is served by `$PATH` (`brew install whisper-cpp ffmpeg`) instead of prebuilt assets.
