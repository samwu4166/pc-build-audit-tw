# 🔍 PC Build Audit — Case 5「明顯虛標」菜單

> Persona: 35 歲 IT 主管 / 預算 NT$ 45,000 / 2026-06-19 audit
> 平台: Intel LGA1700 (i5-14400F + B760M)

---

## 🚨 必修 BLOCKER — 嚴重虛標（不是相容性，是被當盤子）

這份菜單**沒有相容性 BUG**（CPU/MB/RAM gen 都對得上），但有兩個 component 價格**明顯虛標 ~3x**，整單必須先砍價再談配置。

### 1. RAM「ADATA D50 RGB DDR4-3600 32GB」報 NT$ 9,999 — 🚨 嚴重虛標

- **2026 真實行情** (順發 / 比價BigGo / PChome 24h)：**NT$ 2,800 – 3,500**（DDR4 已停產降價中，3 通路中位數 ≈ NT$ 3,100）
- 報價 / 中位數 = **9,999 / 3,100 ≈ 3.2×**，遠超 1.5× 嚴重虛標線
- **多收 ≈ NT$ 6,900**

### 2. SSD「ADATA Legend 850 PRO 1TB Gen4」報 NT$ 7,500 — 🚨 嚴重虛標

- 注意：菜單寫 "850 PRO" 但 ADATA 1TB Gen4 主力 SKU 是 **LEGEND 850**（非 PRO）。如果是 850 PRO 系列要確認賣家給的料號（**待查 / 確認賣家是否混 SKU**）
- LEGEND 850 1TB **2026 真實行情**：autobuy NT$ 1,888 / 官方 NT$ 2,799 / 欣亞分期 ≈ 期 245；中位數 ≈ NT$ 2,200
- 報價 / 中位數 = **7,500 / 2,200 ≈ 3.4×**
- **多收 ≈ NT$ 5,300**

### Fix path

- **Path A（保留原配置砍價）**：要求賣家把 RAM 改報 NT$ 3,100、SSD 改報 NT$ 2,200（或換 WD SN770 1TB ≈ NT$ 2,400），預算可省 ~NT$ 12,000
- **Path B（換通路）**：原價屋 / 欣亞 / autobuy 直接重組，全單透明價

---

## 💰 預算 NT$ 45,000 內 — 我的 final spec（Path B 重組版）

| 項目 | 推薦 | 價格 (NT$) | 為何選 |
|---|---|---:|---|
| CPU | Intel Core **i5-14400F**（盒裝） | 5,800 | 10C/16T、TDP 65W、IT 主管文書 + 偶爾 dev/VM 夠用；保留菜單原本選擇 |
| MB | **MSI PRO B760M-A WIFI DDR4** | 4,990 | M-ATX、DDR4 省 RAM 預算、12+1+1 相、2.5G + Wi-Fi 6E、註冊 4 年保（菜單原版 B760M-A 換 WIFI 版多 Wi-Fi 不用買網卡） |
| RAM | **Kingston FURY Beast DDR4-3600 32GB (16×2) CL18** | 2,990 | DDR4 平台甜蜜點 3600 CL18 XMP、雙通道、終身保；放棄 RGB 省 NT$ 100，IT 主管不靠燈條 |
| SSD | **WD Black SN770 1TB Gen4**（或 Crucial P3 Plus 1TB） | 2,490 | Gen4 5150 MB/s、5 年保、DRAM-less 但 IT 文書夠用；要 DRAM 升 SN850X +NT$ 900 |
| Cooler | **ID-Cooling FROZN A400 BLACK** | 990 | TDP 180W >> i5-14400F 的 65W，4 熱管壓得很輕鬆；保留菜單原選 |
| GPU | **Galax RTX 4060 Ti 8GB**（保留菜單原選） | 13,500 | ⚠️ 見「Use-case 適配度」段，IT 主管用沒問題；若有 AI dev 副業則應升 16GB 版（見 risk 段） |
| Case | **Cooler Master Q300L V2** | 1,690 | M-ATX、磁吸防塵、GPU 360mm 容得下 4060 Ti、保留菜單原選但升 V2 版 |
| PSU | **MSI MAG A650BN 650W 銅牌**（取代 "Galaxy 650W"） | 1,890 | 65W + 165W (4060 Ti) + 30% buffer = 299W << 650W，瓦數足；MSI/全漢/振華比 Galaxy 牌信賴度高，5 年保 |
| **TOTAL** | | **34,340** | 剩 **NT$ 10,660 buffer** |

