# Codex Test Instructions: Current Mecha Assets Through Batch 04

## Goal
Test the current Titan Blocks premium mecha assets without disrupting the existing game.

## What is ready to test
The current assets are enough to test a player visual wrap prototype for:
- torso/core
- head/helmet
- shoulders
- reactor/glow overlays
- early thruster/back modules

They are not enough yet for the complete final mecha because we still need arms, hands, legs, feet, weapons, projectiles, FX, enemies, and boss pieces.

## Critical rule
Do not change mechanics. The original V4 block/square player remains the animation skeleton.

Preserve:
- movement
- hitboxes
- arm motion
- leg motion
- gun rotation
- recoil
- dash
- power-ups
- scoring
- HUD
- music
- enemy AI
- boss logic

## Folder placement
Place the batch folders like this:

assets/mecha_library_raw/
  batch_01_foundation/
  batch_02_armor_modules/
  batch_03_player_torso_core/
  batch_04_player_head_shoulders/

Then create a temporary test folder:

assets/player_wrap_v6_test/
  body_wraps/
  head_wraps/
  shoulder_wraps/
  glow_overlays/
  thruster_frames/

## Batch 03 mappings
From batch_03_player_torso_core:
- player_torso_main_overhead.png -> body_wraps/player_torso_main_overhead.png
- player_torso_white_gold_plate_overhead.png -> body_wraps/player_torso_white_gold_plate_overhead.png
- player_torso_black_underframe_overhead.png -> body_wraps/player_torso_black_underframe_overhead.png
- player_chest_core_blue_overhead.png -> glow_overlays/player_chest_core_blue_overhead.png
- player_core_glow_overlay_overhead.png -> glow_overlays/player_core_glow_overlay_overhead.png
- player_back_reactor_overhead.png -> thruster_frames/player_back_reactor_overhead.png
- player_hip_connector_overhead.png -> body_wraps/player_hip_connector_overhead.png
- player_upper_spine_plate_overhead.png -> body_wraps/player_upper_spine_plate_overhead.png
- player_lower_spine_plate_overhead.png -> body_wraps/player_lower_spine_plate_overhead.png
- player_torso_damage_variant_overhead.png -> body_wraps/player_torso_damage_variant_overhead.png

## Batch 04 mappings
From batch_04_player_head_shoulders:
- player_head_helmet_overhead.png -> head_wraps/player_head_helmet_overhead.png
- player_head_visor_glow_overhead.png -> glow_overlays/player_head_visor_glow_overhead.png
- player_head_damage_variant_overhead.png -> head_wraps/player_head_damage_variant_overhead.png
- player_left_shoulder_white_gold_overhead.png -> shoulder_wraps/player_left_shoulder_white_gold_overhead.png
- player_right_shoulder_white_gold_overhead.png -> shoulder_wraps/player_right_shoulder_white_gold_overhead.png
- player_left_shoulder_dark_overhead.png -> shoulder_wraps/player_left_shoulder_dark_overhead.png
- player_right_shoulder_dark_overhead.png -> shoulder_wraps/player_right_shoulder_dark_overhead.png
- player_neck_connector_overhead.png -> head_wraps/player_neck_connector_overhead.png
- player_head_core_light_overhead.png -> glow_overlays/player_head_core_light_overhead.png
- player_shoulder_thruster_pair_overhead.png -> thruster_frames/player_shoulder_thruster_pair_overhead.png

## Test implementation
Add a debug toggle:

O = toggle premium mecha wrap on/off

When O is off:
- draw original player exactly as before.

When O is on:
- draw original block skeleton at low alpha for debugging.
- draw Batch 03 torso/core assets over the torso transform.
- draw Batch 04 head/shoulder assets over the head and shoulder transforms.
- do not replace arm, hand, leg, foot, or weapon visuals yet unless placeholder wrapping is needed.

## Temporary draw order
1. original shadow
2. player_back_reactor_overhead.png if dash/thruster layer is needed
3. player_torso_black_underframe_overhead.png
4. player_hip_connector_overhead.png
5. player_upper_spine_plate_overhead.png
6. player_lower_spine_plate_overhead.png
7. player_torso_main_overhead.png
8. player_torso_white_gold_plate_overhead.png
9. player_chest_core_blue_overhead.png
10. player_core_glow_overlay_overhead.png
11. player_neck_connector_overhead.png
12. shoulder dark underplates
13. shoulder white/gold plates
14. player_head_helmet_overhead.png
15. player_head_visor_glow_overhead.png
16. player_head_core_light_overhead.png
17. damage variants only when low health or hit state is active

## Scale and pivot testing
Use the original player center as the torso pivot.
Suggested initial scale:
- torso/core: 0.22 to 0.35 of source image size depending on canvas resolution
- head: 0.12 to 0.22
- shoulders: 0.12 to 0.24
- glow overlays: match the torso/head piece they attach to

Do not hardcode final scale. Add one debug config object:

const MechaWrapTuning = {
  torsoScale: 0.28,
  headScale: 0.16,
  shoulderScale: 0.18,
  glowAlpha: 0.85,
  debugBlocks: true
};

## Success condition for this test
The player should still play exactly the same, but should visually show a premium top-down mecha torso/head/shoulder wrap. If the scale or pivot is off, tune only the visual offset and scale. Do not touch game mechanics.
