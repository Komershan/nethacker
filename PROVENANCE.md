# merge-0926

This program merges three lines of work. All three started from the same parent, daglar-dragomirov/nethacker@43cbe5a, on 2026-09-26.

| Source | Commit | What was taken |
|---|---|---|
| Komershan, ryzen run (13-role union) | `Komershan/nethacker@8e0c325` | Force bolt for Wizards, skipping exploration on the way down for gnomes and dwarves, the Xp 9 grind for hostile races (off under `all8`) |
| Komershan, m5 run (union) | `Komershan/nethacker@8e0e320` | Hunger-prayer timing, the Elbereth vigil while fainting, threat prayer, no more prayer after an angered god, digging down the Mines to Mines' End, the Xp 8 grind (`all8`) |
| daglar-dragomirov | `daglar-dragomirov/nethacker@7a65e41` | Fixes only: bounded message and panic histories (the verifier OOM), the exact prayer HP threshold (`critically_low_hp`), corpse age 30, the "hands busy" container stall, stale altars, Sokoban desync, rays that avoid peacefuls, the Tourist's magic mapping, the cockatrice touch guard, Monk healing, dragon-scale names, skipping exploration while diving. His per-role grind table is kept behind `GRIND_POLICY = 'roles'`. |

His force bolt is dropped in favour of the ryzen one: two functions with the same name would shadow each other.

## Grind policy

`GRIND_POLICY` in `autoascend/global_logic.py` selects the Dlvl 1 grind policy. It is set to **`all8`**: every role grinds to Xp 8.

Each policy was scored on held-out seeds, 13 roles × 6 trajectory ids starting at 1000, with the same games for every build (`scripts/heldout_eval.py`):

| Build | Held-out mean |
|---|---|
| merge, `all8` | **0.1219** |
| merge, `roles` | 0.1041 |
| merge, `split` | 0.1005 |
| ryzen union, unmerged | 0.0957 |

Paired bootstrap for `all8` minus `split`: +0.021, 95% CI [-0.004, +0.046].

Nearly all of the gain comes from the Monk and the Valkyrie, which do better grinding to Xp 8 than leaving at Xp 5 or 7. On the other 11 roles the three policies are within noise of each other.

## Credits

The ideas inside come from many people. See `shared/CREDITS.md` and `shared/IDEAS.md`. Name them when you register a descendant of this program.
