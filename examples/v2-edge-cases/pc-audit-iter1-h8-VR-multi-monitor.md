# PC Audit — Iter 1 · Case h8-VR-multi-monitor

> Persona：工程師 + VR 開發 + 4K × 3 monitor，效能優先
> 預算：NT$ 80,000
> 日期：2026-06-19

---

## 🚨 必修 BLOCKER

### BLOCKER 1：**嚴重超預算約 NT$25,000–30,000**

原菜單估算總價（2026 TW 行情中位數）：

| 項目 | 估價 |
|---|---|
| i9-14900K（盒裝） | ~$16,800 |
| ROG Strix Z790-A WIFI II | ~$11,990 |
| Vengeance RGB DDR5-7000 64GB 2×32 | ~$9,000–10,500（[未驗證 TW 報價]，美系標價反推）|
| Samsung 990 Pro 2TB | ~$8,299 |
| Arctic Liquid Freezer III 360 | ~$3,400 |
| ASUS TUF RTX 5080 16GB OC | ~$45,000–47,000（原價屋 5080 區間 $35,990–49,990，TUF OC 落中段）|
| Fractal Torrent ATX | ~$5,990 |
| Corsair RM1000e 1000W | ~$5,490 |
| **TOTAL（不含組裝/作業系統/外設）** | **~$106,000–108,000** |

超預算 **+$26,000–28,000（+33%）**，必須砍。下方 final spec 已重配在 $80k 內可落地的等效方案。

### BLOCKER 2：DDR5-7000 64GB（2×32GB dual-rank）在 LGA1700 + Z790 跑不穩的高機率

- Vengeance DDR5-**7000** 64GB（CMH64GX5M2B7000C40）= 2×32GB dual-rank kit。LGA1700 IMC（記憶體控制器）對 **2 條 dual-rank 高頻**容忍度差，**多數 Z790 板 QVL 上限 64GB(2×32) 落在 6400–6600**。
- 預期症狀：開機 memory training 30–60 秒、無法穩開 XMP、降回 5600 跑。實際就是花高速 RAM 的錢、跑慢速 RAM 的速度。
- ROG Strix Z790-A WIFI II QVL 必查 part number `CMH64GX5M2B7000C40` 才能下單；查不到就降規。
- **推薦降到 DDR5-6400 CL32 64GB(2×32) kit**（Corsair / G.Skill / Kingston FURY），LGA1700 + Z790 甜蜜點，穩、便宜、效能差距 <2%。

### BLOCKER 3：i9-14900K 退化事件未解 + microcode 0x129 修補後效能下降

- Intel 13/14 代 Raptor Lake 高電壓退化問題已知，Intel 釋出 microcode 0x129（ASUS BIOS 1663+ 已內建）抑制 eTVB 過電壓。
- 修補後多核效能小幅下降（測試約 -3 到 -7%），且**保固只到 2026 末**（Intel 已延長到出廠後 5 年，需用 retail box 盒裝走 Intel RMA）。
- VR 開發 + 多螢工作流不會單核狂飆，**用不到 14900K 那種 P+E 怪獸**；長期看 i7-14700K 或乾脆換 Arrow Lake (Core Ultra 9 285K / 265K LGA1851) 更穩、發熱低、不用擔心退化。
- **Fix path A**：14700K（仍 LGA1700，省 ~$4,000，效能差 <10%）
- **Fix path B**：換 Core Ultra 7 265K + LGA1851 板（Z890 / B860），下一代平台、發熱低、無退化風險，但 RAM 必換 DDR5-only

---

## 💰 在 NT$ 80,000 內 final spec（修正版）

**策略**：保留 RTX 5080（VR + 三 4K 不可砍）+ 換 14700K（效能差 5–8% 但省 $4k）+ DDR5-6400 64GB（穩定）+ 750W ATX 3.1 PSU（夠用且省 $1.5k）。

