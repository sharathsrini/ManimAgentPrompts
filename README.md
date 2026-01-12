# Manim Agent Prompts

ManimAgentPrompts is a public collection of system-level compiler prompts that define how AI agents generate layout-safe, publication-quality Manim animations from natural language.

These prompts act as open, versionable animation compiler specifications — governing layout invariants, rendering rules, text safety, and refactor protocols — and are designed to be consumed by runtimes such as [Mathify](https://mathify.dev) to produce reproducible, editable, and classroom-ready mathematical visualizations.

### Open animation-compiler specifications for AI-generated Manim scenes

These prompts are not simple chat instructions.
They are formal, versionable **animation compiler specifications** that govern:

• layout invariants
• text safety rules
• diagram composition contracts
• refactor / remix protocols
• reproducibility and rendering discipline

They are designed to be consumed by runtimes such as [**Mathify**](https://mathify.dev) to produce deterministic, editable, classroom-ready visualizations — without users writing Manim code.

---

## Why this exists

Most “AI animation tools” hide their system prompts.

That means:

• no reproducibility
• no auditability
• no extensibility
• no shared standards

ManimAgentPrompts makes the **compiler layer itself open and forkable** — so animation behavior becomes:

• transparent
• version-locked
• academically citable
• community extensible

This repo aims to define the **reference Manim Animation Compiler Spec.**

---

## How runtimes use this

The compiler spec governs:

• how scenes are structured
• how layouts are enforced
• how overlaps are prevented
• how text is summarized
• how remixes and refactors are handled

This makes every generated animation **reproducible, deterministic, and editable**.

---

## Who this is for

• Math & physics educators
• Researchers
• Curriculum designers
• Visualization engineers
• AI tool builders

If you are building anything that turns language into Manim scenes, this repo is meant to be your compiler layer.

---

## Philosophy

> These prompts define a computational medium, not a chat persona.
> The runtime is an implementation.
> This repository is the language specification.

Keep it simple, calm, and very “this is infrastructure, not a vibe repo.”

Here’s a clean contribution section you can drop straight into the README:

---

## Contributing

Contributions are welcome.

This repository defines **system-level compiler specifications** that control how AI agents generate Manim animations, so changes here directly affect rendering behavior and layout guarantees.

If you’d like to propose improvements:

1. Fork the repository
2. Make your changes in a feature branch
3. Open a pull request with a brief explanation of what the change improves (layout safety, clarity, coverage, etc.)

Guidelines:

- Keep specs clear, deterministic, and implementation-agnostic
- Avoid introducing ambiguous language or model-specific hacks
- Preserve layout safety, readability, and reproducibility guarantees
- Prefer small, focused changes over large rewrites

All pull requests are reviewed manually before merging.

This isn’t a high-friction process — just use common sense and aim to make the compiler specs clearer, safer, and more broadly useful.
