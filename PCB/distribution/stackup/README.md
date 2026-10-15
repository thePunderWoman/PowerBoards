# Distribution board Stackup design

`board.kdl` defines the electrical design and imports parts from the library
pinned in the repository's `manifest.kdl`. `parts.kdl` defines the WAGO
2601-1102 terminal block, including its MPN and LCSC number, so this board
needs no separate `purchasing.kdl`.

The board layout is in `../distribution.kicad_pcb`. To check the design, run
`stackup check PCB/distribution/stackup/board.kdl` from the repository root. To update the
PCB, use the Stackup KiCad plugin with `PCB/distribution/distribution.stackup_sch`.
Run `stackup bom PCB/distribution/stackup/board.kdl --locked` to export the purchasing CSV.
