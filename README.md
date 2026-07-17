# stt-binaries

Prebuilt static speech-to-text binaries (whisper-cli, ffmpeg) auto-downloaded by the [Inference Gateway CLI](https://github.com/inference-gateway/cli) into `~/.infer/bin` when `speech_to_text.auto_download` is enabled.

Assets are named `<name>-<os>-<arch>` and verified against `checksums.txt` (sha256).

Assets are reproducible `nix build nixpkgs#pkgsStatic.{whisper-cpp,ffmpeg-headless}` outputs (musl, Linux amd64/arm64). Dispatching the [Release workflow](.github/workflows/release.yml) runs [semantic-release](https://semantic-release.gitbook.io): the next version is computed from Conventional Commits since the last `vX.Y.Z` tag and published as a new immutable release with freshly built binaries (no commits since the last release → no new release). To refresh binaries against current nixpkgs without other changes, land a `fix: refresh binaries` commit and dispatch. macOS is served by `$PATH` (`brew install whisper-cpp ffmpeg`) instead of prebuilt assets.
