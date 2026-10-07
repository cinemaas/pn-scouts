# Eustis Exterior - measurement data

Everything here is **metres, Z up**, in the scan's own frame. The origin is
**where the operator stood when the capture started** - not a building corner,
not a geographic datum. Nothing here is georeferenced.

Start with `measurements.json`: it carries the storey heights, the extent, and a
description of every file in this folder.

| file | what it is |
|---|---|
| `drawn.svg` | The same linework over the colour ortho plate. (8998.1 KB) |
| `ingest_report.txt` | Everything the ingest measured, in full. (6.2 KB) |
| `levels.json` | Walking-surface height map and storey model. (13.0 KB) |
| `mesh.ply` | Reconstructed mesh from LCC Studio, metres, Z up. (14351.9 KB) |
| `ortho.json` | Georeference for ortho.png: world extent and pixels per metre. (0.3 KB) |
| `ortho.png` | Georeferenced top-down colour plate. (19124.1 KB) |
| `plan.svg` | Drafted wall linework. SVG user units are real millimetres. (15.7 KB) |
| `points.ply` | Decimated splat centres with colour, metres, Z up. ~200k points. (10937.9 KB) |
| `stairs.json` | Detected stair geometry: rise, going, width, direction. (4.8 KB) |
| `walls/line_candidate_list.json` | Candidate wall segments before consolidation. (142.2 KB) |
| `walls/line_limit_z.json` | Floor and ceiling heights (z_ground, z_ceiling), metres. (0.2 KB) |
| `walls/line_result_list.json` | Wall segments, 2D in the X/Y plane. (37.4 KB) |
| `walls/main_dirs.json` | Dominant wall directions, degrees. (0.1 KB) |
| `walls/poses.csv` | Capture trajectory: timestamp, position (m), orientation quaternion. (251.1 KB) |
| `walls/render_param.json` | Sheet extent and scale used for the plan. (0.3 KB) |
| `walls/run_summary.json` | Space-recognition run summary. (0.1 KB) |
| `walls/window_door_candidate_list.json` | Door and window openings along the walls. (1.7 KB) |
| `whitebox.obj` | Wall/floor/ceiling proxy solid, metres, Z up. Openings cut. (16.7 KB) |

## Deriving a plan

`plan.svg` is already drafted linework in real millimetres and is the fastest
route to a blueprint. For geometry you can measure against, use `whitebox.obj`
(a clean proxy solid) or `mesh.ply` (the reconstruction). `points.ply` is the
raw shape of the space as coloured points.

Walls in `walls/line_result_list.json` are 2D segments; extrude them between
`z_ground` and `z_ceiling` from `walls/line_limit_z.json` to get solid walls,
then cut the openings in `walls/window_door_candidate_list.json`.
