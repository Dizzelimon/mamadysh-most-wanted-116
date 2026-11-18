# Mamadysh: Most Wanted 116 — v4.0 / Stage 1 (first integration)

This is a **work-in-progress integration**, not a fully tested v4.0 release.

## Modified/added files
- `scripts/MamadyshWorld.gd`: optional v4 map loading, migration-aware road heights, centerline markings.
- `assets/map/mamadysh_map_v4.json`: generated terrain heights and bridge-adjacent road profiles.
- `tools/migrate_map_v4.py`: deterministic, idempotent migration from original v3 JSON.
- `tools/test_map_v4.py`: offline structural and reproducibility checks.

The original `assets/map/mamadysh_map.json` is intentionally unchanged. All original vehicle GLB node contracts and collision layers are retained.

## Reproduce
From project root:

```bash
python3 tools/migrate_map_v4.py assets/map/mamadysh_map.json --output assets/map/mamadysh_map_v4.json
python3 tools/test_map_v4.py
```

## Godot validation (requires Godot 4.3)

```bash
godot --headless --path . --editor --import --quit
godot --headless --path . --quit-after 120
```

Inspect editor output for parser/shader errors, then visually inspect road/terrain boundaries and drive across each bridge at 50/100/150 km/h. The environment used to prepare this package did not have the Godot executable, so no Godot runtime or FPS claims are made.

## Known remaining stage-1 work
- Grade-separated intersections must be verified against the OSM bridge topology.
- Existing coarse terrain cells can still create geometric overlaps; consider local adaptive tessellation for critical road edges.
- Zebra crossings, stop lines, intersection-aware markings, and race start corridor topology repair are not implemented.
- Bridge approach heights are eased in the source data, but jerk/grade continuity has not been dynamically measured.
- World rebuild still uses queue_free for old nodes; rebuild during active physics should be tested separately.
