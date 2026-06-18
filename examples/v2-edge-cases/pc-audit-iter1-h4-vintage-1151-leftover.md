# PC Build Audit · h4-vintage-1151-leftover

> Persona: 工作室從庫存撿便宜重組 / Intel LGA1151 Coffee Lake 平台 / 預算 NT$ 18,000

---

## 🚨 必修 BLOCKER / WARNING

### ⚠️ 平台等級警告（非硬 BLOCKER，但必須先講）

LGA1151 v2 (Coffee Lake / Refresh, 8/9th gen) **2024 起 Intel 已完全停產**，這是 **dead-end 平台**：
- CPU / MB 100% 只能買二手或拆機品，**沒有原廠保固**
- 不能升級到任何新世代（後續 Intel 改 LGA1700 → LGA1851，全部重買）
- DDR4 也接近 EOL（2026 主流是 DDR5）

→ 但 persona 明確是「**工作室撿庫存便宜重組**」，這條路徑合理，繼續往下 audit。

### 🟡 相容性檢查通過（無硬 BLOCKER）

| 檢查項 | 結果 |
|---|---|
| i7-9700K (Coffee Lake Refresh) → Z390 chipset | ✅ 相容（LGA1151 v2，同 socket） |
| Z390-P 對 9th gen 9700K | ✅ 原生支援，**通常不用刷 BIOS**（Z390 2018 末出，預載 9th gen microcode） |
| Kingston DDR4-3200 16GB → Z390 | ✅ 相容（DDR4 板），但要注意下方頻率降速 |
| ATX Z390-P → Cooler Master Q500L (mATX/ATX dual) | ✅ Q500L 支援 ATX |
| Cooler Snowman M.T6 TDP → 9700K (95W TDP, 多核全載實測 ~150W) | ⚠️ 邊緣，下方詳述 |
| Antec EAG650 650W → 9700K (95W) + GTX 1660 Super (125W) | ✅ 瓦數充裕，下方有 math |

### ⚠️ 真實風險點（不修不會炸，但要知道）

1. **i7-9700K 是「第三手」**：9700K 是 2018 出的旗艦，原使用者通常**長期全開超頻、跑遊戲/挖礦**，矽穩定度衰退、可能 delidded 過。買到要求**現場跑 Cinebench R23 多核 10 分鐘**驗穩定。
2. **Z390-P 二手**：BigGo 報價中位數 ~$1,500-2,000（拆機無盒）。Z390-P **不是高階 SKU**（VRM 7-phase 偏弱），長期燒 9700K 95W TDP 在 VRM 散熱有壓力，不建議再開 5.0+ GHz OC。
3. **Snowman M.T6 是 AliExpress 平輸**：標稱 TDP 245W 是行銷數字，實測壓 9700K all-core 大約撐到 80°C 邊緣 → 9700K 不超頻可用，**任何全核 OC 不要碰**。
4. **DDR4-3200 在 Z390 跑 3200 要看運氣**：9th gen Intel 官方規格 **DDR4-2666**，3200 要靠 XMP，Z390-P 中低階板有時 XMP 不穩開不到 3200（只能降 2933）。

### 🟡 2026 SSD / RAM HBM 紅利期 baseline（必引述）

> 因 HBM3e + AI 訓練卡需求佔走 NAND / DRAM 產能，2026 SSD / DDR 售價相對 2023 **+30~50%**。  
> 1TB SATA SSD ≈ $2,000-2,400、DDR4-3200 16GB kit ≈ $1,600-2,000 為合理區間。  
> **這份菜單 DDR4 + SATA SSD 反而避開了 DDR5/Gen4 NVMe 紅利期溢價**，是這個 build 唯一比 2026 新平台便宜的點。

### ⚙️ PSU math line（hard rule）

```
required_watt = CPU TDP + GPU TDP + 30% headroom
             = 9700K (95W) + GTX 1660 Super (125W) + 30%
             = 220W × 1.3
             = 286W → 推薦 450W 起跳即可
```

