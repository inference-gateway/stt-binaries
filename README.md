# stt-binaries

Prebuilt static speech-to-text binaries (whisper-cli, ffmpeg) auto-downloaded by the [Inference Gateway CLI](https://github.com/inference-gateway/cli) into `~/.infer/bin` when `speech_to_text.auto_download` is enabled.

Assets are named `<name>-<os>-<arch>` and verified against `checksums.txt` (sha256).

Assets are reproducible `nix build nixpkgs#pkgsStatic.{whisper-cpp,ffmpeg-headless}` outputs (musl, Linux amd64/arm64). Dispatching the [Release workflow](.github/workflows/release.yml) runs [semantic-release](https://semantic-release.gitbook.io): the next version is computed from Conventional Commits since the last `vX.Y.Z` tag and published as a new immutable release with freshly built binaries (no commits since the last release → no new release). To refresh binaries against current nixpkgs without other changes, land a `fix: refresh binaries` commit and dispatch. macOS is served by `$PATH` (`brew install whisper-cpp ffmpeg`) instead of prebuilt assets.

## Licenses

The binaries are unmodified builds of the corresponding nixpkgs packages; the exact, reproducible build recipe is [`static.nix`](static.nix), which together with [nixpkgs](https://github.com/NixOS/nixpkgs) constitutes the complete corresponding source for every asset.

- `whisper-cli` — [MIT](https://github.com/ggml-org/whisper.cpp/blob/master/LICENSE), © ggml-org / whisper.cpp contributors.
- `ffmpeg` — [GPL-3.0](https://www.ffmpeg.org/legal.html) (built with `--enable-gpl --enable-version3`, as reported by `ffmpeg -version`); statically linked components include opus, vorbis, speex, lame, alsa-lib, libxml2, zlib, bzip2, xz under their respective LGPL/BSD-class licenses.
