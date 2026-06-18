# PC Build Audit — H610 + Gen5 SSD + 多 M.2 Lane 災難 (預算 NT$28,000)

## 🚨 必修 BLOCKER

這份菜單有**三個 showstopper**，一個比一個嚴重，**主機板選錯了**是根因。

### BLOCKER #1 — ASUS PRIME H610M-D D4 只有 **1 個 M.2 插槽**，第二顆 SSD 沒地方裝

查 ASUS 官方 spec：PRIME H610M-D D4 全板只有 **1× M.2 (PCIe 4.0 x4)**。
- Crucial T700 2TB 裝上去 → 佔掉唯一 M.2
- **Lexar NM800 PRO 1TB 完全無處安裝** ← 直接買回家放抽屜
- H610M-D D4 也只有 **4× SATA**，但 NM800 PRO 是 M.2 NVMe，不能轉 SATA 接，**沒有任何方法救援**

### BLOCKER #2 — Crucial T700 是 **PCIe Gen5 SSD**，但整個 H610 平台沒有 Gen5 storage lane

技術細節：
- i3-14100F (Raptor Lake Refresh) CPU 確實有 PCIe 5.0 lane，但**只給 GPU x16 slot**，不給 storage
- **H610 chipset 全板 storage M.2 規格上限 = PCIe 4.0 x4**（ASUS spec 寫死）
- T700 標稱 12,400 MB/s 讀取，插上去**強制降速到 ~7,000 MB/s**（Gen4 頻寬天花板）
- 你花了 Gen5 SSD 的錢（~$6,500）只跑 Gen4 的速度，**$3,000+ 直接浪費**
- 而且 T700 是出了名的發燒大戶，H610M-D D4 **沒附 M.2 散熱片**，會 thermal throttle 再掉一波速度

### BLOCKER #3 — i3-14100F 是 4C/8T 入門 CPU，配 Gen5 SSD 完全是 spec mismatch

- 4 核 8 緒處理器的 IO bottleneck 早就不在 SSD，而在 CPU 本身
- Gen5 SSD 的優勢場景是 AI dataset loading / 8K 影音剪輯 / 大型 DB —— i3-14100F 根本跑不動這些 workload
- 拿 Gen5 SSD 配 i3 就像給 March 裝渦輪，**錢花在錯的零件上**

### Fix Path（推薦 Path A）

**Path A（推薦）：H610 平台 + 換掉 Gen5 SSD + 把錢挪到 GPU/CPU**
- 主板換 **ASUS PRIME B760M-K D4** 或 **MSI PRO B760M-E D4**（B760, 2× M.2 都 Gen4 x4, $2,490–2,890）
- 拔掉 T700 Gen5，改 **WD Black SN770 2TB Gen4** 或 **Lexar NM790 2TB**（$3,990–4,490，Gen4 效能完全夠 i3 用）
- 留 Lexar NM800 PRO 1TB 當第二顆遊戲碟 → B760 有兩個 M.2 都能用
- 省下的 ~$2,000 升 GPU 到 **RX 7600** 或 CPU 升 **i5-14400F**

**Path B（保 H610 + 砍配置）：**
- 主板留 H610M-D D4，但**只裝一顆 SSD**：留 Lexar NM800 PRO 1TB，T700 退掉
- 省下的 $4,000+ 直接升 **i5-14400F**（10C/16T）+ **RX 7600 8GB**
- 但仍要警告：H610 是死路平台，未來不能升 i9 / 不能超頻記憶體

**Path C（重灌 spec，升 AM5 內顯路線）：**
- 換 **Ryzen 5 8500G** + **A620M** + DDR5 16GB，內顯夠日常 + 輕度遊戲
- 把 GPU 預算挪到 **RX 7600 XT 16GB**（如果有 LLM/AI 需求才走這條）

---

## 💰 [預算 $28,000] 內 final spec（採 **Path A**）

### 🟡 2026 SSD / RAM HBM 紅利期 baseline
> 因 HBM3e + AI 訓練卡需求佔走 NAND / DRAM 產能，2026 SSD / DDR5 售價相對 2023 **+30~50%**。1TB Gen4 NVMe ≈ $2,200–2,800、DDR4-3200 16GB kit ≈ $1,200–1,500 仍相對便宜（DDR4 已退場降溫）。報價低於此區間反而要懷疑水貨/拆機。

### PSU math
```
required_watt = CPU TDP + GPU TDP + 30% headroom
              = i3-14100F (58W base, 110W boost) + RX 6600 (132W) + 30%
              = 242W × 1.3 = 315W → 推 550W 就夠用，650W 是奢侈
```
原菜單的 Antec NeoEco 650W 對這台 build 是**過大配置**，但 650W 80+ Bronze 留升級空間沒問題，留著。

### Final spec table

