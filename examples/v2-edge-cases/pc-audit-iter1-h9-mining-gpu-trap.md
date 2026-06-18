# PC Build Audit — h9-mining-gpu-trap

> 預算 NT$ 28,000 · 想撿便宜挖礦卡 (RTX 3070 8GB 4,500 元) 但**怕舊礦卡有風險**
> 主訴求：在預算內撐 1080p~1440p gaming + 一些 dev workload，又想避開礦卡坑

---

## 🚨 必修 BLOCKER

### BLOCKER 1：二手 RTX 3070 礦卡 — 強烈不建議買

這是這份菜單最大的雷，先講清楚再講後面。

**為什麼是 BLOCKER（不是「風險」而已）**：

1. **RTX 30 系列 2024 已停產**，市面流通的絕大多數 3070 都是礦潮後二度就業卡。Steam 硬體調查 2023 7 月就抓到 3060 / 3070 / 3080 異常增長 → 礦卡退潮回流（PTT PC_Shopping 情報串 [未驗證討論串]）。
2. **3070 礦卡常見症狀**（PTT / 巴哈 PCDIY 反覆出現的回報 [未驗證討論]）：
   - VRAM 過熱降頻（Samsung GDDR6 焊點疲勞）→ 跑 AI / 久戰花屏黑機
   - 風扇軸承乾掉、散熱膏硬化 → 即使更新散熱也壓不下
   - PCB 氧化 / 鏽蝕（南部潮濕礦場特別嚴重）
   - 假修品：燒過拆 GPU 晶片重植 BGA，外觀完美但壽命存疑
3. **保固完全沒有**：原廠保固在第一手礦場已耗完；二手交易無賣家保固；若送修被原廠判定為礦卡會**拒保**（滄者極限討論串明文）。
4. **3070 只有 8GB VRAM** — 跑現代 AAA 1440p 高畫質已開始爆 VRAM；做 LLM dev 連 Llama 3.1 8B Q4 都要剝層。撿便宜買來卻撐不到下一個世代。
5. **「便宜」程度其實沒想像中誇張**：3070 二手行情 2026 約 NT$ 4,500–6,500，但同價位有更安全替代（見下方 Fix path）。

**Sam 怕舊礦卡是對的，這直覺要相信。**

### Fix path A（推薦）：拿掉獨顯，全力買新世代入門卡 RTX 5060 8GB

- 把獨顯預算從「4,500（礦卡）」拉到「~9,800（5060 全新）」
- 多出 ~5,300 從哪來：CPU 換 7500F → 7400F（省 1,000）、RAM 改 16GB DDR5-6000 單條（省 600）、SSD 改 WD SN580 1TB（同價）、案頭 NX410 → 小一點如 Montech AIR 100 ARGB（省 500）、PSU 換 GEX 550W（省 200）；剩下用 BIOS update / 散熱膏 / 風扇 buffer 吸收
- **新卡有原廠 3 年保固，無礦卡疑慮**，DLSS 4 + Frame Gen 比 3070 8GB 有未來
- 缺點：5060 純算力 ~= 3070，沒有跳級驚喜，但**安心**換得起

### Fix path B：APU only，等下半年加卡

- CPU 換 **AMD Ryzen 5 8600G**（內建 Radeon 780M），完全拿掉獨顯
- 1080p Low–Medium 主流遊戲（LoL / Valorant / Apex / 黑悟空降畫質）可玩
- 省下的 ~4,500 留著等 2026 Q4 RTX 5060 Ti 16GB 降到 13,000 區間再加
- AM5 平台保留升級路，這條 path 最 future-proof

### Fix path C（若堅持 8GB 等級獨顯）：Intel Arc B580 12GB 全新

- 全新 Arc B580 12GB 約 NT$ 8,500–9,500，比 3070 多 4GB VRAM、原廠 3 年保、無礦疑慮
- 純游戲 raster 性能 ~= 3060 Ti / 3070，AI workload Intel driver 還在追
- 適合「我就是要全新 + 想要 VRAM 多一點」族群

### BLOCKER 2：PSU 規格說明錯誤（minor，但要訂正）

菜單寫「COUGAR GEX 650W **bronze**」— **GEX 系列是 80+ 金牌全模組**，不是銅牌。
- 原價屋 / 欣亞 / autobuy 確認 GEX 650W 為 80+ Gold、全模組、5 年保
- 若實際拿到的是 bronze 版本（可能是 GX 系列舊款）要退換
- 維持金牌 GEX 650W 沒問題，瓦數計算見下方

---

