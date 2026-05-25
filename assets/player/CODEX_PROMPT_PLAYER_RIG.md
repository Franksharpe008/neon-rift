Codex prompt for Titan Blocks modular main character rig:

Use the PNG files from `/assets/player/` to replace the simple block player with a modular top-down mech character.

Important:
- Do not use the assembled preview as the game sprite. It is only a visual reference.
- Load individual body parts and draw them with pivots so arms and legs can animate.
- Keep the character readable at small size.
- Preserve the existing hitbox size and player controls.
- Rotate the whole rig toward the mouse aim angle.
- Use the current weapon state to choose the weapon PNG.

Recommended drawing order:
1. thruster flame if moving/dashing
2. legs: thighs, shins, feet
3. torso
4. upper arms
5. forearms
6. hands
7. weapon
8. head
9. shield/hit effects

Animation requirements:
- Idle: slight torso bob and arm breathing.
- Walk: alternate leg swing based on player velocity.
- Shooting: short recoil on forearm and weapon.
- Dash: show larger thruster flame and cyan trail.
- Shield active: draw `tb_fx_player_shield_flash_cyan.png` with additive/glow.
- Damage: flash `tb_fx_player_hit_spark_red.png`.

Suggested API:
```js
const TitanPlayerRig = {
  loadAssets(),
  draw(ctx, {
    x, y,
    aimAngle,
    velocityX,
    velocityY,
    weaponName,
    isShooting,
    isDashing,
    shieldActive,
    damagedAt,
    time
  })
};
```

Use `tb_player_rig_manifest.json` for suggested pivots and anchors.

Files to copy into `/assets/player/`:
- tb_player_torso_core_topdown.png
- tb_player_head_helmet_topdown.png
- tb_player_left_upper_arm_topdown.png
- tb_player_right_upper_arm_topdown.png
- tb_player_left_forearm_topdown.png
- tb_player_right_forearm_topdown.png
- tb_player_left_hand_topdown.png
- tb_player_right_hand_topdown.png
- tb_player_left_thigh_topdown.png
- tb_player_right_thigh_topdown.png
- tb_player_left_shin_topdown.png
- tb_player_right_shin_topdown.png
- tb_player_left_foot_topdown.png
- tb_player_right_foot_topdown.png
- tb_weapon_blaster_topdown.png
- tb_weapon_laser_cannon_topdown.png
- tb_weapon_missile_launcher_topdown.png
- tb_weapon_bomb_cannon_topdown.png
- tb_player_thruster_flame_frame_00.png through tb_player_thruster_flame_frame_03.png
- tb_fx_player_hit_spark_red.png
- tb_fx_player_shield_flash_cyan.png
