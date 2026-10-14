---
name: terminal-math
description: >
  Write math so it reads correctly in a terminal (Claude Code, Codex, any CLI
  agent) instead of raw LaTeX. Use whenever a reply contains any equation,
  formula, derivation, matrix, integral, sum, limit, or proof step, or when the
  user says "render math", "show the equation", "pretty print math". Display
  math goes in a code block as multi-line Unicode art; short inline math uses
  Unicode symbols. Never output $...$, \frac, \int or other LaTeX source unless
  the user explicitly asks for LaTeX.
---

# Terminal Math

The terminal does not render LaTeX. Raw `$\frac{a}{b}$` is noise. Draw the math.

## Rules

1. **Never emit LaTeX source** (`$...$`, `\[...\]`, `\frac`, `\sum`, ...) unless the
   user asks for LaTeX code to copy (then give it in a ```latex block, in
   addition to the drawing).
2. **Inline math** (short, inside a sentence): Unicode symbols on one line.
   `x² + y² = r²`, `α ≤ β`, `f′(x)`, `√2`, `n!`, `aᵢⱼ`, `e^(iπ)`, `a/b`.
   Use superscript/subscript characters when they exist (`⁰¹²³⁴⁵⁶⁷⁸⁹⁺⁻⁼⁽⁾ⁿⁱ`,
   `₀₁₂₃₄₅₆₇₈₉₊₋₌₍₎ₐₑₒₓᵢⱼₖₙₘₚₜ`); otherwise fall back to `^(...)` / `_(...)`.
3. **Display math** (anything with a fraction, big operator, matrix, or more than
   ~1 level of nesting): a fenced code block with no language tag, drawn over
   multiple lines, so monospace alignment holds.
4. Align on the baseline: the main line of the equation (where `=` sits) is the
   middle row; numerators above, denominators below, limits above/below operators.
5. Multi-step derivations: one step per line, `=` signs vertically aligned.
6. Keep every mathematical fact exact. Pretty layout never replaces correctness;
   if a construct can't be drawn clearly, write it in linear Unicode instead.
7. After drawing, check widths: fraction bars must span the wider of numerator
   and denominator, and everything must be centered over its bar.

## Symbol palette

```
Greek    α β γ δ ε ζ η θ ι κ λ μ ν ξ π ρ σ τ υ φ χ ψ ω   Γ Δ Θ Λ Ξ Π Σ Φ Ψ Ω
Ops      ± ∓ × ÷ · ∘ ⊗ ⊕ ∇ ∂ ∫ ∬ ∮ ∑ ∏ √ ∛ ∞ ′ ″
Rel      = ≠ ≈ ≡ ≤ ≥ ≪ ≫ ∝ ∼ ≅ ⇒ ⇔ → ← ↦ ⟹ ⟺
Sets     ∈ ∉ ⊂ ⊆ ⊃ ⊇ ∪ ∩ ∅ ℕ ℤ ℚ ℝ ℂ ∀ ∃ ¬ ∧ ∨
Misc     ⟨ ⟩ ‖ ⌊ ⌋ ⌈ ⌉ ħ ℓ °  vectors: bold isn't available, use v⃗ or 𝐯
Drawing  ─ │ ╱ ╲ ⌠ ⎮ ⌡ ⎛ ⎜ ⎝ ⎞ ⎟ ⎠ ⎡ ⎢ ⎣ ⎤ ⎥ ⎦ ⎧ ⎨ ⎩ ⎫ ⎬ ⎭
```

## Patterns

Fraction and root (`x =` sits on the bar row):
```
            ________
     -b ± ╲╱b² - 4ac
x = ─────────────────
           2a
```

Integral with limits:
```
 ∞               _
 ⌠    -x²      ╲╱π
 ⎮   e    dx = ───
 ⌡              2
-∞
```

Sum / product (⎲ ⎳ form the Σ; use ∏ inline for products):
```
 ∞
 ⎲   1     π²
 ⎳  ─── = ───
n=1  n²    6
```

Limit:
```
      sin x
 lim  ───── = 1
x→0     x
```

Derivative / partial:
```
∂u       ∂²u
── = α  ───
∂t       ∂x²
```

Matrix and determinant:
```
    ⎡ a  b ⎤                 │ a  b │
A = ⎢      ⎥ ,     det A =   │      │ = ad - bc
    ⎣ c  d ⎦                 │ c  d │
```

Piecewise:
```
       ⎧  x    if x ≥ 0
|x| =  ⎨
       ⎩ -x    if x < 0
```

Aligned derivation:
```
(a + b)² = (a + b)(a + b)
         = a² + ab + ba + b²
         = a² + 2ab + b²
```

## Mixing prose and math

Explain in normal markdown; put each displayed equation in its own code block
right where it belongs in the explanation. Refer to symbols in prose with
inline Unicode (`where σ is the standard deviation`), not backtick-LaTeX.
