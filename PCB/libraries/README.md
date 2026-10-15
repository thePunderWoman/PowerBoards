# Shared KiCad libraries

Symbols (`*.kicad_sym`), footprints (`*.pretty/`) and 3D models (`3dmodels/`) used by more than one
board, or that a board needs and KiCad does not ship. Each board's `sym-lib-table` and `fp-lib-table`
point here with `${KIPRJMOD}/../libraries/...`, so the paths work on any machine that has the repo.

Record where each 3D model came from, and any offset or rotation it needs, in `3dmodels/README.md`.
