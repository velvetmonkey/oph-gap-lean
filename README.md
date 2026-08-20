# oph-gap-lean

Private, local-only Lean 4 / Mathlib corroboration of the OPH source-gap brick.
No remote. Build only with `/home/monkey/bin/leanbuild build`.

`OphGap/SignedGap.lean` proves, with zero `sorry`:

1. `signed_kinetic_identity` — x ⬝ (Dᵀ D x) = Σ_e (σ_e x(tgt e) − x(src e))².
2. `gram_posDef_of_injective` — injective D ⇒ Dᵀ D positive definite.
3. `triangle_posDef` — the all-negative triangle matrix is positive definite (a CONTROL).
4. `kernel_trivial_of_negative_cycle` / `gram_posDef_of_negative_cycle` — connected +
   a negative signed cycle ⇒ ker D = 0 ⇒ Dᵀ D positive definite (signed-balance-to-injectivity).

Negative control: the all-negative square is shown NOT injective, NOT positive definite,
and to admit NO negative closed walk (`square_no_negative_cycle`).

See `/home/monkey/gapproof-report.md` for the full account.
