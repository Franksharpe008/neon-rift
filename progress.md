Original prompt: Fix the Titan Blocks boss bug where the boss becomes invincible after dashing.

2026-05-25:
- Centralized boss damage and boss clear logic so bullets and flame aura cannot bypass the same death/damage path.
- Validation target: force a boss into dash state, confirm one hit damages during dash, wait for dash to end, then confirm another hit damages after dash.
- Found root cause: boss collision was nested inside the regular enemy loop, so if no enemies were alive the boss never received bullet collision checks.
- Browser validation passed on localhost: during-dash hit reduced HP 1000 -> 950, post-dash hit reduced HP 950 -> 850, final lethal hit cleared the boss and awarded score.
- Reverted the overbroad fullscreen/boss-drop feature after it broke restart flow. Repaired with fullscreen only via the visible FULLSCREEN button or F key; start/restart no longer request fullscreen.
