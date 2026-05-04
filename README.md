# orrchestrator — Releases

Pre-built binaries of **orrchestrator**, an AI-powered software development hypervisor: a Rust TUI that runs many parallel coding sessions, organizes them into agent workforces, and routes raw user thought into a managed dev pipeline.

> This repository hosts only the official compiled binaries.

## What it is

orrchestrator is a single Rust binary that sits between you and the army of AI coding sessions you'd otherwise be juggling by hand. It:

- **Manages parallel sessions.** tmux-controlled local Claude Code (and other harness) sessions, grouped by project, displayed in a TUI.
- **Runs agent workforces.** Teams of agent profiles (PM, Developer, Researcher, Penetration Tester, Repository Manager, …) wired as a step pipeline. The hypervisor dispatches mechanically — no LLM reasoning in the dispatcher itself.
- **Routes raw input.** Stream-of-consciousness ideas get optimized into discrete instructions, audited by you, then routed to the right project's inbox.
- **Tracks the dev pipeline.** Multi-project plan view, session tracking, token-usage analytics, release packaging — all in one TUI, with a web UI mirror.

## Download

Latest binaries: **[Releases](https://github.com/TruStoryHnsl/orrchestrator-releases/releases/latest)**

Each release ships:

| File | Platform |
|---|---|
| `orrchestrator-x86_64-unknown-linux-musl.tar.gz` | Linux x86_64 (statically linked, runs on any glibc/musl distro) |
| `orrchestrator-aarch64-apple-darwin.tar.gz` | macOS (Apple Silicon — M1/M2/M3/M4) |
| `orrchestrator-x86_64-apple-darwin.tar.gz` | macOS (Intel) |
| `*.sha256` | SHA-256 checksum for each archive |

**Windows users:** orrchestrator runs cleanly under WSL2 — install the Linux x86_64 build inside your WSL distro.

## Install

```bash
# Pick your platform
TARGET=x86_64-unknown-linux-musl      # Linux
# TARGET=aarch64-apple-darwin         # Apple Silicon Mac
# TARGET=x86_64-apple-darwin          # Intel Mac

VERSION=v0.1.0   # replace with the latest release tag

curl -L "https://github.com/TruStoryHnsl/orrchestrator-releases/releases/download/${VERSION}/orrchestrator-${TARGET}.tar.gz" -o orrchestrator.tar.gz
curl -L "https://github.com/TruStoryHnsl/orrchestrator-releases/releases/download/${VERSION}/orrchestrator-${TARGET}.tar.gz.sha256" -o orrchestrator.tar.gz.sha256

# Verify checksum (Linux: sha256sum; macOS: shasum -a 256)
shasum -a 256 -c orrchestrator.tar.gz.sha256

tar -xzf orrchestrator.tar.gz
sudo install "orrchestrator-${TARGET}/orrchestrator" /usr/local/bin/
```

Then run:

```bash
orrchestrator           # launch the TUI (default)
orrchestrator --webedit # launch the web node editor on a local port
```

## Configuration

orrchestrator stores its configuration under `~/.config/orrchestrator/`. On first run it scaffolds defaults; everything is local-first.

Optional environment variables for the always-on WebUI server:

| Variable | Purpose |
|---|---|
| `ORRCH_WEBUI_PORT` | local HTTP port (default `8484`) |
| `ORRCH_WEBUI_BIND` | local HTTP bind address (default `127.0.0.1`) |
| `ORRCH_WEBUI_TLS_CERT` / `ORRCH_WEBUI_TLS_KEY` | enable native TLS termination |
| `ORRCH_WEBUI_TOKEN` | bearer token required by remote (non-loopback, non-trusted-CIDR) clients |
| `ORRCH_WEBUI_TRUSTED_CIDRS` | CSV of CIDRs whose peers bypass the token (e.g. `100.64.0.0/10` for tailnet) |

See the in-app **Esc** menu for live URLs.

## License

The binaries published here are licensed for **personal, non-commercial use** on the device of the end user who downloaded them. Redistribution is not permitted. The full license is bundled inside each archive.

For commercial licensing, embedding, or redistribution inquiries, contact: **colton.j.orr@gmail.com**.

## Issues & feedback

This repository accepts issues for download / installation problems and bug reports against released binaries. For feature requests, ideas, or roadmap discussion, contact the maintainer directly — orrchestrator's own intake pipeline is how that work gets prioritized.