| 項目 | 推薦 | 價格 | 為何選 |
|---|---|---|---|
| **CPU** | Intel **Core i7-14700K**（盒裝） | ~$12,800 | 20 核（8P+12E）28 緒；VR engine（Unreal/Unity）多核跑得動；省 $4k；同 LGA1700 socket、Z790 直接用 |
| **MB** | ASUS **ROG Strix Z790-A GAMING WIFI II** | $11,990 | 維持原選；ATX、Wi-Fi 7、PCIe 5.0 ×16、DDR5、5+3 年保；BIOS 已內建 0x129 microcode |
| **RAM** | **G.Skill Trident Z5 DDR5-6400 CL32 64GB (2×32)** XMP | ~$7,500–8,200 | 降規但穩；2×32 dual-rank 在 Z790 QVL 範圍內；64GB 應付 VR scene + Unreal editor + Photoshop + Chrome |
| **SSD** | **Samsung 990 Pro 2TB**（含散熱片版本） | $8,299 | 維持；Gen4 7450/6900 MB/s；VR asset 讀寫快；5 年保 |
| **GPU** | **ASUS TUF RTX 5080 16GB OC**（或 PRIME 版） | ~$43,990–45,990 | VR + 4K×3 (3840×2160 ×3 = 24.9MP) 必須 5080 起跳；16GB VRAM 撐 VR texture streaming + 4K 多螢；DLSS 4 助攻；原生 12V-2x6 接頭 |
| **Cooler** | **Arctic Liquid Freezer III 360**（非 Pro 版） | ~$3,400 | 360 AIO、TDP 支援 350W+、壓 14700K 綽綽；VRM 風扇順便壓 Z790 供電；6 年保 |
| **PSU** | **Corsair RM850e (2025) ATX 3.1**（**降到 850W**） | ~$4,290 | 850W = 14700K (253W PL2) + 5080 (360W) + 30% headroom = **796W**，850W 剛好；原生 12V-2x6；Cybenetics Gold；省 $1.2k vs RM1000e |
| **Case** | **Fractal Torrent ATX**（黑/灰） | $5,990 | 維持；正面 2×180mm + 3×140mm 進氣，壓 5080 + 14700K + 360 AIO 熱量；顯卡長 423mm 容 TUF 5080（~330mm）寬鬆 |
| **TOTAL** | | **~$98,259–100,159** | ⚠️ 仍超預算 ~$18-20k |

### ⚠️ 還是超預算 — 真要 $80k 內的二次妥協方案

如果 **$80k 是硬天花板**，下面是第二輪砍法（標 **[砍]**）：

| 項目 | 第二輪方案 | 價格 | 妥協說明 |
|---|---|---|---|
| CPU | i7-14700K | $12,800 | — |
| MB | **[砍] MSI MAG Z790 TOMAHAWK MAX WIFI** | ~$8,990 | 降一階 MB，仍 ATX + Wi-Fi 7 + DDR5；省 $3k |
| RAM | **[砍] G.Skill Ripjaws S5 DDR5-6400 CL32 32GB(2×16)** | ~$3,800 | **VR 開發要 64GB 但被預算逼到 32GB**；之後再加 2×16 升 64GB（保留 4 槽板）|
| SSD | Samsung 990 Pro 2TB | $8,299 | — |
| GPU | TUF RTX 5080 OC | $43,990 | 不可砍（VR + 4K×3 紅線） |
| Cooler | Arctic Liquid Freezer III 360 | $3,400 | — |
| PSU | Corsair RM850e | $4,290 | — |
| Case | **[砍] Fractal Pop XL Air RGB / Lian Li Lancool 216** | ~$3,990 | 降一階機殼；風流仍足夠 |
| **TOTAL** | | **~$89,759** | 仍超 $9.7k；要回 $80k 內必須砍到 14700**F**（無內顯 -$1.5k）+ 5070 Ti 16GB（-$15k） |

### 🔴 真.$80k 預算可成型方案（須降 GPU 到 5070 Ti）

| 項目 | 推薦 | 價格 |
|---|---|---|
| CPU | Intel i7-14700K | $12,800 |
| MB | MSI MAG Z790 TOMAHAWK MAX WIFI | $8,990 |
| RAM | G.Skill DDR5-6400 64GB(2×32) CL32 | $7,800 |
| SSD | Samsung 990 Pro 2TB | $8,299 |
| GPU | **RTX 5070 Ti 16GB**（TUF/PRIME OC）| ~$28,990 |
| Cooler | Arctic Liquid Freezer III 360 | $3,400 |
| PSU | Corsair RM850e ATX 3.1 | $4,290 |
| Case | Fractal Pop XL Air RGB | $3,990 |
| **TOTAL** | | **~$78,559** ✅ 預算內 |

**Trade-off**：5070 Ti vs 5080 在 VR（Quest 3 / Index）+ 4K×3 工作流的差距：
- 純 VR（90Hz 雙眼 2064×2208）：5070 Ti 撐得住主流 VR 引擎；高端如 MSFS VR / DCS VR 會吃力
- 4K×3 productive（瀏覽、coding、Figma）：完全不是問題（產能用途）
- 4K×3 遊戲：5070 Ti 12K 解析度肯定不夠，5080 也只能開低
- **建議**：若 VR 開發是 daily driver，咬牙留 5080，砍到 32GB RAM 再分期加；若 VR 只是專案性、平日多螢 productive 為主，5070 Ti 已夠用

---

## 📊 Use-case 適配度

- **Primary use**：VR 開發（Unreal / Unity / OpenXR）+ 4K × 3 monitor 多工 productivity
- **適配亮點**：
  - 16GB VRAM 撐 VR texture streaming + Unreal editor viewport + 4K 多螢輸出（Lossless Scaling / Virtual Desktop 跑得動）
  - 20 核 28 緒 14700K：Unreal Shader Compile / Unity Build 多核加速
  - 64GB RAM（如保得住）：VR scene assets + Unreal editor + 大型 Blender scene + Chrome 30 分頁同時掛
  - Gen4 NVMe 2TB：VR asset hot reload 快、scene streaming 順
  - Fractal Torrent 大進氣：4K×3 + 5080 + 14700K 全載熱量壓得住