### Buffer 用途建議（NT$ 10,660）

- 上門組裝費 + 跑 stress test（原價屋）≈ NT$ 1,000
- 散熱膏 MX-6 / 機殼風扇 ×2 ≈ NT$ 800
- **GPU 升級到 RTX 5060 Ti 16GB**（+NT$ 5,900-6,500，原價屋有微星 CYCLONE OC 雪螳螂方案）— **強烈建議**，後文 risk 段詳述
- 剩 NT$ 2,000-3,000 留 Windows 11 Home OEM 或 144Hz 螢幕補差

---

## 📊 Use-case 適配度

- **Primary use**: IT 主管（推測：文書 + RDP/VPN + 多視窗 + 偶爾 docker / VM / Wireshark / Power BI；可能有遊戲副需求）
- **適配亮點**:
  1. i5-14400F 10C/16T 開 30+ Chrome tabs + Teams + 2-3 VM 沒壓力
  2. DDR4 32GB 多工 buffer 充足，IT 工作 RAM 比 SSD 速度重要
  3. M-ATX 機殼桌面友善，4060 Ti 應付 1080p / 1440p 遊戲 + 多螢幕輸出
- **未來升級空間**:
  - RAM 升 64GB（同模組再買一對）
  - 第二顆 NVMe（B760M-A 有 2 個 M.2 slot）
  - GPU 升 RTX 5070（PSU 650W 還 hold 得住）

---

## ⚠️ 還沒解的 risk

1. **GPU 8GB VRAM 是 2026 下限線**：若 IT 主管有 AI side project（跑 LLM / Stable Diffusion）8GB 完全不夠。**強烈建議用 buffer 升 RTX 5060 Ti 16GB**（+NT$ 5,900），16GB VRAM 可跑 Llama 3.1 8B Q4 / SDXL；原價屋微星 CYCLONE OC 雪螳螂方案有現貨。確認 Sam 客戶有沒有這需求再 lock。
2. **"Galaxy 650W bronze" 牌子待查**：菜單寫的 Galaxy 是不是指 GALAX（影馳）？影馳 PSU 在台灣保固通路不如全漢 / 振華 / 海韻 / MSI，建議換 MSI MAG A650BN 或全漢 Hydro G PRO 650W。
3. **SSD 報價虛標可能伴隨假料號**：賣家把 "Legend 850" 寫成 "Legend 850 PRO" 收 3x 價，要警惕**是否整單其他料件也偷換 SKU**（e.g., MB 是不是給到 B760M-E 而非 B760M-A WIFI、RAM 顆粒是否是 OEM 散裝拆封品）。建議**要求賣家給每件 component 的盒裝照 + 序號 + 保固卡**再下訂。
4. **Cooler Master Q300L 舊版已停產**，現流通版本是 Q300L V2 / Q300L Retro；菜單寫 "Q300L" 要確認賣家給的版本，舊版可能是清庫存。

---

## 🛒 採購建議

- 🥇 **原價屋 (coolpc.com.tw)** — 強烈建議直接重新估價單，菜單貼上自選 → 線上估價系統，可指定上門組裝 NT$ 800-1,500；**透明價、無虛標空間**，這份菜單拿去原價屋對價會發現多收 NT$ 12,000+
- 🥈 **欣亞 (sinya.com.tw)** — 實體店可現場驗機 / 驗 SSD 健康度（CrystalDiskInfo），對抗賣家偷換 SKU 風險最佳
- 🥉 **autobuy.tw** — 單件殺價常見（SSD/RAM 促銷），可作為原價屋的比價對照
- **不建議**：這份原菜單的賣家通路（單從報價 3x 看，幾乎可確定是 LINE 群 / 蝦皮個人賣家 / 不肖組裝店）。**直接走原價屋**，35 歲 IT 主管時間就是錢，不要花精力跟賣家拉鋸。

### 對比套裝機

- PCHome 24h / momo 同 spec（i5-14400F + 4060 Ti + 32GB + 1TB）套裝約 **NT$ 38,000-42,000**（整機 1 年保固但料件不透明）
- 原價屋自組 NT$ 34,340 + 組裝費 NT$ 1,500 = **NT$ 35,840**，每件 component 各自 3-5 年保，CP 比套裝機強
- **原菜單 NT$ 45,000+ 是雙輸**：比套裝機貴、料件還可能假，是被宰標準案例
