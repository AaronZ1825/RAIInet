# RAIInet (CS246)

This repository contains a C++20 Modules implementation of a turn-based board game with both text and X11 graphics. Players move, battle, and use abilities on an 8x8 grid, aiming to download opponent links or let their data escape.

## Structure
- `raiinet/`: main project directory
- `raiinet/src/`: core source (Game/Board/Player/Ability/Display, etc.)
- `raiinet/tests/`: test scripts and cases
- `raiinet/Makefile`: build script (C++20 modules + X11)

## Build
From `raiinet/`:

```bash
make
```

Dependencies:
- C++20 modules-capable compiler (default: `g++`)
- X11 development libraries (for graphics mode)

## Run
From `raiinet/`:

```bash
./raiinet
```

Common flags:
- `-text`: text-only mode (disable graphics)
- `-ability1 <str>` / `-ability2 <str>`: player 1/2 ability string (length 5)
- `-link1 <str>` / `-link2 <str>`: player 1/2 link setup
- `-enableExtraFeature`: enable extra abilities (H/E/A)
- `-enableTextFlip`: flip text board for player 2 (180 degrees)

Example:
```bash
./raiinet -text -ability1 LFDSP -ability2 LFDSP
```

## In-Game Commands
- `move <linkId> <up|down|left|right>`
- `ability <idx> [params]` (idx starts at 1)
- `abilities`
- `board`
- `sequence <file>` (run a script file)
- `quit`

## Ability Codes
Default ability string: `LFDSP`
- `L` LinkBoost: move 2 tiles
- `F` Firewall: place a firewall
- `D` Download: steal opponent link
- `S` Scan: reveal opponent link
- `P` Polarize: flip link type

Extra abilities (require `-enableExtraFeature`):
- `H` Headshot
- `E` Exchange
- `A` Ambush

Ability string rules (see `src/main.cc`):
- must be exactly 5 characters
- max 2 of the same ability
- without `-enableExtraFeature`, H/E/A fall back to default

## Tests
From `raiinet/`:

```bash
./run_tests.sh
```

Extra ability tests:
```bash
./run_new_ability_tests.sh
```

Run a single test:
```bash
./raiinet < tests/test_basic_movement.txt
```

## Defaults
- default links: `V1V2V3V4D1D2D3D4`
- default abilities: `LFDSP`
- graphics enabled by default (use `-text` to disable)

## Key Entry Points
- `raiinet/src/main.cc`: CLI parsing, game init, displays
- `raiinet/src/game.cc`: turn logic, win checks, abilities
- `raiinet/src/controller.cc`: command parsing and input loop
- `raiinet/src/graphicsdisplay.cc` / `raiinet/src/textdisplay.cc`: displays
