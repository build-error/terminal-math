# terminal-math

An agent skill that makes AI coding agents (Claude Code, Codex, Copilot, and others) write math that actually reads in a terminal: multi-line Unicode drawings in code blocks, not raw LaTeX.

**Without the skill:**

```
$\int_{-\infty}^{\infty} e^{-x^2}\,dx = \sqrt{\pi}$
```

**With the skill:**

```
 ∞               _
 ⌠    -x²      ╲╱π
 ⎮   e    dx = ───
 ⌡              2
-∞
```

## Install

```
npx skills add build-error/terminal-math --skill terminal-math -g
```

It triggers automatically whenever a reply contains math, or run `/terminal-math`.

## What it covers

- Inline math with Unicode symbols, superscripts, and subscripts: `x² + y² = r²`, `aᵢⱼ`, `α ≤ β`
- Displayed equations drawn over several lines: fractions, roots, integrals, sums, limits, derivatives, matrices, determinants, piecewise functions
- Step-by-step derivations with the `=` signs lined up
- LaTeX source only when you ask for it, given alongside the drawing

## More examples

```
            ________
     -b ± ╲╱b² - 4ac
x = ─────────────────
           2a
```

```
    ⎡ a  b ⎤                 │ a  b │
A = ⎢      ⎥ ,     det A =   │      │ = ad - bc
    ⎣ c  d ⎦                 │ c  d │
```

```
       ⎧  x    if x ≥ 0
|x| =  ⎨
       ⎩ -x    if x < 0
```

## License

MIT