| 項目 | 推薦 | 價格 | 為何選 |
|---|---|---|---|
| CPU | Intel Core i3-14100F | $3,490 | 4C/8T、LGA1700、TDP 58W，散熱壓力小；1080p gaming 配 RX 6600 不瓶頸 |
| MB | **ASUS PRIME B760M-K D4**（換掉 H610M-D D4） | $2,490 | B760 給 **2× M.2 Gen4 x4**，兩顆 SSD 都能裝；H610 永久跳掉 |
| RAM | Klevv CRAS XR5 DDR4-3200 16GB (8×2) | $1,290 | DDR4-3200 是 LGA1700 D4 板甜蜜點；雙通道 8GBx2 比單條 16GB 性能好 15% |
| SSD #1 | **WD Black SN770 2TB Gen4**（換掉 T700 Gen5） | $4,490 | Gen4 5,150 MB/s 對 i3 完全夠用；無 DRAM 但 HMB 補；5 年保 |
| SSD #2 | Lexar NM800 PRO 1TB Gen4 | $2,290 | 第二顆遊戲/工作碟，B760 第二個 M.2 槽剛好接 |
| GPU | AMD RX 6600 8GB | $5,990 | 1080p Medium-High 主流遊戲穩 60+ FPS；PCIe 4.0 x8 不挑板 |
| PSU | Antec NeoEco 650W 80+ Bronze | $2,090 | 留原配置；瓦數有餘 = 安靜風扇低轉、留升 GPU 空間 |
| Cooler | ID-Cooling DK-03 | $450 | 單塔 95W TDP，壓 i3-14100F (58W base) 綽綽有餘 |
| Case | DeepCool Matrexx 50 ATX | $1,490 | ATX 中塔、走線 OK、含 4× 風扇位；側透美觀 |
| **小計** | | **$24,070** | |
| Buffer | 上門組裝費 + 散熱膏 + 風扇 | **$1,500** | 原價屋上門 $800–1,500 |
| **TOTAL** | | **~$25,570** | **剩 $2,430 buffer**（在 $28K 預算內） |

預算還剩 **$2,430**，可選：
- 升 SSD #1 到 **Lexar NM790 4TB**（+$3,500，超預算少量）
- 升 GPU 到 **RX 7600 8GB**（+$1,500，1080p Ultra/1440p Medium 更穩）← **建議**
- 加 **Wi-Fi 6 PCIe 卡**（B760M-K 無內建 Wi-Fi，+$600）

---

## 📊 Use-case 適配度

- **Primary use 推測**：1080p gaming + 日常 + 輕度工作（從 i3 + RX 6600 + Gen5 SSD 矛盾組合看，原 build 主人可能是被通路推銷 Gen5 SSD 沒搞懂）
- **適配亮點**（Path A）：
  - 1080p Medium-High AAA 遊戲穩 60 FPS（RX 6600 benchmark vs 3060 互有勝負）
  - 雙 SSD 配置 6TB 容量（2T + 1T），夠裝 Steam library + 工作檔
  - DDR4 平台 RAM 便宜，要升 32GB 之後只要 +$1,290
- **不適合**：AI / LLM dev（VRAM 8GB 不夠）、4K gaming、影音剪輯
- **升級空間**：
  - CPU 升 **i5-14400F** / **i5-14600KF**（LGA1700 同腳位，B760 直接吃）
  - RAM 升 32GB（2 條 16GB 替換掉 8×2）
  - GPU 升 **RX 7700 XT** 或 **RTX 4060 Ti 16GB**（PSU 650W 還夠）

---

## ⚠️ 還沒解的 risk

1. **LGA1700 是死路平台** — Intel 已轉 LGA1851（Core Ultra 200），i3-14100F 是 LGA1700 末代 i3。將來想升 i7/i9 仍可用同主板，但**不能升下世代 CPU**。
2. **H610 / B760 都不支援 RAM 超頻** — DDR4-3200 是 JEDEC 上限，買 DDR4-3600 / 4000 kit 也只跑 3200。所以 Klevv CRAS XR5 DDR4-3200 剛好踩點，**不要花錢買更高頻 DDR4**。
3. **PCIe lane 共享警告**（即使換 B760）— B760M-K 的第二個 M.2 是走 chipset DMI，跟 SATA / USB 共享頻寬。同時跑兩個 SSD 大量讀寫，總頻寬不會超過 DMI 4.0 x4（~7.8 GB/s），但日常用感受不到。
4. **RX 6600 是 PCIe 4.0 x8** — 在 PCIe 4.0 板上零損失，但若未來升二手 PCIe 3.0 系統會掉約 5–10% FPS（你不會這樣做，提醒備案）。
5. **DDR4 庫存退場風險** — 2026 DDR4 已停產，新貨越來越少。RAM 故障要換貨可能買不到同 kit，建議**多買一條備品**或保留發票走原廠保。
6. **Antec NeoEco 650W 是定電壓非全模組** — 線材無法拆，背線機殼會塞滿線。可接受，但若機殼小要注意走線空間。

---

## 🛒 採購建議

- **原價屋（coolpc.com.tw）**：菜單貼上自選，可指定**代刷主板 BIOS + 上門組裝**（$800–1,500）；B760M-K 出廠 BIOS 通常已支援 14 代，但保險請代驗。
- **欣亞（sinya.com.tw）**：實體店現場驗機，14 代 i3 + RX 6600 都是常備庫存。
- **autobuy.tw**：促銷時 SSD 殺價兇，WD SN770 2TB 有時殺到 $3,990。
- **套裝機對比**：PCHome 24h 同 spec 套裝（i3-14100F + RX 6600 + 16GB + 1TB）約 $26,900–28,900，**自組省 ~$2–3K** 但要會組裝 + 跑 MemTest86 + 3DMark stress。
- **二手警示**：RX 6600 / 6650 XT 二手 $3,500–4,500，但 2022 礦潮後流出顯卡多，**買二手卡務必跑 FurMark 30 分鐘 + GPU-Z 看 fan curve**，礦卡 VRAM 退化常見。

---

## 📋 改動摘要（給用戶 1 行版）

> 原 build 主板選 H610M-D D4 → **只 1 個 M.2 槽 + 不支援 Gen5**，Lexar SSD 沒地方裝、T700 Gen5 強制降速。**主板換 B760M-K D4 + T700 換 SN770 2TB Gen4**，省 $2,000 升 GPU 或留 buffer，**問題解掉、預算內、性能不減反增**。