→ **EAG650 (650W) 大幅超規**，可以撐未來換到 RTX 4060 / 5060 等級 GPU。OK。

---

## 💰 NT$ 18,000 預算 final spec（保留 + 微調）

整份菜單**基本通過**，下方表格給：建議價格區間（依 BigGo / 飛比 / coolpc 2026-06 中位數）+ 為何保留 / 微調 reasoning。

| 項目 | 推薦 | 估價 NT$ | 為何選 / 為何保留 |
|---|---|---|---|
| CPU | Intel i7-9700K (3rd-hand) | $2,800 - $3,800 | 8C8T 純物理核，工作室一般生產力夠用；**驗機必跑 R23 ×10min** |
| MB | ASUS PRIME Z390-P (used) | $1,500 - $2,000 | 同 socket、ATX 大板；VRM 中階別 OC；**買前確認 BIOS 不要太舊，最好賣家先刷到 1801 以後** |
| RAM | Kingston FURY Beast DDR4-3200 16GB (2×8) | $1,600 - $1,900 | 雙通道、容量足；**XMP 跑不到 3200 就降 2933**，差距 < 3% |
| SSD | Crucial MX500 SATA 1TB | $1,900 - $2,300 | TLC 顆粒、5 年保仍在；速度只有 560 MB/s 但**工作室文件 / 編譯產物夠用** |
| GPU | GTX 1660 Super 6GB (used) | $3,000 - $3,800 | 1080p 中畫質 OK；**6GB VRAM 對 AI / LLM 完全不夠**（下方 use-case 註記） |
| Cooler | Snowman M.T6 雙塔風冷 | $700 - $900 | AliExpress 平輸雙塔六熱管；壓 9700K 不超頻 OK；不要碰 OC |
| Case | Cooler Master Q500L | $1,600 - $1,800 | ATX 緊湊機殼；空間夠 Z390-P + 1660 Super (250mm 內) |
| PSU | Antec EAG650 650W 80+ Gold | $2,200 - $2,600 | 半模 Gold；瓦數對 9700K + 1660S 有大量 headroom |
| **TOTAL（中位數）** | | **約 $15,300 - $19,100** | 預算內，buffer **$0 - $2,700** 留組裝/雜項 |

→ **菜單原樣放行**。不需要替換任何零件。

---

## 📊 Use-case 適配度

- **Primary use**：工作室通用生產力（文件 / 開發 / 輕度 1080p 遊戲 / 內部測試機）
- **適配亮點**：
  - 8 物理核 9700K → 編譯 / 多開 IDE / Docker 都吃得下
  - GTX 1660 Super → 1080p Medium-High 主流遊戲（CS2 / 英雄聯盟 / Valorant）穩 100+ FPS
  - 650W PSU 留瓦數 → 之後撿到 RTX 3060 / 4060 二手能直上不用換電源
- **❌ 不適用**：
  - **AI / LLM dev**：1660S 只有 6GB VRAM，Llama 3.1 8B Q4 都裝不下。要 LLM 必須升 16GB VRAM 卡（RTX 4060 Ti 16GB / 5060 Ti 16GB / 二手 3090 24GB）。
  - **影音剪輯（Premiere/DaVinci）**：1660S 沒 AV1 encode、VRAM 太小；4K 剪輯卡頓。
  - **3D render（Blender Cycles）**：6GB VRAM 撐不住複雜場景。

→ 工作室如果之後要碰 AI，**GPU 一定要換**。其他零件可留。

### 未來升級空間（Coffee Lake 平台天花板）

| 項目 | 可升級到 |
|---|---|
| CPU | 平台天花板就是 9900K (8C16T)，二手 $4,000-5,000；不值得換 |
| RAM | 32GB（再加 2×8 同型號）；Z390-P 4 槽，上限 64GB |
| SSD | 加裝第二顆 NVMe（Z390-P 有 1× M.2 PCIe 3.0 slot）→ 注意是 **Gen3** 不是 Gen4 |
| GPU | **這台升級空間最大的零件**；650W PSU 撐到 RTX 4070 Super (220W) 沒問題 |
| 平台 | **無路可升**，要新世代要整套換 LGA1700 / 1851 / AM5 |

