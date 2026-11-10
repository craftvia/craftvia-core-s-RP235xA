# CraftVia Core-S RP235xA v1 Rev0 検証計画

> 状態: 未検証Rev0向けのDraft計画です。項目の記載は試験合格を意味しません。

Board ID、MCU/Flash Variant、実装日、BOM差分、測定器、Firmware commit、実施者、Evidenceを記録し、各項目をPass / Fail / Blocked / Not runで判定します。

| ID | 試験 | 合格基準 |
| --- | --- | --- |
| `CSRP-R0-001` | Release識別とSHA-256 | Board、Source、BOM、Gerberがv1 Rev0を示し、凍結資産がmanifestと一致する。 |
| `CSRP-R0-002` | 外観・機械確認 | QFN向き、Exposed pad実装、Variant、外形、Header、Keyに異常がない。 |
| `CSRP-R0-003` | 未通電電源確認 | 3.3 V、1.1 V、GNDに短絡がなく、実装が記録Variantと一致する。 |
| `CSRP-R0-004` | 電流制限付き初回通電 | 各Railが正常起動し、電流制限や異常発熱がない。 |
| `CSRP-R0-005` | Regulator/Clock | 1.1 V、Ripple、Load応答、12 MHz起動、電流、温度を記録する。 |
| `CSRP-R0-006` | SWD/RUN recovery | Attach、halt、program、verify、RUN reset、connect-under-resetが反復成功する。 |
| `CSRP-R0-007` | Flash Variant | RP2354A内部2 MBとRP2350A外付け16 MBの各構成でerase/program/verifyが成功する。 |
| `CSRP-R0-008` | USB BOOTSEL | N4/RUN sequenceで安定してBOOTSELへ入り、N4をHigh-Zへ戻せる。 |
| `CSRP-R0-009` | Application USB | Station-S経路でenumeration、transfer、reset、reconnect、SWD recoveryが成功する。 |
| `CSRP-R0-010` | Core-S/J8接点 | 共通GPIO 26本とJ8 GPIO 4本のMappingと隣接絶縁が正しい。 |
| `CSRP-R0-011` | ADC/Peripheral | ADC0-3と代表UART/SPI/I2C/PWM/PIOが動作する。 |
| `CSRP-R0-012` | 150 MHz/温度 | 連続動作、入力電流、Regulator、表面温度を記録し、異常がない。 |

異常発熱、電源不安定、電流制限、逆挿し、Driver競合があれば直ちに停止します。初期Bring-upでは不可逆OTP Security設定を書き込みません。Mandatory testが製造代表個体で合格し、Evidenceを公開するまでVerifiedと表示しません。
