Codex prompt: Titan Blocks V4 true-overhead character wrap assets

Goal:
Use the V4 true-overhead PNG assets as armor caps on top of the existing square/block player. Keep the original character mechanics exactly as they are.

Critical visual rule:
These assets are 100% directly overhead. Treat the camera like it is looking straight down from the sky onto the top of the character's head. Do not interpret these as side-view, angled, or isometric art.

Important:
The old block character is the skeleton. Do not replace it. The existing blocks already have the movement, arm motion, leg motion, gun recoil, rotation, dash, and hitbox that Frank likes. These PNGs should simply wrap on top of those original moving blocks.

Folder:
`/assets/player_wrap_v4/`

Recommended implementation:
1. Load the V4 PNGs into an image cache.
2. Locate the existing player draw function where torso, arms, legs, and gun are drawn as square/rect shapes.
3. Keep the existing mechanics and coordinates.
4. For each original block part, draw the matching PNG over it:
   - torso block -> tb_v4_wrap_torso_true_overhead.png
   - head/core block -> tb_v4_wrap_head_true_overhead.png
   - left arm block -> tb_v4_wrap_left_arm_true_overhead.png
   - right arm block -> tb_v4_wrap_right_arm_true_overhead.png
   - left leg block -> tb_v4_wrap_left_leg_true_overhead.png
   - right leg block -> tb_v4_wrap_right_leg_true_overhead.png
   - gun rectangle -> active gun PNG
5. Use the same x, y, rotation, and animation timing as the existing block part.
6. Scale each PNG so it covers the old block but still lets overlapping parts create depth.
7. Keep the original circular player hitbox exactly the same.
8. Add a toggle key `O` to show/hide the wrap layer for comparison.
9. Add console logs:
   - `[TitanWrapV4] assets loaded`
   - `[TitanWrapV4] drawing true overhead wraps`

Draw order:
1. thruster frame behind torso
2. leg wraps
3. shin/foot wraps if supported
4. arm wraps
5. forearm/hand wraps if supported
6. torso wrap
7. head wrap
8. active gun wrap
9. shield/hit effects

Weapon mapping:
- BLASTER -> tb_v4_wrap_gun_blaster_true_overhead.png
- LASER -> tb_v4_wrap_gun_laser_true_overhead.png
- MISSILE -> tb_v4_wrap_gun_missile_true_overhead.png
- BOMB -> tb_v4_wrap_gun_bomb_true_overhead.png
- NAPALM -> tb_v4_wrap_gun_bomb_true_overhead.png

Preview file:
Use `tb_v4_preview_true_overhead_wrap_on_original_blocks.png` only to understand the concept. Do not use it as the in-game sprite.

Success check:
The player should still move exactly like the original animated square/block character. The difference is that the squares now look like premium top-down armor plates from a straight overhead view.