---

## ⚠️ 還沒解的 risk

1. **9700K 第三手矽質量是賭運氣**：賣家若不肯讓你現場 stress test 就**直接走人**。買回家壞了二手無保。
2. **Z390-P 二手 BIOS 版本**：若賣家不確定 BIOS 版本，準備一顆便宜 8th gen（i3-8100 二手 $500）做 BIOS 復活備援。
3. **Snowman M.T6 安裝品質**：AliExpress 平輸壓力不均常見，**塗散熱膏一定要均勻**、扣具鎖緊。建議準備 MX-4 / TF7 散熱膏 ($200) 重塗。
4. **1660 Super 是否礦卡**：1660S 是 2019-2021 ETH 礦卡主力之一，**強烈建議只買有原廠序號 + 賣家能秀購買憑證**的。VRAM 衰退會跑遊戲花屏 / 跳驅動。
5. **Q500L 機殼風扇預設只有 1 顆後排**：建議補 2 顆前進風 ($300-500），否則夏天 9700K + 1660S 全載會悶。
6. **DDR4-3200 雙條 XMP 開不上**：Z390-P 中階板 BIOS 若不穩，先降 DDR4-2933 試。
7. **EAG650 不是 ATX 3.0**：但因為沒上 RTX 40+ 12V-2x6 GPU，**不需要 ATX 3.0**，現規格夠用。
8. **無 Wi-Fi**：Z390-P 沒內建 Wi-Fi，要無線網要加 PCIe Wi-Fi 卡 ($600-1,000) 或 USB Wi-Fi 棒 ($300)。

---

## 🛒 採購建議

這台**全部都是二手 / 撿庫存**，採購通路跟一般自組不一樣：

| 通路 | 用途 | 風險 |
|---|---|---|
| **PTT PC_Shopping 買賣版** | CPU / MB / GPU 二手主力（價格最低、看得到賣家評價歷史） | 自負風險、可面交驗機 |
| **巴哈姆特 PCDIY 交易區** | 同上，另一個社群池 | 同上 |
| **蝦皮拍賣**「3C零件 → 二手」 | GPU / SSD / PSU 二手 | 蝦皮買家保護 7 天，但賣家可能拒退 |
| **Yahoo 拍賣 / 露天** | 雜項零件 / Snowman 等平輸 | 平輸無台灣保固 |
| **原價屋 (coolpc.com.tw)** | **只用來買新零件**：Q500L 機殼、EAG650 PSU、Kingston RAM、MX500 SSD、Snowman 散熱、散熱膏 | 新品有保固 |
| **AliExpress** | Snowman M.T6 來源（如果原價屋沒貨） | 等 2-3 週、海關運費 |

### 推薦採購順序

1. **先去原價屋**買新品零件（PSU + 機殼 + RAM + SSD + 散熱）→ 約 $7,500-8,500
2. **再去 PTT / 巴哈交易區**等 9700K + Z390-P + 1660S 的合理開價（可以等 1-2 週撿）→ 約 $7,000-9,000
3. **預留 $1,500** 給：散熱膏 ($200) + 前進風扇 ×2 ($400-600) + Wi-Fi 方案 ($300-1000) + 雜項
4. **不建議付上門組裝費**（$800-1,500），這份菜單二手居多賣場不一定收，自己組學一次 ROI 高

### 套裝機對比

PCHome / momo **不會賣 LGA1151 套裝機**（早停產），這個 build 是「**只有自組 + 撿便宜才存在的解**」，找不到對比基準。

---

### 📌 audit 結論一句話

> **菜單整套通過、預算內 $15.3k-19.1k 區間落入 $18k 預算**；風險全部在「二手三個零件（CPU/MB/GPU）能否驗機通過」，硬體規格相容性 OK，但**這台不能拿來碰 AI / LLM** —— 要 AI 等之後升 GPU 到 16GB VRAM。
