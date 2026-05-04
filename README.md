<div align="center">

<img src="assets/logo.png" alt="orrchestrator logo" width="160" />

# orrchestrator

**An AI software-development hypervisor.**
Run a fleet of AI coding sessions from a single Rust TUI — organized into agent workforces, routed through a deterministic dispatch pipeline, and tracked alongside the projects they're building.

[![Latest release](https://img.shields.io/github/v/release/TruStoryHnsl/orrchestrator-releases?label=release&color=0888A8)](https://github.com/TruStoryHnsl/orrchestrator-releases/releases/latest)
[![Downloads](https://img.shields.io/github/downloads/TruStoryHnsl/orrchestrator-releases/total?color=087898)](https://github.com/TruStoryHnsl/orrchestrator-releases/releases)
[![Platforms](https://img.shields.io/badge/platform-linux%20%7C%20macOS%20%7C%20WSL2-086888)](#download)
[![License](https://img.shields.io/badge/license-personal%20non--commercial-085878)](#license)

</div>

> **Source is proprietary.** This repository hosts only the official pre-built binaries.
> For commercial licensing, embedding, or redistribution: **colton.j.orr@gmail.com**

---

## What you get

A single ~5 MB Rust binary that sits between you and the army of AI coding sessions you'd otherwise be juggling by hand. orrchestrator manages parallel sessions, dispatches structured agent workforces, routes raw stream-of-consciousness input into project-scoped pipelines, and gives you one TUI to see all of it.

<div align="center">
  <img src="assets/screenshots/01-oversee-projects.png" alt="Oversee panel — multi-project tracker" width="92%" />
  <p><em>Oversee — every project, every session, every state, in one view.</em></p>
</div>

---

## Why it exists

Coding with one AI assistant is fast. Coding with ten in parallel is faster — but only if you can keep them isolated, fed with the right context, and stopped from clobbering each other on the same files. Doing that by hand turns into full-time switching overhead. orrchestrator collapses the overhead into a TUI:

- **One session per workflow, not per agent.** Token efficiency is a first-class design goal.
- **The dispatcher is deterministic.** No LLM "reasoning" sits in the orchestration layer — workforce steps execute mechanically. All the AI judgment lives inside the agents themselves, where you can see it.
- **Context isolation is enforced.** Verifiers never see other verifiers' results on the same task. PMs never see the developer's reasoning blob. Each agent gets exactly the context its role requires.
- **File-cluster batching, not role batching.** Tasks are grouped by which files they touch — three Developer agents in parallel beats one serial Developer when the file footprints are disjoint.

---

## Tour

### Project oversight

Every project on disk is tracked in the **Oversee** panel — git status, sessions, recent activity, expandable file browser, all in one tab.

<div align="center">
  <img src="assets/screenshots/02-oversee-admin-expanded.png" alt="Oversee — file browser expanded into a project subtree" width="80%" />
</div>

### Stream-of-consciousness intake

The **Design > Intentions** panel is the ideas vault. You write raw — half-thoughts, feedback, "this should…", whatever. A COO agent optimizes each entry into discrete instructions; you audit the side-by-side diff; only then does it route to the project's instruction inbox. Each idea tracks a 0–100% progress gradient as the work lands.

<div align="center">
  <img src="assets/screenshots/03-design-intentions.png" alt="Design > Intentions — ideas vault with progress tracking" width="80%" />
</div>

### Workforces are markdown

Teams, workflows, agents, skills, tools, MCP servers, models, harnesses — all defined in plain markdown with structured frontmatter and pipe-delimited step tables. The **Design > Workforce** panel is a full editor over them. The pipeline below is the built-in `DEVELOP_FEATURE` workflow: PM → Resource Optimizer → Lead Architect → Developer fleet → Feature Tester → Penetration Tester → Repository Manager.

<div align="center">
  <img src="assets/screenshots/04-design-workforce-teams.png" alt="Design > Workforce > Teams — DEVELOP_FEATURE step pipeline" width="92%" />
</div>

### Agent library

21 agent profiles ship in the library — across Admin, Engineering, QA, DevOps, Marketing, and Legal departments. Each agent is a single markdown file: triggers, capabilities, tone, escalation rules, model tier.

<div align="center">
  <img src="assets/screenshots/05-design-library-agents.png" alt="Design > Library > Agents — Feature Tester profile" width="92%" />
</div>

### Cross-project plans

The **Design > Plans** panel is a unified `PLAN.md` browser across every project on disk. Expand a phase, mark a feature verified, cycle status, deprecate — changes persist directly to the source `PLAN.md`.

<div align="center">
  <img src="assets/screenshots/06-design-plans.png" alt="Design > Plans — concord PLAN.md tree" width="80%" />
</div>

---

## Panel reference

| Panel | What it does |
|---|---|
| **Design** | Intentions (ideas vault) · Workforce (workflow editor) · Library (agents/skills/tools/models/MCP/harnesses) · Plans (cross-project PLAN.md browser) |
| **Oversee** | Project tracker, file browser, session management |
| **Hypervise** | Live multi-session control over the running tmux fleet |
| **Analyze** | Token usage, throughput, cost estimates per session/project |
| **Publish** | Release lifecycle — packaging, distribution, compliance, marketing, history |

A web node-editor mirror is also available (`orrchestrator --webedit`) for terminal-averse workflows, and an optional native egui window (`--egui`) when built with that feature.

---

## Download

Latest binaries: **[Releases](https://github.com/TruStoryHnsl/orrchestrator-releases/releases/latest)**

| File | Platform |
|---|---|
| `orrchestrator-x86_64-unknown-linux-musl.tar.gz` | Linux x86_64 (statically linked — runs on any glibc/musl distro) |
| `orrchestrator-aarch64-apple-darwin.tar.gz` | macOS Apple Silicon (M1/M2/M3/M4) |
| `orrchestrator-x86_64-apple-darwin.tar.gz` | macOS Intel |
| `*.sha256` | SHA-256 checksum for each archive |

**Windows:** runs cleanly under WSL2 — install the Linux x86_64 build inside your WSL distro.

---

## Install

```bash
# Pick your platform
TARGET=x86_64-unknown-linux-musl      # Linux
# TARGET=aarch64-apple-darwin         # Apple Silicon Mac
# TARGET=x86_64-apple-darwin          # Intel Mac

VERSION=v0.1.0   # replace with the latest release tag

curl -L "https://github.com/TruStoryHnsl/orrchestrator-releases/releases/download/${VERSION}/orrchestrator-${TARGET}.tar.gz"        -o orrchestrator.tar.gz
curl -L "https://github.com/TruStoryHnsl/orrchestrator-releases/releases/download/${VERSION}/orrchestrator-${TARGET}.tar.gz.sha256" -o orrchestrator.tar.gz.sha256

# Verify (Linux: sha256sum; macOS: shasum -a 256)
shasum -a 256 -c orrchestrator.tar.gz.sha256

tar -xzf orrchestrator.tar.gz
sudo install "orrchestrator-${TARGET}/orrchestrator" /usr/local/bin/
```

Then:

```bash
orrchestrator           # launch the TUI (default)
orrchestrator --webedit # launch the web node editor on a local port
```

---

## Configuration

Configuration lives under `~/.config/orrchestrator/` and is scaffolded on first run. Everything is local-first.

The always-on WebUI server reads these optional environment variables:

| Variable | Purpose |
|---|---|
| `ORRCH_WEBUI_PORT` | Local HTTP port (default `8484`) |
| `ORRCH_WEBUI_BIND` | Local HTTP bind address (default `127.0.0.1`) |
| `ORRCH_WEBUI_TLS_CERT` / `ORRCH_WEBUI_TLS_KEY` | Enable native TLS termination |
| `ORRCH_WEBUI_TLS_PORT` | TLS listen port (default `8443`) |
| `ORRCH_WEBUI_PUBLIC_HTTP_PORT` | Optional secondary public-HTTP listener (off by default) |
| `ORRCH_WEBUI_TOKEN` | Bearer token required for non-loopback / non-trusted-CIDR clients |
| `ORRCH_WEBUI_TRUSTED_CIDRS` | CSV of CIDRs whose peers bypass the token (e.g. `100.64.0.0/10` for tailnet) |

Press **Esc** from any panel for live URLs.

---

## License

The binaries published here are licensed for **personal, non-commercial use** on the device of the end user who downloaded them. Redistribution is not permitted. The full license is bundled inside each archive and reproduced in [`LICENSE`](LICENSE).

For commercial licensing, embedding, or redistribution: **colton.j.orr@gmail.com**

---

## Issues & feedback

This repository accepts issues for download / installation problems and bug reports against released binaries. Feature requests, ideas, and roadmap discussion are routed through orrchestrator's own intake pipeline — contact the maintainer directly.

<div align="center">
<sub>orrchestrator · built in Rust · ratatui · tmux</sub>
</div>