## 🟡 2026 SSD / RAM HBM 紅利期 CALLOUT

> 因 HBM3e + AI 訓練卡需求佔走 NAND / DRAM 產能，2026 SSD / DDR5 售價相對 2023 **+30~50%**。1TB Gen4 NVMe 合理區間 NT$ 2,200–2,800、DDR5-6000 32GB kit NT$ 3,200–3,800、DDR5-5600 16GB kit NT$ 1,600–2,000。RTX 30 系列已停產二手化，這也是為何 3070 礦卡氾濫 — 新卡買不到就有人想撿便宜。

---

## ✅ Compatibility 檢查（菜單其他部分）

| 檢查項 | 結果 | 備註 |
|---|---|---|
| CPU 7500F (AM5) ↔ MB B650M-A (AM5) | ✅ 相容 | socket / chipset 完全 match |
| RAM DDR5-5600 ↔ AM5 平台 | ✅ 相容 | AM5 是 DDR5 only |
| RAM 速度 5600 vs AM5 甜蜜點 | ⚠️ 偏慢 | AM5 甜蜜點是 **DDR5-6000 CL30 EXPO**；5600 跑得起來但 IF clock 上不去，遊戲 1% low 略遜。價差只差 ~200-400，建議升 6000 |
| MB B650M-A 是否 7500F ready | ✅ 出廠 BIOS OK | 7500F 是 Zen 4，B650 板原生支援；不像 Ryzen 9000 要刷 BIOS |
| Case NX410 (ATX) ↔ MB mATX | ✅ 相容 | ATX 機殼吃 mATX 板沒問題 |
| Cooler FROZN A410 TDP 230W ↔ CPU 7500F TDP 65W | ✅ 壓力極小 | A410 壓 7500F 綽綽有餘，溫度應 < 70°C |
| PSU 650W 瓦數 | ✅ 足夠 | math 見下 |
| GPU 接頭 | ✅ 3070 是傳統 8pin x2，無 12VHPWR 燒接頭問題 |

### PSU 瓦數 math（hard rule）

```
required_watt = CPU TDP + GPU TDP + 30% headroom
              = 65W (7500F) + 220W (RTX 3070) + 30% = 285 × 1.3
              = 370W → 推 550W~650W
```

**650W 金牌足夠且有 buffer**，未來升級到 RTX 5070 (250W) 也夠。GEX 650W 維持。

---

## 💰 推薦 final spec（採 Fix Path A：5060 8GB 全新）

預算 NT$ 28,000

| 項目 | 推薦 | 價格 (NT$) | 為何選 |
|---|---|---|---|
| CPU | AMD Ryzen 5 **7500F** MPK（搭板價） | 3,990 | 6C12T、AM5、Zen 4、TDP 65W；搭板 $3,990 是原價屋甜蜜點（PTT 情報 [未驗證討論串]）。原菜單對的 |
| MB | MSI **PRO B650M-A WiFi** DDR5 | 3,490 | B650 chipset、mATX、DDR5、Wi-Fi 6E、4 年保；原菜單 OK |
| RAM | Kingston FURY Beast **DDR5-6000 32GB (16×2)** EXPO | 3,290 | AM5 甜蜜點 6000 CL30、雙通道；比原菜單 5600 16GB 大一倍、速度更快，價差只多 ~1,400 |
| SSD | Crucial **P3 Plus 1TB** Gen4 NVMe | 2,290 | Gen4 5000 MB/s、5 年保；原菜單對的（雖然是 QLC，做系統碟夠用） |
| Cooler | ID-Cooling **FROZN A410** | 790 | TDP 230W、四熱管、雙風扇；壓 7500F 綽綽有餘；原菜單 CP 值神物 |
| GPU | NVIDIA **RTX 5060 8GB** (全新，華碩 DUAL/技嘉 EAGLE) | 9,800 | 全新 3 年保、DLSS 4 + Frame Gen、1080p 高畫質滿幀、無礦卡疑慮 |
| Case | Antec **NX410** ATX | 1,790 | 3×ARGB 風扇預裝、Mesh 前面板、走線 OK；原菜單對的 |
| PSU | COUGAR **GEX 650W** 金牌全模組 | 2,090 | 80+ Gold、5 年保、285W×1.3=370W 足夠 + buffer；原菜單寫 bronze 是誤標 |
| **小計** | | **27,530** | |
| **Buffer** | 上門組裝 / 散熱膏 / 雜項 | **470** | 預留 |
| **TOTAL** | | **28,000** | 剛好打到預算上限 |

### 替代方案總價對比

