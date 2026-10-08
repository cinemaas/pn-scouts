# House 1600s Interior - measurement data

Everything here is **metres, Z up**, in the scan's own frame. The origin is
**where the operator stood when the capture started** - not a building corner,
not a geographic datum. Nothing here is georeferenced.

Start with `measurements.json`: it carries the storey heights, the extent, and a
description of every file in this folder.

| file | what it is |
|---|---|
| `drawn.svg` | The same linework over the colour ortho plate. (473.0 KB) |
| `ingest_report.txt` | Everything the ingest measured, in full. (3.4 KB) |
| `levels.json` | Walking-surface height map and storey model. (4.2 KB) |
| `ortho.json` | Georeference for ortho.png: world extent and pixels per metre. (0.2 KB) |
| `ortho.png` | Georeferenced top-down colour plate. (1466.7 KB) |
| `plan.svg` | Drafted wall linework. SVG user units are real millimetres. (7.5 KB) |
| `points.ply` | Decimated splat centres with colour, metres, Z up. ~200k points. (10937.9 KB) |
| `stairs.json` | Detected stair geometry: rise, going, width, direction. (0.4 KB) |
| `walls/line_candidate_list.json` | Candidate wall segments before consolidation. (43.3 KB) |
| `walls/line_limit_z.json` | Floor and ceiling heights (z_ground, z_ceiling), metres. (0.1 KB) |
| `walls/line_result_list.json` | Wall segments, 2D in the X/Y plane. (20.1 KB) |
| `walls/main_dirs.json` | Dominant wall directions, degrees. (0.1 KB) |
| `walls/poses.csv` | Capture trajectory: timestamp, position (m), orientation quaternion. (563.0 KB) |
| `walls/render_param.json` | Sheet extent and scale used for the plan. (0.2 KB) |
| `walls/run_summary.json` | Space-recognition run summary. (0.1 KB) |
| `walls/window_door_candidate_list.json` | Door and window openings along the walls. (1.7 KB) |
| `whitebox.obj` | Wall/floor/ceiling proxy solid, metres, Z up. Openings cut. (9.5 KB) |
| `mesh.ply` | Reconstructed mesh from LCC Studio, metres, Z up. Merged from LCC's 16 split tiles. (1463.6 KB) |

## Deriving a plan

`plan.svg` is already drafted linework in real millimetres and is the fastest
route to a blueprint. For geometry you can measure against, use `whitebox.obj`
(a clean proxy solid) or `mesh.ply` (the reconstruction). `points.ply` is the
raw shape of the space as coloured points.

Walls in `walls/line_result_list.json` are 2D segments; extrude them between
`z_ground` and `z_ceiling` from `walls/line_limit_z.json` to get solid walls,
then cut the openings in `walls/window_door_candidate_list.json`.
