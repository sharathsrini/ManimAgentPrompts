# Layout Debugger / Overlap Fix Protocol

Whenever you see existing Manim code, especially when the user mentions "overlap", "crowded", or "layout problem", you MUST run this protocol **before** finalizing edits:

## Step 1: Identify all text/equation blocks

Collect every `Text`, `Tex`, and `MathTex` object in the scene. For each, mentally tag:
- **ROLE:** title, subtitle, main problem, explanation/panel, note, equation band, axis label, final result, other
- **ANCHOR:** what it is placed relative to (digits, main diagram, axis, etc.)

## Step 2: Bucket into vertical bands

- **Top band:** titles / subtitles
- **Middle band:** main diagram / digits / graph
- **Lower band(s):** explanations, panels, equations, notes
- **Final band:** final result / summary

If multiple items share the *same band* and are long, they must be arranged with `VGroup(...).arrange(DOWN/RIGHT)` instead of manual coordinates.

## Step 3: Detect risky layout patterns

You MUST treat the following as suspicious and fix them:

- Text or MathTex placed with manual coordinates, e.g.:
  ```python
  some_text.move_to([x_value, y_value, 0])
  ```
- Many text objects using the same y coordinate with different x, or tiny vertical gaps:
  `y = 0.0` for multiple texts, `buff < 0.3`
- Vertical placement using `next_to(..., DOWN, buff < 0.3)` for phrase + equation that live in the same area
- Notes or panels using magic numeric thresholds (tiny offsets like `+0.1`, `+0.12`) instead of robust VGroup arrange

## Step 4: Rewrite layout using stacked groups

For vertical bands, PREFER this pattern:

```python
band = VGroup(block1, block2, block3)
band.arrange(DOWN, buff=0.4)
band.next_to(reference_group, DOWN, buff=0.5)
band.set_x(0)
```

Explanations + equations should usually live in a shared band:

```python
explanation_band = VGroup(panel, equation_slot)
explanation_band.arrange(DOWN, buff=0.4)
explanation_band.next_to(main_diagram, DOWN, buff=0.6)
explanation_band.set_x(0)
```

Do NOT rely on fixed y coordinates for phrases or equations if they might stack.

## Step 5: Enforce minimum vertical gap

When stacking any two text-like elements:

```python
VGroup(top, bottom).arrange(DOWN, buff >= 0.35)
```

If your mental layout suggests they are close, increase buff to 0.45 or reduce `font_size`.

## Step 6: Shorten or split long phrases

If any Text has more than ~35-40 characters:
- Rewrite it into a shorter phrase, OR
- Split into two lines or two stacked Text objects arranged with `VGroup(...).arrange(DOWN)`

## Step 7: Final "mental collision check"

- Titles should not share vertical space with panels or equations.
- Panels and equations should not share the same approximate y-range.
- Notes should not inhabit the exact same band as panels or equations: prefer notes ABOVE the highlighted column or ABOVE the main diagram rather than squeezed between panel and equation.

If any of these checks feels even slightly at risk, you MUST adjust positions, font sizes, and grouping until the vertical bands are clearly separated.

---

## Suspicious Layout Patterns You Must Rewrite

When modifying existing code, you MUST treat these patterns as bugs and rewrite them:

- Multiple Text/Tex/MathTex placed with `.move_to([...])` near the same y coordinate
- Text or equations positioned with "magic numbers" like:
  ```python
  obj.next_to(other, DOWN, buff=0.2)
  obj.move_to([x_h, y_bottom - 0.25, 0])
  ```
- Helper functions that:
  - Place panels or notes with fixed buff but no VGroup stacking
  - Place notes BELOW a target that already has a panel or equation below it

For any such pattern, you MUST:
- Replace manual coordinates with relative positioning + `VGroup.arrange`
- Increase vertical separation until panels, notes, and equations clearly live in different vertical bands
- Simplify or shorten text if needed to keep everything readable
