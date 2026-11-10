# CraftVia Core-S RP235xA v1 Rev0 リリースノート（参考訳・要約）

英語版 [`RELEASE_NOTES.md`](RELEASE_NOTES.md) を正本とします。

- Freeze: 2026-11-04 00:03 JST
- 状態: 初回Prototype基板製造向けに凍結、実機未検証
- 標準実装: RP2354A + 内部2 MB Flash
- 代替実装: RP2350A + W25Q128JVSIQ 16 MB Flash
- PCB: 25.40 mm角、4層、公称1.60 mm
- PCB DRC: 検出事項0件
- 原理図DRC: Fatal 0 / Error 0 / Warning 2（Supplier/component属性正規化警告）
- 製造正本: `fabrication/Gerber_PCB1_2026-11-04.zip`
- CPLは未Filterで、両Variant部品とTP1-TP5を含む

Turnkey実装へ使用する前に、選択したMCU variantに合わせてBOM/CPLをFilterし、U1とFlash関連部品U2/R7/R8/C17の実装条件を揃えてください。詳細なStack-up、USB、電源、BOOTSEL、初品検証条件は英語正本を確認してください。
