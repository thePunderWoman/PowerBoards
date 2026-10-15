# Distribution Board

Six identical 2-pole terminals share a V+ plane (`VPWR`, top copper) and a ground plane (`GND`,
bottom copper). Any terminal can be the input; the other five are outputs. There are no active or
passive components.

The electrical design is in [Stackup KDL](stackup/board.kdl). The KiCad PCB
(`distribution.kicad_pcb`) is linked to it through `distribution.stackup_sch`; sync it with the Stackup
KiCad plugin. Run `stackup check PCB/distribution/stackup/board.kdl` from the repository root
before syncing.

## Hardware overview

| Ref | Function | Part |
|---|---|---|
| J1-J6 | Power terminal, input or output | WAGO 2601-1102 |

Every terminal has pin 1 (square pad, `+` on the silkscreen) on `VPWR` and pin 2 (`-`) on `GND`.

## Terminal: WAGO 2601-1102

Lever-actuated Push-in CAGE CLAMP, 2-pole, 3.5 mm pitch, wire entry parallel to the PCB.
From the [WAGO data sheet](../datasheets/WAGO_2601-1102.pdf) (version 25.01.2023):

| Spec | Value | Source |
|---|---|---|
| Wire, solid | 0.14-1.5 mm² / 26-16 AWG | p. 2 |
| Wire, fine-stranded | 0.2-1.5 mm² / 24-16 AWG | p. 2 |
| Strip length | 8-9 mm | p. 2 |
| Rated current | 17.5 A (IEC/EN 60664-1); 10 A (UL 1059 / CSA, Use Groups B and D) | p. 2 |
| Wire entry angle to PCB | 0° | p. 2 |
| Solder pins | 2 per pole, rows 5 mm apart, 1.2 (+0.1) mm hole | p. 1, p. 3 |

The 2601-3102 is the vertical, top-entry version of the same block; it is not a substitute.

## Design decisions

- **Current limit is the input terminal.** Whichever terminal is used as the input carries the sum of
  all the outputs. The design limit is 10 A total, the terminal's UL rating, with 16 AWG wire.
- **No input or output labels.** Any terminal can be the input, so the silkscreen marks only `+` and `-`.
- **3 x 2 grid, rows back to back.** J1-J3 form the top row, rotated 180° so their wires enter from
  the top edge. J4-J6 form the bottom row, with wires entering from the
  bottom edge. Columns are on a 10 mm pitch (8.5 mm body plus room to work the levers), and an 8 mm gap
  between the rows holds the polarity labels. Seen from its own edge, every terminal has `+` on the left.
- **Wire entry faces are flush with the top and bottom board edges**, so the wires leave the board and
  the levers (16.58 mm deep including the lever, versus a 14.5 mm body) overhang the edge. This puts the
  footprints' silkscreen outlines across the edge: the 12 `silk_edge_clearance` DRC warnings are
  expected and the fab clips that silkscreen.
- **Four M3 mounting holes, one per corner.** KiCad `MountingHole_3.2mm_M3` (3.2 mm unplated), placed
  on side extensions beside the terminals, with each hole centre 4.5 mm from the nearest terminal body.
  They are board-only footprints in the layout, not Stackup parts: Stackup sync leaves board-only
  footprints alone, and they stay out of the BOM and placement files.
- **Copper keep-out around each hole.** An 8 mm diameter rule area on both copper layers keeps the V+ and
  GND planes away from the screw head and standoff. Otherwise a metal screw would sit on V+ copper on
  top and GND on the bottom with only solder mask between them.
- **Planes, not traces.** At 10 A, IPC-2221 needs about 7.2 mm of 1 oz outer copper for a 10 °C rise.
  Each plane spans the whole 45.5 x 37 mm board. Pads join their plane through thermal reliefs with
  1.0 mm spokes; with two solder pins per pole, that is 8 spokes (8 mm of copper) per pole.

## Bench checklist

- Before connecting a load, check continuity between all six `+` pins and between all six `-` pins, and
  confirm there is no short between V+ and GND.
- Run the full intended load through the input and one output, and check the input terminal and the
  board near it for heating.
