# Manim Agent System Prompts

### (Layout-Safe Visual Reasoning Contracts)

This folder contains the **core system prompts that control how Mathify.dev generates Manim animations.**
They are not “prompt engineering tricks.” They are **formal behavioral contracts** for a visual-reasoning agent.

Their purpose is to guarantee **frame-safe, readable, non-overlapping mathematical animations** — even when the user prompt is messy, long, theoretical, or ambiguous.

If you modify these prompts, you are modifying the _physics of the agent’s output_.

---

## Why These Prompts Exist

Early versions of the agent produced animations that were:

- Crowded
- Overlapping
- Off-frame
- Text-heavy
- Fragile to prompt phrasing

Trying to “word the prompt better” did not fix this.

What did fix it was changing the mindset entirely:

> From _prompt engineering_ → to **constraint engineering**

Instead of telling the model what we _want_, these prompts define:

- What must **always** be true
- What must **never** happen
- What structural invariants must be preserved
- How layout must be repaired when it breaks
- Where text is allowed to exist
- How diagrams must shrink, reflow, and center
- What layout patterns are treated as **bugs**

The result is an agent that **self-repairs its own layouts**.

---

## What These Prompts Actually Are

They are a **formal layout contract** for a Manim animation generator:

- They define a 16:9 safe frame and padding rules
- They impose strict text-density limits
- They prohibit overlapping text
- They define vertical “bands” for titles, diagrams, equations, notes, and summaries
- They include a mandatory _Layout Debugger Protocol_ the agent must run before finalizing output
- They define autoshrink, recentering, and refactoring rules
- They give the agent explicit permission to **rewrite user-provided code** to enforce clarity and layout safety

These prompts effectively turn an LLM into a **layout-aware diagram engine**.

---

## Folder Contents

You will typically see:

- `MANIM_PROMPT` – The full visual reasoning and layout contract
- `RESPONSE_PROMPT` – Short natural-language summary prompt
- `FRAGMENT_TITLE_PROMPT` – Short concept naming prompt

Together they define the agent’s complete behavior.

---

## How To Modify These Prompts Safely

These prompts are **not stylistic. They are structural.**

Safe changes:

- Adjusting safe-frame dimensions
- Changing font sizes and spacing thresholds
- Adding new layout invariants
- Adding new suspicious patterns to rewrite
- Adding new refactor permissions

Dangerous changes:

- Removing vertical band rules
- Weakening overlap constraints
- Allowing manual coordinates without grouping
- Allowing long text blocks
- Removing autoshrink / recenter rules

If you loosen constraints, the agent _will_ regress into cluttered, fragile, overlapping layouts.

---

## Mental Model

Treat these prompts as:

> **A visual type system for Manim layouts.**

They are not instructions.
They are **invariants the agent must satisfy** before output is considered valid.

---

## Philosophy

This folder is the difference between:

> “An LLM that sometimes draws math”
> and
> **A deterministic visual reasoning machine with layout guarantees.**
