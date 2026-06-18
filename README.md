# pc-build-audit-tw

> A Claude Code Skill that audits Taiwan PC build menus (原價屋 / 欣亞 / autobuy / PCHome / momo) for compatibility, 2026 pricing realism, and use-case fit. Output in 繁體中文.

[![License: Apache 2.0](https://img.shields.io/badge/License-Apache_2.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)
[![Skill Format](https://img.shields.io/badge/Format-Claude_Code_Skill-orange.svg)](https://docs.claude.com/en/docs/claude-code/skills)

## What it does

Drop a Taiwan PC parts list (image screenshot or text) into a Claude Code session with this skill loaded, and it will:

1. **Parse** every component (CPU / MB / RAM / SSD / GPU / PSU / Case / Cooler)
2. **Catch BLOCKER bugs**:
   - CPU socket vs MB chipset mismatch (e.g. AM5 CPU + LGA1700 board)
   - DDR4 RAM in DDR5-only platform
   - PSU undersized for CPU+GPU TDP
   - Case form factor incompatibility
   - AM5 X3D on older B650 board → BIOS update gotcha
   - High-speed DDR5 not on MB's QVL
3. **Verify pricing** against 2026 Taiwan market (sinya / coolpc / autobuy median + 倍率)
4. **Match spec to use case** (gaming / AI-LLM dev / content creator / data eng / family / streamer)
5. **Output 繁中** final spec table + reasoning column + budget buffer + risks

## Why it exists

PTT PC_Shopping and 巴哈 PCDIY see CPU-MB compatibility errors at least 3 times per month in 菜單 posts. Online configurators don't catch them all (especially mixed AMD-Intel mistakes when ordering parts à la carte from different retailers). This skill encodes the audit checklist a senior 組機師 would run, so the answer comes back fast and consistent.

Also: 2026 SSD/RAM pricing is +30-50% over 2023 due to HBM/AI demand. Old reference prices on the web are stale; this skill enforces a 2026 baseline callout in every audit.

## Installation (Claude Code)

```bash
# Drop SKILL.md into your skills directory
mkdir -p ~/.claude/skills/pc-build-audit-tw
curl -L https://raw.githubusercontent.com/samwu4166/pc-build-audit-tw/main/SKILL.md \
  -o ~/.claude/skills/pc-build-audit-tw/SKILL.md
```

Restart your Claude Code session. The skill appears as `pc-build-audit-tw` in `Skill` tool listings and triggers automatically when you paste a parts list.

Project-level install: drop into `<project>/.claude/skills/pc-build-audit-tw/SKILL.md`.

## Usage

In any Claude Code session with the skill installed:

```
[paste a screenshot of an 原價屋 menu]

預算 40K，主要拿來玩 1440p 遊戲 + 偶爾跑 LLM
```

The agent will:

1. Parse the parts list from the image
2. Run the 5-step audit
3. Reply with 繁中 BLOCKER section (if any) + final spec table + budget breakdown + risks

See [`examples/`](./examples/) for 20 real audit outputs across diverse scenarios.

## Examples

20 dogfooded audit reports covering:

**v1 foundation (8 cases)** — gaming 25k, AI/LLM dev 60k, creator 50k, fatal compat bug (AMD CPU + Intel MB), overpriced LINE 群 seller, PSU undersized, data eng 40k, family 32k.

**v2 edge cases (12 cases)** — ITX 25cm GPU clearance, AM4 leftover upgrade, 420mm AIO water cooling, vintage LGA1151 budget rebuild, NVIDIA Tesla M40 24GB 洋垃圾 LLM, H610 + Gen5 SSD lane sharing, Threadripper workstation, VR multi-monitor, ex-mining RTX 3070 risk, iGPU-only office build, 7800X3D + 老 BIOS B650 trap, 水貨 X3D + 中國貨 grey market.

Each example shows the parsed parts list, 5-step audit reasoning, final spec table, and risk notes.

## Skill structure

```
SKILL.md           — the skill itself (253 lines)
├── 1. 觸發場景       — when this skill should fire
├── 2. 5-step algorithm
│   ├── Step 1: Parse parts list (vision → JSON)
│   ├── Step 2: Compatibility (socket / RAM / PSU / case / BIOS / QVL)
│   ├── Step 3: 2026 TW price verification (per-component sinya/coolpc/autobuy median 倍率)
│   ├── Step 4: Use-case fit
│   └── Step 5: Final spec table
├── 3. Knowledge sources       — 巴哈 PCDIY / PTT / 原價屋 / 欣亞 / autobuy / Reddit
├── 4. Hard rules (8)          — non-negotiables
├── 5. Common edge cases       — chipset naming, D4/D5 suffix, mATX/ITX 機殼, EXPO/XMP, etc.
├── 6. Output template         — 繁中 markdown
└── 7. 執行 checklist          — 14-item self-check before responding
```

## Hard rules enforced

1. CPU-MB incompatibility = **BLOCKER first, before anything else**
2. Must verify 2026 real prices (SSD/RAM 比 2023 +30-50% baseline)
3. Use case unclear → ask before recommending
4. Every recommendation includes reasoning, not just spec
5. 5-10% budget buffer for assembly fee / thermal paste / Wi-Fi antenna
6. Never fabricate part specs — Brave search to verify, mark "待查" if unknown
7. PSU sizing: `CPU TDP + GPU TDP + 30% headroom` (math line printed in every report)
8. RTX 40 series and newer → ATX 3.0/3.1 PSU native 12V-2x6, no adapters

## Knowledge sources

| For | Source |
|---|---|
| 行話 / 縮寫 | 巴哈姆特 PCDIY 看版 + PTT PC_Shopping |
| 即時行情 | 原價屋 coolpc.com.tw, 欣亞 sinya.com.tw, autobuy.tw |
| 套裝機 benchmark | PCHome 24h, momo |
| 國際對照 | r/buildapc, Tom's Hardware, TechPowerUp |
| 二手 | PTT PC_Shopping 買賣, 蝦皮, 巴哈 PCDIY 交易區 (自負風險) |

## Development & validation

This skill was built with a multi-agent dogfood loop:

- **v1**: 8 diverse cases (gaming / dev / creator / family / data eng) + 3 catastrophic-fail trap cases (compat bug, overpriced seller, PSU undersized). All 8 passed senior reviewer scoring on first iteration.
- **v2 polish**: Applied 7 reviewer improvements (specific 巴哈/PTT citation URLs, per-component median 倍率 table, 2026 HBM baseline callout, PSU math line, BIOS update warning, QVL check, iGPU sweet spot).
- **v2 robustness**: 12 harder edge cases (ITX clearance, AM4 legacy, AIO, Threadripper, used cards, iGPU-only, BIOS trap, 水貨/grey market). All 12 passed senior reviewer on first iteration.

Reviewer rubric per case:
- Compatibility: ≥10/10 (mandatory)
- Edge case handling: ≥8/10
- Pricing accuracy: ≥8/10
- Use-case fit: ≥8/10
- Output quality: ≥7/10
- Knowledge source attribution: ≥6/10
- Zero blockers

All 20 cases shipped to [`examples/`](./examples/).

## Contributing

Bug reports and edge cases welcome. Especially valuable:

- New trap scenarios not in the 20 examples
- 2026 Q3+ pricing recalibrations as HBM market shifts
- New AMD Zen 5 / Intel Arrow Lake refresh chipset launches
- Taiwan-specific retailer quirks (e.g. 套裝機 SKU hidden specs)

Open an issue or PR. 繁中 or English both fine.

## License

Apache License 2.0 — see [LICENSE](./LICENSE).

## Author

Built by Cheng-Ju Wu (Sam). Contact: cjwu.aieng@gmail.com

Part of an ongoing exploration of Claude Code Skills as deterministic domain expertise. If you build on top of this, drop a star or reach out — happy to chat about extending the pattern (e.g. servers / homelab / 工作站 audits).
