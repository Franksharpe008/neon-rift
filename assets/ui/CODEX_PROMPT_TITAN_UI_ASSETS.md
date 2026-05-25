Codex prompt for Titan Blocks UI asset integration:

You are patching the local browser game Titan Blocks: Neon Rift.

Goal:
Integrate the provided individual PNG UI assets from `/assets/ui/` as premium animated overlays without breaking the existing game mechanics, music patch, boss logic, power-ups, or controls.

Assets to use:
- `/assets/ui/tb_ui_mission_update_panel.png`
- `/assets/ui/tb_ui_powerup_acquired_panel.png`
- `/assets/ui/tb_ui_panic_burst_panel.png`
- `/assets/ui/tb_ui_boss_battle_panel.png`
- `/assets/ui/tb_ui_boss_cleared_panel.png`
- `/assets/ui/tb_ui_score_counter_panel.png`
- `/assets/ui/tb_ui_music_status_panel.png`
- `/assets/ui/tb_ui_nova_bomb_panel.png`

Implementation requirements:
1. Create a new visual overlay system named `TitanOverlayFX`.
2. Do not replace the current HUD. Add these as event overlays on top of the canvas.
3. Use the PNG as the background image of each overlay card.
4. Render live dynamic values on top of the PNG using HTML text or canvas text:
   - score
   - level
   - weapon name
   - timer seconds
   - boss HP percent
   - combo/multiplier
   - active music track
5. Animate overlays with:
   - slide down from top
   - scale from 0.94 to 1.0
   - opacity fade in/out
   - neon pulse
   - timer/progress bar width animation
6. Trigger overlays from existing game events:
   - mission update when level changes
   - power-up acquired when a core is collected or shot
   - panic burst when E or right-click is used
   - boss battle when the boss spawns
   - boss cleared when the boss dies
   - nova bomb/bomb/napalm when a screen-clear or explosion happens
   - music status when Orbital Lockdown or Goliath starts
7. Preserve all current game controls and mechanics.
8. Keep a backup of `index.html` before patching.
9. Add cache-busted asset URLs when testing, e.g. `tb_ui_boss_battle_panel.png?v=1`.
10. Add `console.log` lines for each overlay trigger so we can verify events in DevTools.

Suggested API:
```js
window.TitanOverlayFX = {
  missionUpdate({score, level, boost}),
  powerupAcquired({name, timer, score, level}),
  panicBurst({radius, damage, cooldown}),
  bossBattle({bossName, bossHp, level}),
  bossCleared({scoreBonus, nextWave}),
  novaBomb({damage, radius}),
  musicStatus({trackName, bpm, loopEnd})
};
```

CSS behavior:
- `.titan-overlay-card` should be position fixed, pointer-events none, z-index very high.
- Use background-image with the matching PNG.
- Use CSS variables for progress width and glow color.
- Use `@keyframes overlayIn`, `overlayOut`, `neonPulse`, and `timerDrain`.

Success check:
When the game starts, show `tb_ui_music_status_panel.png`.
When a power-up is collected, show `tb_ui_powerup_acquired_panel.png`.
When E is pressed, show `tb_ui_panic_burst_panel.png`.
When the boss starts, show `tb_ui_boss_battle_panel.png`.
