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

## gapwitness (2026-08-20): the rule applied to OPH's actual graph

* `OphGap/Checker.lean` — a certificate checker `check n es cyc : Bool` (spanning tree rooted at
  vertex 0 given by edge order; negative closed walk given by edge indices) and its SOUNDNESS
  `posDef_of_check : check n es cyc = true → (Dᵀ D).PosDef`, zero `sorry`.
* `OphGap/OphData.lean` — the frozen OPH visible seam complex, 8,662 nodes / 11,816 edges, all
  signs −1, regenerated from `MAIN_CONFIG` (seed 20260751) and matched byte-for-byte to the
  receipt's `domain_freeze_sha256 = a0be6fc6…`; vertices BFS-relabelled from the witness start.
* `OphGap/OphWitness.lean` — `check_true` is decided by the Lean KERNEL (`decide +kernel`, no
  `native_decide`), giving `oph_gram_posDef`, `oph_eigenvalues_pos`, `oph_kernel_trivial` for the
  real graph. Negative control `tampered_refused`: flipping ONE sign on a witness edge makes the
  kernel reject the same certificate.

See `/home/monkey/gapwitness-report.md`.
