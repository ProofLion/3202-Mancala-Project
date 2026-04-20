CSCI 3202 — Mancala Project Cheat Sheet

File: 3202_Mancala_Project.ipynb

Summary
- Random moves: `random.seed(109)` (cell 9). `random_move_generator()` gathers non-empty pits and returns `random.choice(valid_pits)` (cell 11).
- Mancala implementation: `class Mancala:` (cell 10).
- 100-game random-vs-random sim: `simulate_games(num_games=100)` (cell 24) and `results = simulate_games(100)` (cell 25). Example output in notebook: P1=51, P2=40, Ties=9, Avg turns ≈43.58.
- Minimax: `clone_game(game)` (cell 28), `minimax_value(...)` and `minimax_best_move(game, depth)` (cell 30). Simulation harness: `simulate_ai_vs_random(...)` and runs for depths 2 & 5 (cell 31–32).
- Alpha-Beta: `alpha_beta_value(...)` and `alpha_beta_best_move(game, depth)` (cell 36). Timed harness: `simulate_alpha_beta_vs_random(...)` and 5/10 ply runs (cell 38–39). Timing comparison harness (minimax timed) in cell 40–41.
- Extra utility: `utility_v2(game, ai_player)` and `alpha_beta_best_move_custom(...)` with `simulate_ab_custom(...)` (cell 47).
- Interview demo: `demo_single_game(...)` — runs 2-ply Minimax and 4-ply Alpha-Beta (cell 51).

Key concepts & short answers (practice-ready)
- How random moves generated: collect non-empty pits and `random.choice()`; seed set for reproducibility (`random.seed(109)`).
- Where is state tree stored: not stored; it's implicit on recursion stack. Each child is a shallow clone via `clone_game()`.
- How best move is found: enumerate legal moves, clone & apply, evaluate with `minimax_value()` (or alpha-beta), choose highest backed-up utility.
- Utility: original = `mancala(AI) - mancala(opp)`. Extra: `utility_v2 = (mancala_diff) + 0.5*(side_diff)` to value mid-game side stones.
- Why deeper plies help: see farther sequences (captures/sweeps) and avoid shortsighted losses; cost grows exponentially (~branching^depth, branching≈6).
- Minimax vs Alpha-Beta: same decisions for fixed depth/utility; alpha-beta prunes branches using alpha/beta bounds → much less work.

Rubric checklist (what to show & one-line phrasing)
- Intermediate report: show cells 24–25. Phrase: “My random-run produced P1=51, P2=40, Ties=9, avg turns ≈43.6 — small first-player advantage.”
- Minimax: show clone/minimax cells (28–32). Run 2-ply during interview. Phrase: “Minimax reasons about replies and sets up captures; even 2-ply wins vs random.”
- Alpha-Beta: show alpha-beta cells (36–41). Show timing comparison (cell 41). Phrase: “Alpha-Beta prunes and is much faster; 5→10 without pruning scales ~7776×.”
- Extra credit: show `utility_v2` and `simulate_ab_custom` (cell 47). Phrase: “Add 0.5× side-stones because they sweep at end — gives a richer mid-game signal.”

Quick run commands (copyable)
- 2-ply Minimax demo:
```python
demo_single_game(minimax_best_move, depth=2, label="Minimax demo")
```

- 4-ply Alpha-Beta demo:
```python
demo_single_game(alpha_beta_best_move, depth=4, label="Alpha-Beta demo")
```

Numbers & talking points to quote
- Random-vs-random example: P1=51, P2=40, Ties=9, Avg turns ≈43.58.
- Branching ≈ 6 → nodes ~6^d, so 5→10 multiplies by ~6^5 ≈ 7776.

Conversion instructions (to PDF)
- Option A (quick, cross-platform): open `3202_Cheat_Sheet.md` in VS Code or a browser extension and print → Save as PDF.
- Option B (pandoc): if pandoc is installed, run in project folder:
```bash
pandoc 3202_Cheat_Sheet.md -o 3202_Cheat_Sheet.pdf
```

Next steps
- I can produce a one-page PDF for you locally if you want — I can attempt to run `pandoc` here (if installed) or instruct you how to convert. Or I can create a styled HTML and you can print to PDF. Which do you prefer?