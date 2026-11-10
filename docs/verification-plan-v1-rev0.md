# CraftVia Core-S RP235xA v1 Rev0 Verification Plan

> Status: Draft plan for unverified Rev0 hardware. A listed test is not a test result.

Record board ID, MCU/Flash variant, assembly date, BOM deviations, instruments, firmware commit, test operator, and evidence. Mark each item Pass, Fail, Blocked, or Not run.

| ID | Test | Pass criteria |
| --- | --- | --- |
| `CSRP-R0-001` | Release identity and SHA-256 | Board, source, BOM, and Gerber identify v1 Rev0; frozen assets match `SHA256SUMS.txt`. |
| `CSRP-R0-002` | Visual and mechanical inspection | QFN orientation, exposed-pad assembly, variants, outline, headers, and keying have no visible defect. |
| `CSRP-R0-003` | Unpowered rail checks | No short on 3.3 V, 1.1 V, or GND; fitted population matches the recorded variant. |
| `CSRP-R0-004` | Current-limited first power | Rails start correctly with no current-limit event or abnormal heat. |
| `CSRP-R0-005` | Regulator and clock | 1.1 V rail, ripple, load behavior, 12 MHz startup, current, and temperature are recorded. |
| `CSRP-R0-006` | SWD/RUN recovery | Device attach, halt, program, verify, RUN reset, and connect-under-reset succeed repeatedly. |
| `CSRP-R0-007` | Flash variants | RP2354A internal 2 MB and RP2350A external 16 MB configurations each erase, program, and verify. |
| `CSRP-R0-008` | USB BOOTSEL | N4/RUN sequence reliably enters BOOTSEL and returns N4 to high impedance. |
| `CSRP-R0-009` | Application USB | Enumeration, transfer, reset, reconnect, and SWD recovery pass through the intended Station-S path. |
| `CSRP-R0-010` | Core-S and J8 contacts | All 26 common GPIO and four J8 GPIO map correctly; adjacent contacts are isolated. |
| `CSRP-R0-011` | ADC and peripherals | ADC0-3 plus representative UART, SPI, I2C, PWM, and PIO functions pass. |
| `CSRP-R0-012` | 150 MHz and thermal run | Sustained operation, input current, regulator behavior, and surface temperature are acceptable and recorded. |

Stop immediately for unexpected heating, unstable supply, current limiting, reversed orientation, or signal-driver contention. Do not program irreversible OTP security settings during initial bring-up. Rev0 may be marked verified only after mandatory tests pass on an identified production-representative assembly and the evidence is published.
