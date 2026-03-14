# Code Remix / Refactor Rules

When the user provides code, or says "modify this", "add to this", "extend this", "remix this", or similar:

## Rule 0: Layout and clarity override preservation

If the existing code conflicts with any layout invariant or makes the scene hard to read, you MUST prioritize fixing those issues, even if that requires large refactors.

## Rule 0b: Layout debugger mode

If the user mentions overlap or layout problems explicitly, you MUST enter "layout debugger mode":
- Run the full Layout Debugger / Overlap Fix Protocol (see [layout-debugger.md](layout-debugger.md))
- Rewrite ALL text/equation placement logic that is fragile, not just a few lines
- It is better to rebuild the layout section completely than to leave any risky overlaps

## Rule 1: Treat existing code as a draft

Use the user's code to understand the intent, main objects, and structure. You are NOT required to make only minimal edits. You may reorganize, simplify, or rewrite big portions of the scene to achieve a clean layout and clear storyboard.

## Rule 2: Preserve the mathematical idea, not every line

Keep the same high-level concept, class name(s), and any clearly meaningful variable names when possible. Everything else (positions, grouping, timings, intermediate text) may be changed freely.

## Rule 3: Be bold in refactoring

You are explicitly allowed to:
- Change positions, `font_size`, `buff`, and alignment of any Text/Tex/MathTex
- Split long text blocks into shorter phrases or merge multiple short blocks
- Replace long sentences with short labels
- Regroup mobjects into new VGroups and re-arrange them
- Remove redundant text or animations that do not help understanding
- Extract helper methods or restructure `construct()` for cleaner logic

## Rule 4: Reuse what works, fix what doesn't

If a part of the existing code already respects layout invariants and is clear, you MAY keep it. If a part causes overlap, clutter, or pushes content outside the frame, rewrite it without hesitation.

## Rule 5: Rewrite entire scene if needed

If overlapping or off-frame problems appear in multiple places, it is better to rewrite the entire `construct()` body using the same class name and concept, rather than patching small pieces.

## Rule 6: Class naming

Keep the same class name unless the user explicitly asks to change it. You may change the internal implementation completely if needed.

## Rule 7: Text safety heuristic

For every Text/Tex/MathTex you KEEP or CREATE:
- Place it relative to something (`next_to`, `to_edge`, `aligned_edge`)
- Keep it inside x in [-5, 5]
- Prefer BELOW or ABOVE the right-most diagram rather than to its RIGHT
- Put final summary text BELOW and centered under the main diagram

## Rule 8: Do not blindly preserve bad layout

Never keep overlapping or cramped layout just because it appears in the original code. Your job is to improve the scene: make it cleaner, more legible, and more visually structured than the original, even if that means substantial changes.

These remix rules override storyboard simplification: when modifying existing code, you SHOULD improve the storyboard and layout, not just bolt new lines onto the old structure.
