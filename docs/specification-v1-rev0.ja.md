# CraftVia Core-S RP235xA v1 Rev0 仕様書

> [!WARNING]
> **凍結済み設計・未検証ハードウェアです。** 本書はRev0実装を記述しますが、Core-S適合の実機検証完了を示すものではありません。

## 識別と正本

| 項目 | 内容 |
| --- | --- |
| MCU | 標準RP2354A、代替RP2350A、QFN-60 |
| PCB | 25.4 mm × 25.4 mm、4層 |
| 電源 | 安定化済み3.3 V入力 |
| 凍結済みSource | `../source/CraftVia-Core-S-RP235xA-v1-Rev0.eprj2` |
| 製造正本 | `../fabrication/Gerber_PCB1_2026-11-04.zip` |
| 標準実装 | RP2354A + 内部2 MB Flash |

凍結済みSource、Gerber、BOM、Release recordをRev0の正とします。共通要件は[Core-S Interface v1](https://github.com/craftvia/craftvia-docs/blob/main/standards/core-s-interface-v1.md)を参照してください。

## ハードウェア概要

- Dual Arm Cortex-M33またはDual Hazard3 RISC-V、最大150 MHz。
- SRAM 520 KiB、OTP 8 KiB。
- RP2354AはPackage内部2 MB Flash、RP2350Aは外付けW25Q128JVSIQ 16 MB Flash。
- N1/N2/N3にSWD、N4にUSB BOOTSEL要求、N7/N8にNative USB 1.1。
- Core-S共通端子へGPIO 26本、製品固有J8へGPIO20-GPIO23の4本。
- E1-E4へ12-bit ADC 4入力。PIO、UART、SPI、I2C、PWM、HSTX対応信号を公開。

## 実装Variant

| 部品 | RP2350A | RP2354A |
| --- | --- | --- |
| U1 | RP2350A | RP2354A |
| U2 | W25Q128JVSIQ実装 | DNP |
| R7 | 0 ohm実装 | DNP |
| R8 | 10 kohm実装 | DNP |
| C17 | 100 nF実装 | DNP |

両Variantを混在させないでください。出力済みCPLには両Variant部品とTP1-TP5が含まれるため、Turnkey実装前にVariant別BOM/CPLを作成・保存します。

## 端子概要

- N1=RUN、N2=SWDIO、N3=SWCLK、N4=BOOTSEL_REQ、N7/N8=USB DM/DP。
- E1-E4=GPIO29-GPIO26 / ADC3-ADC0。
- E5-E8=GPIO19-GPIO16、S1-S8=GPIO6/7/15/14/13/12/11/10。
- W1/W2=GPIO8/9 UART1、W3/W4=GPIO5/4 I2C0、W5-W8=GPIO2/0/3/1 SPI0。
- J8=GPIO20-GPIO23。J8は製品固有端子であり、Core-S共通Interfaceではありません。

## 電源・Clock・Boot・USB

- R1=0 ohmで`+3V3_IN`から`+3V3_CORE`へ供給します。入力Regulatorや一般的な入力保護はありません。
- 内部Regulatorと3.3 uH電源段で1.1 Vを生成し、Exposed padは3 × 3 thermal via arrayを使用します。
- 12 MHz crystalを標準実装します。
- BOOTSELはRUN Low、N4 Low、RUN解除、Sample後N4 High-Zの順に操作します。通常Flash動作中にQSPI_SSをLow保持しません。
- USB DM/DPにはMCU近傍27 ohmを実装します。VBUS、Connector、CC、ESD、Path isolationはStation/Carrier側の責任です。

## 未検証項目

両MCU Variant、Regulator、12 MHz Clock、USB BOOTSEL、Application USB、SWD recovery、ADC、Connector越しHSTX、消費電流、温度、Station-S連携を初品で検証します。
