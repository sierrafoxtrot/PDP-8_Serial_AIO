# PDP-8 Serial All-in-One

A W070 compatible serial interface for the original DEC PDP-8, providing both teletype current loop and RS-232 compatible interfaces.

## Background

The original PDP-8 was commonly used with an ASR-33 Teletype connected through a DEC W070 interface. The ASR-33 provided a 110 baud printing terminal together with paper tape punch and reader facilities.

The Australian Computer Museum Society PDP-8 is missing its W070 interface. This project started as a []RetroChallenge 2026/10](https://www.retrochallenge.org/) project to build a practical replacement, while adding an RS-232 interface so the machine can also be used with terminals such as a DECWriter or VT220, or with a modern computer through a USB to RS-232 adaptor.

Project background and RetroChallenge progress:

[RetroChallenge 2026/10 project thread](https://forum.acms.org.au/t/rc2026-10-pdp-8-serial-interface/1152)

## Design goals

* Provide a functional replacement for the serial and current loop functions of the DEC W070.
* Retain support for a period current loop Teletype, including reader enable.
* Provide an RS-232 DCE interface on a DE-9 connector.
* Allow the PDP-8 transmit, receive and reader enable paths to be independently selected between current loop and RS-232.
* Preserve the PDP-8 negative logic interface levels.
* Provide visible TX, RX and Reader Enable status indicators.
* Use straightforward, readily available components and remain practical to diagnose and repair.

There is deliberately no onboard USB interface. A conventional RS-232 interface keeps the board useful with both period equipment and modern USB to RS-232 adaptors. I've compromised on going with the the more 1980's era DE-9 connector to accomodate the screw terminals for the current loop.

## Interfaces

### W070 compatible current loop

The six position terminal block provides the Teletype connections:

| Terminal | Connection |
| ---: | --- |
| 1 | TTI return |
| 2 | TTO |
| 3 | TTI, -15 V |
| 4 | Reader, +10 V |
| 5 | Reader enable |
| 6 | TTO return |

The connections are arranged as three pairs:

* **TTI / keyboard:** 3 (-15 V), 1 (return)
* **TTO / printer:** 2 (TTO), 6 (return)
* **Reader enable:** 4 (+10 V), 5 (enable)

### RS-232

The DE-9 connector is wired as **DCE** and is intended for use with a straight through cable to a DTE terminal or computer. If you are using a USB-RS232 adaptor, it should plug in directly.

| Pin | Function |
| ---: | --- |
| 2 | TX |
| 3 | RX |
| 5 | GND |
| 8 | CTS / Reader Enable |

### Interface selection

Three selector links choose the interface used for the relevant PDP-8 signals:

| Link position | Interface |
| --- | --- |
| 1 to 2 | RS-232 |
| 2 to 3 | Current loop |

### Indicators

* **TX** indicates transmitted SPACE states.
* **RX** indicates received SPACE states.
* **RE** indicates Reader Enable.

## Power

The board uses the supplies already available in the PDP-8:

* +10 V
* -15 V
* GND

A local 78L05 regulator provides the +5 V supply required by the interface logic.

## Design files

The project is designed in [KiCad](https://www.kicad.org/). The repository contains the schematic, PCB layout and associated project files required to reproduce or modify the board.

Before manufacturing a board, check the current revision notes and run KiCad ERC and DRC. As with any interface connected to vintage hardware, verify supply voltages and connector wiring before installation.

## Licence

This hardware design is licensed under the **CERN Open Hardware Licence Version 2, Weakly Reciprocal**.

SPDX-License-Identifier: `CERN-OHL-W-2.0`

See [LICENSE](LICENSE) for the full licence text.
