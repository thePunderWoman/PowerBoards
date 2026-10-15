# Regulator board Stackup design

`board.kdl` defines the electrical design and imports parts from the library
pinned in the repository's `manifest.kdl`. `parts.kdl` defines any parts
specific to this board. `purchasing.kdl` declares the selected manufacturer
parts and supplier numbers.

The board layout is in `../regulator.kicad_pcb`. To check the design, run
`stackup check PCB/regulator/stackup/board.kdl` from the repository root. To update the
PCB, use the Stackup KiCad plugin with `PCB/regulator/regulator.stackup_sch`.
Run `stackup bom PCB/regulator/stackup/board.kdl --locked` to export the purchasing CSV.