| 方案 | GPU | 總價 | 風險 | 推薦度 |
|---|---|---|---|---|
| **原菜單（礦卡 3070）** | 二手 3070 8GB | ~27,400 | 🚨 高（無保固、VRAM 退化、可能花屏） | ❌ 不建議 |
| **Fix A（推薦）** | RTX 5060 8GB 全新 | 28,000 | 低 | ✅ 主推 |
| **Fix B（APU only）** | 內建 780M | ~22,500 (省 5,500) | 低（gaming 弱） | ✅ 若可等下半年加卡 |
| **Fix C（Arc B580）** | Intel B580 12GB 全新 | 27,500 | 中（driver 還在追） | ⚠️ VRAM 控可選 |

---

## 📊 Use-case 適配度

- **Primary use**：1080p gaming + 輕度 dev（推測，建議跟你確認）
- **Fix A 適配亮點**：
  - 5060 8GB 1080p 高畫質主流遊戲 60+ FPS，DLSS 4 可拉到 1440p
  - 32GB DDR5-6000 對 dev workload（多開 docker / IDE / chrome）很舒服
  - 7500F 6C12T 對純 gaming 是 sweet spot，省下的預算放到 RAM / GPU
- **未來升級空間**：
  - AM5 平台至少撐到 2027（Ryzen 11000？）— CPU 可換 9700X / 9800X3D
  - RAM 可再加 32GB 變 64GB（同 kit）
  - 第二顆 SSD M.2 slot 還有
  - PSU 650W 可撐到換 RTX 5070（250W）
- **不適合**：
  - LLM dev（8GB VRAM 連 Llama 3.1 8B Q4 都吃緊 → 要 16GB 起跳，預算要拉到 38k+ 換 5060 Ti 16GB）
  - 4K gaming（5060 不夠）
  - 影音剪輯（VRAM + CPU 都不夠 prosumer 用）

---

## ⚠️ 還沒解的 risk

1. **5060 8GB VRAM 是新時代 entry**：2026 起 8GB 在 1440p 已經會爆，買的時候要心理準備這張卡的「畫質上限壽命」可能只到 2027
2. **B650M-A WiFi 沒有 PCIe 5.0 GPU slot**（只 Gen4 x16）— 5060 / 5070 完全沒差，但若未來想上 5080 / 5090 會看到 ~3-5% 損失
3. **DDR5-6000 32GB kit QVL**：選 Kingston FURY Beast 6000 CL30 / G.Skill Flare X5 / Crucial Pro 都在 MSI B650M-A QVL，買前再對一次 part number
4. **5060 全新缺貨**：2026-06 上市初期可能要等貨；若急著用，Arc B580 是現貨備案
5. **使用情境若你其實是 LLM dev / 想跑 SDXL**：8GB 都不夠，建議直接把預算拉到 35-40k 上 5060 Ti 16GB 或撿二手 4060 Ti 16GB（4060 Ti 不在礦潮主力卡名單，二手相對安全）

---

## 🛒 採購建議

- **原價屋（coolpc.com.tw）**：CPU + MB 搭板價最殺（7500F MPK $3,990 必拿）；可勾選上門組裝 $800-1,500，幫你跑 stress test + 灌系統
- **欣亞（sinya.com.tw）**：實體店面板橋 / 台中都有，可現場驗 GPU 沒風扇異音、PSU 沒鼓包
- **autobuy.tw**：5060 上市初期會有折價券，先放購物車比價
- **不要碰**：
  - 蝦皮 / FB 社團「個人賣 RTX 3070」— 95% 礦卡
  - PCHome 24h「3070 整新福利品」— 通常是退貨修復品
  - 露天「RTX 3070 保內」— 保卡是不是真的要查序號
- **若真要買二手卡作 backup plan**：
  - 找 PTT PC_Shopping 賣場板 → 看賣家評價 / 出貨地（避開高雄潮濕區）
  - 要求 furmark 拷機 30 分鐘溫度 < 85°C 影片
  - 序號查原廠保固剩餘期限
  - 殺價砍到 NT$ 3,500 以下才值得賭

---

## TL;DR

原菜單 7 個零件**配置邏輯都對**，只有 GPU 是死穴：用 4,500 買礦卡 3070 是用安全換價差 1,000 的差勁交易。**升 5,300 拉到全新 RTX 5060 8GB**，總價剛好打 28k 上限，買的是 3 年原廠保固 + DLSS 4 + 心安。Sam 怕礦卡的直覺要相信。

PSU bronze → gold 也順便訂正。
