# Repository Guidelines

## Project Structure & Module Organization
This repository is intentionally small. The main executable is `wechat-multi-open.sh`, which contains the interactive macOS workflow for cloning, signing, and removing WeChat app copies. Static assets live under `icon/` (app icons and release zip files), and documentation images live under `screenshots/`. `README.md` is the user-facing install and usage guide.

## Build, Test, and Development Commands
There is no compile step or package manager in this project.

- `chmod +x wechat-multi-open.sh`  
  Makes the script executable.
- `./wechat-multi-open.sh`  
  Runs the interactive tool locally on macOS.
- `bash -n wechat-multi-open.sh`  
  Performs a syntax check before committing shell changes.
- `shellcheck wechat-multi-open.sh`  
  Recommended when `shellcheck` is available; use it to catch quoting, array, and portability issues.

## Coding Style & Naming Conventions
Use Bash with `set -euo pipefail`, as the existing script does. Prefer 4-space indentation, `snake_case` function names, and uppercase names for readonly/global configuration such as `SRC` and `BASE_BUNDLE_ID`. Quote variable expansions, keep helper functions small, and preserve the script's current user-facing style for prompts and status output.

## Testing Guidelines
This repository does not include an automated test suite yet. For script changes, run `bash -n` and then verify behavior manually on macOS with an installed `/Applications/WeChat.app`. Test the affected flow directly: create copies, launch them, and remove them cleanly. If you change icons, README screenshots, or release assets, confirm the referenced filenames still exist.

## Commit & Pull Request Guidelines
Recent history mixes simple messages (`Update README.md`) with conventional prefixes such as `feat:`, `fix(icon):`, `refactor:`, and `docs:`. Follow the prefixed style for substantive changes and keep subjects imperative and concise, for example `fix(script): handle missing container cleanup`.

Pull requests should state the macOS version tested, summarize the user-visible behavior change, and note any `sudo`, `codesign`, or app bundle handling changes. Include screenshots only when README or asset presentation changes.

## Security & Configuration Notes
The script operates on `/Applications` and uses `sudo`, `rm -rf`, `codesign`, and `PlistBuddy`. Keep path handling explicit and avoid broad deletes outside the numbered `WeChat*.app` copies and their matching container directories.
