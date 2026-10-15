# Regulator Board

Purpose, input and output ranges, and current budget: to be written.

The electrical design is in [Stackup KDL](stackup/board.kdl). The KiCad PCB
(`regulator.kicad_pcb`) is linked to it through `regulator.stackup_sch`; sync it with the Stackup
KiCad plugin. Run `stackup check PCB/regulator/stackup/board.kdl` from the repository root
before syncing.

## Hardware overview

| Function | Part | Notes | Layout diagram |
|---|---|---|---|
