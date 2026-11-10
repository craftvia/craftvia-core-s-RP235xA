# CraftVia Core-S RP235xA v1 Rev0 Specification

> [!WARNING]
> **Frozen design, unverified hardware.** This document describes the Rev0 implementation; it does not claim verified Core-S conformance.

## Identity and authority

| Item | Value |
| --- | --- |
| MCU | RP2354A default or RP2350A alternate, QFN-60 |
| PCB | 25.4 mm × 25.4 mm, 4 layers |
| Supply | Regulated 3.3 V input |
| Frozen source | `../source/CraftVia-Core-S-RP235xA-v1-Rev0.eprj2` |
| Fabrication master | `../fabrication/Gerber_PCB1_2026-11-04.zip` |
| Default population | RP2354A + internal 2 MB Flash |

The frozen source, fabrication master, authoritative BOM, and release record control Rev0. Common requirements are defined by the [Core-S Interface v1](https://github.com/craftvia/craftvia-docs/blob/main/standards/core-s-interface-v1.md).

## Hardware summary

- Dual Arm Cortex-M33 or dual Hazard3 RISC-V cores up to 150 MHz.
- 520 KiB SRAM and 8 KiB OTP.
- RP2354A uses package-internal 2 MB Flash. RP2350A uses external W25Q128JVSIQ 16 MB Flash.
- SWD debug on N1/N2/N3; USB BOOTSEL request on N4.
- Native USB 1.1 on N7/N8.
- 26 GPIO signals on the common Core-S contacts plus GPIO20-GPIO23 on product-specific J8.
- Four 12-bit ADC inputs on E1-E4; PIO, UART, SPI, I2C, PWM, and HSTX-capable signals are exposed.

## Assembly variants

| Part | RP2350A variant | RP2354A variant |
| --- | --- | --- |
| U1 | RP2350A | RP2354A |
| U2 | W25Q128JVSIQ fitted | DNP |
| R7 | 0 ohm fitted | DNP |
| R8 | 10 kohm fitted | DNP |
| C17 | 100 nF fitted | DNP |

Do not mix the two populations. The exported CPL is unfiltered and includes both variant choices plus TP1-TP5; create and archive variant-specific manufacturing files before turnkey assembly.

## Core-S contact mapping

| Contact | RP235xA signal | Representative role |
| --- | --- | --- |
| N1 | RUN | Active-low global reset |
| N2 | SWDIO | SWD data |
| N3 | SWCLK | SWD clock |
| N4 | QSPI_SS through 1 kohm | BOOTSEL request; normally high impedance |
| N5-N6 | GPIO24-GPIO25 | Product-specific GPIO |
| N7-N8 | USB DM/DP | Native USB 1.1 |
| E1-E4 | GPIO29-GPIO26 | ADC3-ADC0 |
| E5-E8 | GPIO19-GPIO16 | GPIO / HSTX-capable group |
| S1-S8 | GPIO6, 7, 15, 14, 13, 12, 11, 10 | PWM/timer/GPIO group |
| W1-W2 | GPIO8-GPIO9 | UART1 pair |
| W3-W4 | GPIO5-GPIO4 | I2C0 pair |
| W5-W8 | GPIO2, 0, 3, 1 | SPI0 group |
| J8-1..4 | GPIO20-GPIO23 | Product-specific auxiliary header |

`K-SW` is the 3.3 V input. `K-NW` and `K-NE` are GND. J8 is not part of the common Core-S interface and must not be required by a generic Station or Carrier.

## Power, clock, boot, and USB

- R1 is 0 ohm by default between `+3V3_IN` and `+3V3_CORE`; no input regulator or general-purpose input protection is provided.
- The internal regulator and 3.3 uH power stage generate the 1.1 V core rail; the exposed pad uses a 3 × 3 thermal-via array.
- A 12 MHz crystal is fitted.
- For BOOTSEL, assert RUN low, drive N4 low, release RUN, then return N4 to high impedance after sampling. Do not hold QSPI_SS low during normal flash operation.
- USB DM/DP use 27-ohm MCU-side series resistors. VBUS, connector, CC, ESD, and path isolation belong on the Station/Carrier.

## Manufacturing constraints

- Four-layer JLC04161H-7628 baseline, nominal 1.60 mm.
- USB target is 90 ohm differential, ±10% manufacturing tolerance; confirm against the selected production stack-up.
- Review QFN-60 paste segmentation, exposed-pad voiding, and via wicking for the selected assembly process.
- Preserve frozen assets and create a new PCB revision for electrical, footprint, routing, silkscreen, or population changes.

## Known unverified areas

Both MCU variants, the regulator, 12 MHz clock, USB BOOTSEL, application USB, SWD recovery, ADC performance, HSTX over the connector, power consumption, thermal behavior, and Station-S interoperability require first-article validation.