- **PSU math**：14700K (253W PL2) + RTX 5080 (360W) = 613W × 1.3 = **796W → 推 850W**（不是原 1000W；RM1000e 雖然好但 200W 沒用到）
- **未來升級空間**：
  - LGA1700 是 dead-end socket（下代是 LGA1851 Arrow Lake），CPU 不能升
  - RAM 可從 32→64GB 加裝（如走二次妥協）
  - GPU 可升 5090 但 PSU 850W 邊緣，要再評
- **顯示輸出**：5080 有 1×HDMI 2.1 + 3×DP 2.1，可直接吃 3 台 4K@60/120Hz（DP 2.1 UHBR20 支援 4K@240Hz HDR）

---

## ⚠️ 還沒解的 risk

1. **DDR5-7000 64GB 原菜單如硬要上**：必須在 ASUS Z790-A WIFI II 官網 QVL（memory support list）查到 `CMH64GX5M2B7000C40` part number，查不到極大機率跑不起 XMP。Sam 自己手動查：https://www.asus.com/motherboards-components/motherboards/rog-strix/rog-strix-z790-a-gaming-wifi-ii/helpdesk_qvl_memory/
2. **i9-14900K（如不換）保固期內必確認**：賣場板已內建 0x129 microcode（ASUS Z790-A BIOS 1663 之後）；買回家後第一件事 BIOS 看是否 ≥ 1663 才開機，否則先用內顯刷 BIOS。
3. **Fractal Torrent ATX 顯卡長 423mm**：TUF 5080 長 ~330mm，輕鬆容；但前進氣風扇是 180mm × 2，**不要把 360 AIO 排在前面**（會擋進氣 + 衝突），360 AIO 排頂部即可（Torrent 頂部支援 360）。
4. **4K × 3 同時 90Hz**：5080 有 4 個視訊輸出口足夠，但 DP 2.1 需用認證 cable，便宜山寨線會降到 DP 1.4 訊號降畫質。
5. **HBM 紅利期 2026 報價**：

> 🟡 **2026 SSD / RAM HBM 紅利期 baseline**：因 HBM3e + AI 訓練卡需求佔走 NAND / DRAM 產能，2026 SSD / DDR5 售價相對 2023 **+30~50%**。990 Pro 2TB 從 2023 的 ~$5,500 漲到 2026 的 ~$8,299；DDR5-6400 64GB kit 約 $7,500–8,200 是合理區間，報價低於此區間反而要懷疑水貨/拆機。

6. **VR 周邊未列**：Index / Quest 3 / BSB 之類 headset 沒列入預算，VR 開發必備 controllers / base stations 等可能再 +$15,000–30,000。
7. **Display 未列**：4K × 3 monitor 沒列預算（4K 27" IPS 每台 ~$10,000–18,000，三台 $30,000+）。如 80k 含 monitor 則本機只剩 ~$50k 預算，要全面重做。**需向 Sam 確認 monitor 是否已有**。

---

## 🛒 採購建議

- **原價屋 coolpc.com.tw**：菜單貼上自選，門市現場估價可指定 0x129 BIOS 預刷 + 上門組裝（$800–1,500）。CPU 大型零件建議盒裝、不要散裝。
- **欣亞 sinya.com.tw**：實體可現場驗機、退換貨方便；RTX 5080 大型卡建議選有保固卡的代理商貨（華碩 4 年保 = 3 年原廠 + 1 年延長）
- **autobuy.tw**：i9-14900K / 14700K 常有殺，但要確認**盒裝 retail box + Intel 三年保**，不要散裝
- **套裝機對比**：PCHome 24h 同 spec 5080 套裝約 $115,000–125,000，自組省 $15k+ 但要會排線。RM1000e 或 RM850e 走 cybenetics 認證確認原生 12V-2x6（不要轉接頭）
- **顯卡保固**：華碩 TUF 5080 = 3 年原廠保（線上註冊 +1 年），燒卡走代理商不走原廠（避免水貨陷阱）

---

## Summary（給 Sam 一句話）

原菜單三大問題：**預算超 33% / RAM 跑不起 7000 速 / 14900K 退化風險 + 過量**。建議**降 CPU 到 14700K、RAM 改 DDR5-6400、PSU 改 850W**，保留 RTX 5080 + Z790 + Torrent + 990 Pro 2TB，估到 ~$98k（仍超 18k）；要硬卡 $80k 內需把 GPU 降到 5070 Ti，VR 工作流會有感。**先確認 monitor 是否已有 → 才能決定最終 GPU 留 5080 還是 5070 Ti**。
