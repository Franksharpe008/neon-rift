Codex prompt for Titan Blocks top-down environment assets:

Use the individual PNG files from `/assets/environment/` to upgrade the Titan Blocks arena.

Design goals:
1. Keep the current top-down shooter mechanics intact.
2. Replace the plain background grid with a layered top-down battlefield.
3. Use grass and dirt tiles as repeating terrain.
4. Place rock clusters, foliage, cover wall segments, neon crystals, and sci-fi base pads as decorative and tactical props.
5. Use enemy spawn gates or clear map-edge lanes so enemy entry is predictable but still threatening.
6. Do not block the player unfairly. Leave open movement lanes.
7. Keep the center of the arena readable. Most props should sit around the outer third of the map or as small cover islands.
8. Add parallax/lighting only if it does not hurt performance.

Suggested map layout:
- Center: open dirt/grass combat lane.
- Corners: sci-fi base pads and neon crystals.
- Left/right edges: enemy spawn gate zones.
- Outer ring: boulders and foliage.
- Tactical cover: 3 to 5 small cover clusters that do not trap the player.

Implementation notes:
- Use `drawImage()` for the props.
- Cache loaded images before the game loop.
- Add a `mapProps` array with `{img, x, y, w, h, collision, glow}`.
- Use simple circular collision only for large boulders and cover walls.
- Keep prop draw order:
  1. ground tiles
  2. paths
  3. low props
  4. player/enemies/projectiles
  5. tall props/glow overlays
  6. HUD

Required trigger points:
- Draw `tb_env_enemy_spawn_gate_magenta.png` near enemy spawn lanes.
- Use `tb_player_ship_topdown_cyan.png` as the player visual if it fits the style.
- Keep the existing block character fallback if image loading fails.
