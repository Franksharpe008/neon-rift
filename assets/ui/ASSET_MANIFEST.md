# Titan Blocks UI Asset Manifest

Place these files in:

`/assets/ui/`

Recommended use:
- Use PNG panels as visual overlays.
- Keep score, level, weapon, boss HP, and timer text as live HTML/canvas text on top of the PNG.
- Do not bake changing numbers into the PNG at runtime.
- Animate the PNG with CSS transforms and opacity.
- Animate the timer bar with CSS width or use the included frame sequence.

Files:
- tb_ui_mission_update_panel.png
- tb_ui_powerup_acquired_panel.png
- tb_ui_panic_burst_panel.png
- tb_ui_boss_battle_panel.png
- tb_ui_boss_cleared_panel.png
- tb_ui_score_counter_panel.png
- tb_ui_music_status_panel.png
- tb_ui_nova_bomb_panel.png
- animation_frames/tb_ui_event_timer_frame_00.png through tb_ui_event_timer_frame_05.png
