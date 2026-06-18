# Examples

20 real audit reports produced by `pc-build-audit-tw` skill across two test phases.

## v1 — foundation (8 cases)

| File | Persona | Budget |
|---|---|---|
| [case1-gaming-budget-25k](v1-foundation/pc-audit-case1-gaming-budget-25k.md) | 1080p gamer | NT$25,000 |
| [case2-ai-llm-dev-60k](v1-foundation/pc-audit-case2-ai-llm-dev-60k.md) | LLM/AI dev workstation | NT$60,000 |
| [case3-creator-50k](v1-foundation/pc-audit-case3-creator-50k.md) | Premiere/DaVinci editor | NT$50,000 |
| [case4-fatal-compat-bug](v1-foundation/pc-audit-case4-fatal-compat-bug.md) | **🚨 AMD CPU + Intel MB trap** | NT$30,000 |
| [case5-overpriced](v1-foundation/pc-audit-case5-overpriced.md) | **🚨 LINE 群 賣家虛標 1.5-2x** | NT$45,000 |
| [case6-psu-undersized](v1-foundation/pc-audit-case6-psu-undersized.md) | **🚨 14700KF + 4080 Super on 550W** | NT$70,000 |
| [case7-data-eng-multicore-40k](v1-foundation/pc-audit-case7-data-eng-multicore-40k.md) | Data engineering | NT$40,000 |
| [case8-family-modest-32k](v1-foundation/pc-audit-case8-family-modest-32k.md) | Family / office | NT$32,000 |

## v2 — edge cases (12 cases)

| File | Edge case probed |
|---|---|
| [h1-itx-compact](v2-edge-cases/pc-audit-iter1-h1-itx-compact.md) | ITX 25cm GPU clearance + cooler height |
| [h2-am4-still-good](v2-edge-cases/pc-audit-iter1-h2-am4-still-good.md) | AM4 leftover platform — accept, don't force upgrade |
| [h3-aio-water-cool](v2-edge-cases/pc-audit-iter1-h3-aio-water-cool.md) | 420mm AIO case top/side mount |
| [h4-vintage-1151-leftover](v2-edge-cases/pc-audit-iter1-h4-vintage-1151-leftover.md) | Vintage LGA1151 9700K + used 1660 Super |
| [h5-used-cards-llm-budget](v2-edge-cases/pc-audit-iter1-h5-used-cards-llm-budget.md) | **NVIDIA Tesla M40 24GB** 洋垃圾 LLM build |
| [h6-undersized-pcie-lane](v2-edge-cases/pc-audit-iter1-h6-undersized-pcie-lane.md) | H610 + Gen5 SSD + multi M.2 lane sharing |
| [h7-content-pro-mac-replacement](v2-edge-cases/pc-audit-iter1-h7-content-pro-mac-replacement.md) | **Threadripper 7960X** workstation |
| [h8-VR-multi-monitor](v2-edge-cases/pc-audit-iter1-h8-VR-multi-monitor.md) | 14900K + 5080 + 4K×3 monitor + VR |
| [h9-mining-gpu-trap](v2-edge-cases/pc-audit-iter1-h9-mining-gpu-trap.md) | **2nd-hand mining RTX 3070** risk |
| [h10-iGPU-no-dgpu](v2-edge-cases/pc-audit-iter1-h10-iGPU-no-dgpu.md) | 8600G iGPU-only, no dGPU |
| [h11-bios-trap](v2-edge-cases/pc-audit-iter1-h11-bios-trap.md) | **7800X3D + 老 B650 BIOS** (won't boot) |
| [h12-curveball-china-grey-market](v2-edge-cases/pc-audit-iter1-h12-curveball-china-grey-market.md) | **水貨 5800X3D + 中國貨 GPU** |

## How to read each report

Each follows the SKILL.md output template:

1. **🚨 BLOCKER** — if any compatibility/safety showstopper
2. **💰 Final spec table** — item / pick / price / reasoning column
3. **📊 Use-case fit** — primary use + adaptation points + upgrade headroom
4. **⚠️ Remaining risks** — unresolved compat/cost concerns
5. **🛒 採購建議** — retailer routing (原價屋 vs 欣亞 vs autobuy vs 套裝機)

Pricing is 2026 TW market (HBM-elevated baseline). Component median computed across sinya / coolpc / autobuy / 賣家報價. Knowledge claims cite 巴哈 PCDIY / PTT PC_Shopping where applicable.
