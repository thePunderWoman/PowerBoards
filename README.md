# Power Boards

Small PCBs for power regulation and distribution.

Each board's electrical design is written in [Stackup](https://github.com/stackup-eda/stackup) KDL, which
is the source of truth for the circuit; there are no KiCad schematics. The layout is done in KiCad
(currently 10), linked to the KDL through a `.stackup_sch` file and synced with the Stackup KiCad plugin.

## Boards

| Board | Folder | Purpose | Status |
|---|---|---|---|
| Regulator | [`PCB/regulator/`](PCB/regulator) | Power regulation | Not started |
| Distribution | [`PCB/distribution/`](PCB/distribution) | Six interchangeable power terminals (any one can be the input) over shared V+ and GND planes, WAGO 2601 lever terminals | Initial layout done |

## Repository layout

| Path | Contents |
|---|---|
| [`manifest.kdl`](manifest.kdl) | Stackup version and the parts library, pinned by commit. Shared by every board |
| `PCB/<board>/` | One folder per board: its KiCad project (`<board>.kicad_pro`, `.kicad_pcb`, `.stackup_sch`) and the folders below |
| `PCB/<board>/stackup/` | `board.kdl` (circuit), `parts.kdl` (board-specific parts), `purchasing.kdl` (manufacturer and supplier choices) |
| `PCB/<board>/diagrams/` | Layout floorplans for circuits with real layout stakes (switching loops, thermal pads, high-current paths) |
| `PCB/<board>/analysis/` | Generated analysis output. Only `manifest.json` is committed |
| `PCB/<board>/production/` | Fab outputs: `bom/`, `gerbers/`, `jlcpcb/`, `placement/` |
| [`PCB/libraries/`](PCB/libraries) | KiCad symbols, footprints and 3D models shared by all boards |
| [`PCB/datasheets/`](PCB/datasheets) | Manufacturer datasheets for the parts used, shared by all boards |
| [`scripts/spice/`](scripts/spice) | ngspice simulations of the power, enable and protection circuits |
| [`graphics/`](graphics) | Logos and images |

To add a board, create `PCB/<board>/` with the same subfolders as an existing one and add it to the
table above.

## Working on a board

Run these from the repository root.

```bash
# Check the circuit
stackup check PCB/<board>/stackup/board.kdl

# Export the purchasing BOM
stackup bom PCB/<board>/stackup/board.kdl --locked -o <board>-bom.csv
```

After `stackup check` passes, open `PCB/<board>/<board>.kicad_pcb` in KiCad and sync it with the Stackup
plugin.

## Contributing

All changes go through pull requests; nothing is pushed directly to `main`. History is kept linear, so
PRs land by rebase.
