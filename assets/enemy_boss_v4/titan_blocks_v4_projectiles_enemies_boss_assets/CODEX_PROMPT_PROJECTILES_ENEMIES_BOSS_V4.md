Codex prompt: Titan Blocks V4 projectiles, enemies, and boss assets

Goal:
Integrate the V4 true-overhead projectile, enemy, and boss PNG assets into Titan Blocks without breaking existing mechanics.

Camera rule:
Everything is 100% directly overhead. No isometric interpretation.

Folder:
`/assets/v4_combat/`

Projectile integration:
1. Use frame sequences for animated projectiles.
2. Rotate projectile sprites toward their velocity angle.
3. Keep current projectile hitboxes and damage logic.
4. Map current weapons:
   - BLASTER -> tb_v4_proj_blaster_frame_00-03
   - Homing missile / MISSILE -> tb_v4_proj_homing_frame_00-05 or tb_v4_proj_missile_frame_00-03
   - LASER -> tb_v4_proj_laser_frame_00-05 stretched along beam direction if needed
   - BOMB -> tb_v4_proj_bomb_frame_00-03
   - NAPALM -> tb_v4_proj_napalm_frame_00-05
   - PIERCE -> tb_v4_proj_pierce_frame_00-03
5. Bomb explosion uses tb_v4_fx_bomb_explosion_frame_00-07.
6. Nova/screen clear uses tb_v4_fx_nova_screen_burst_frame_00-07.
7. Napalm burn zone uses tb_v4_fx_napalm_pool_frame_00-05.

Enemy integration:
1. Keep existing enemy AI and hitboxes.
2. Replace enemy square visuals with top-down modular enemy wraps.
3. Enemy types:
   - chaser -> magenta core/claws/thruster
   - charger -> orange core/claws/thruster
   - splitter -> purple core/claws/thruster
   - sniper -> yellow core/claws/thruster
   - hunter -> red core/claws/thruster
4. Draw order:
   - thruster
   - left/right claw
   - core
   - health bar / glow
5. Use assembled preview files only for reference, not as the main implementation if modular drawing is available.

Boss integration:
1. Keep existing boss behavior, HP, bullet patterns, slam shockwave, and rewards.
2. Replace visual with modular Goliath boss:
   - tb_v4_boss_goliath_core_true_overhead.png
   - tb_v4_boss_goliath_left_arm_true_overhead.png
   - tb_v4_boss_goliath_right_arm_true_overhead.png
   - tb_v4_boss_goliath_left_leg_true_overhead.png
   - tb_v4_boss_goliath_right_leg_true_overhead.png
   - tb_v4_boss_goliath_cannon_true_overhead.png
   - tb_v4_boss_goliath_shield_ring_true_overhead.png
3. Animate boss arms with slight rotation, cannon recoil during fire, shield pulse on spawn, and core glow on hit.
4. Keep the boss hitbox as the original circle/rectangle logic. Do not use visual bounds for collision.

Debug:
Add console logs:
- `[TitanCombatV4] projectiles loaded`
- `[TitanCombatV4] enemies loaded`
- `[TitanCombatV4] boss loaded`
- `[TitanCombatV4] drawing projectile <type>`
- `[TitanCombatV4] drawing enemy <type>`
- `[TitanCombatV4] drawing boss Goliath`

Success check:
The game should keep the exact mechanics, but bullets, enemies, boss, explosions, lasers, napalm, and homing missiles should look like premium direct-overhead assets.
