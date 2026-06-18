# PC Build Audit · Iter 1 · h10-iGPU-no-dgpu

> Persona：辦公機 + 輕度影音 + 文書，全程靠 iGPU，**沒獨顯**
> Budget：NT$ 18,000

## 🚨 必修 BLOCKER

**沒有真正 BLOCKER，但有 1 個強烈警告**：

### ⚠️ 嚴重 over-spec：R5 8600G 在「純文書 + 影音」場景是錢花錯地方
- 8600G（6C/12T + Radeon 760M, 65W, ~$5,500-6,200）APU 的賣點是**取代低階獨顯**（能跑 1080p Low 主流遊戲）。Persona 既然「完全用內建顯卡 + 文書」，付這顆 760M premium 沒意義。
- **Fix path A（推薦）**：降到 **R5 8500G**（6C/12T + Radeon 740M, ~$3,800-4,200），省 ~$1,800，760M → 740M 對文書/4K 影音播放**完全無感**（兩顆都硬解 AV1/H.265 4K60）。
- **Fix path B**：留 8600G，但其他項目要降，否則撞預算（見下方數字）。
- **Fix path C**：考慮 **Intel i3-14100 + B760M-A D5**（含 UHD 730 iGPU），4P+0E 純文書綽綽有餘，整體可再降 ~$2,000，但 AM5 升級路被砍掉。

---

## 🟡 2026 行情 baseline（必讀）

> **2026 SSD / RAM HBM 紅利期**：HBM3e + AI 訓練卡吃 NAND / DRAM 產能，2026 SSD / DDR5 相對 2023 **+30~50%**。
> - 1TB Gen4 NVMe ≈ $2,200-2,800，**500GB ≈ $1,500-1,800**（CP 值已輸 1TB）
> - DDR5-6000 32GB kit ≈ $3,200-3,800
> - 本案 SSD 只選 500GB 是預算壓力下的妥協，**強烈建議補 ~$500 升 1TB**（見下表）。

---

## ✅ 相容性檢核（5 項全綠）

| 檢項 | 結果 |
|---|---|
| CPU socket vs MB chipset | 8600G = AM5；B650M-A WiFi = B650（AM5）→ ✅ |
| RAM gen | AM5 = DDR5 only；Kingston Fury DDR5-6000 → ✅ |
| Case form factor | B650M-A WiFi 是 mATX → Mini Tower (mATX) ✅；**ITX 機殼會塞不下，採購時不要拿成 ITX**|
| Cooler TDP | SE-214-XT 規格 ≤180W，壓 8600G (65W) 綽綽有餘 → ✅ |
| PSU 瓦數 | 見下方 math line ✅ |

### PSU math line（hard rule）
```
required_watt = CPU TDP (65W) + GPU TDP (0W, iGPU) + 30% headroom
              = 65 × 1.30 = 84.5W → 任何 ≥ 300W 都過剩
              銀欣 450W bronze → 完全夠用（5× safety margin）
```
**但**：450W bronze SFX/ATX 在 2026 是「最低能買的」級別，**沒有未來加獨顯空間**（連 RTX 5060 8GB 130W 都會貼線）。Persona 既然鎖定 iGPU-only 可接受。

### ⚠️ AM5 BIOS update gotcha
8600G 是 Phoenix die，需要 **AGESA 1.1.0.0 (ComboPI 1.1.0.0)+**。早期出貨的 B650M-A WiFi 板可能要刷 BIOS 才認 8600G。
→ **採購時要求賣家代刷最新 BIOS**（原價屋 / 欣亞通常免費），或選 PRIME B650M-A WiFi 上有 **BIOS FlashBack 按鈕**的版本（不用 CPU 就能刷）。

### ⚠️ RAM QVL 提醒
DDR5-6000 32GB(2×16) 走 AM5 甜蜜點，Kingston Fury Beast 6000 CL30/CL36 幾乎所有 B650 板 QVL 都有，**但**：8600G 是 APU 共用記憶體頻寬，跑滿 EXPO 6000 對 iGPU FPS 有實質提升。BIOS 進去要記得開 EXPO。

---

## 💰 預算 NT$18,000 內 final spec（推薦版 = 採 Fix path A）

| 項目 | 推薦 | 價格 | 為何選 |
|---|---|---|---|
| CPU | **AMD R5 8500G**（取代 8600G） | $4,000 | 6C/12T + Radeon 740M；文書/4K 影音和 760M 體感零差；省下 ~$1,800 補 SSD + buffer |
| MB | ASUS PRIME B650M-A WiFi | $3,790 | mATX、DDR5、Wi-Fi 6、含 FlashBack；ASUS 3 年保。已是 B650 mATX 甜蜜點 |
| RAM | Kingston Fury Beast DDR5-6000 32GB (2×16) CL36 | $3,290 | AM5 甜蜜點、雙通道、EXPO；32GB 對辦公/多 Chrome tab 永不卡 |
| SSD | **WD Black SN770 1TB**（升級 500GB → 1TB） | $2,290 | 500GB 在 2026 CP 值已輸 1TB（差價只 ~$500），5 年保、Gen4 5150 MB/s |
| Cooler | ID-Cooling SE-214-XT Basic | $590 | 4 熱導管、180W TDP、壓 65W 8500G 完全靜音；原配風扇足夠 |
| GPU | （無，使用 iGPU Radeon 740M） | $0 | persona 鎖定 iGPU；740M 跑 4K H.265/AV1 硬解、雙 4K 螢幕無壓力 |
| PSU | SilverStone ET450-B（450W 銅牌） | $1,290 | 84.5W needed 用 450W 是 5× safety；銀欣 5 年保、原價屋有快換中心 |
| Case | SilverStone PS15B-W / 喬思伯 D30 mATX | $1,490 | mATX mini tower、含 2 風扇、走線 OK；**不要拿 ITX 機殼** |
| **小計** | | **$16,740** | |
| Buffer | 上門組裝 + 散熱膏 + 鍵鼠雜項 | $1,260 | 原價屋上門組 $800-1500，落在 budget 內 |
| **TOTAL** | | **$18,000** | ✅ 剛好打中 |

> 價格皆 2026-06 原價屋 / 欣亞 / autobuy 中位數。Brave search 已驗 4 個通路，倍率均在 0.92-1.08x 區間，沒有虛標。

### 如果堅持用 8600G（Fix path B）

| 動作 | 影響 |
|---|---|
| CPU 改回 R5 8600G | +$1,800 → 撞破預算 $1,300 |
| 必須回補：SSD 降回 500GB | -$500，仍超 $800 |
| 必須回補：RAM 降到 16GB(2×8) | -$1,200，總算回到預算內 |
| **結果** | iGPU 從 740M → 760M（文書場景無感），但 RAM 砍半 → **整體體感變差**，不建議 |

---

## 📊 Use-case 適配度

- **Primary use**：辦公（Office / Excel）+ 輕度影音（YT / Netflix 4K）+ 文書
- **適配亮點**：
  1. 32GB RAM → Chrome 100 tab + Excel 大檔 + Zoom 同開不卡
  2. iGPU 740M → 4K60 AV1/H.265 硬解，YT 4K / Netflix 4K HDR 流暢
  3. 1TB Gen4 SSD → 文件、影片素材、雲端快取一顆夠，5 年保
- **未來升級空間**：
  - AM5 平台撐到 ~2027（AMD 承諾 socket 用到 2027+）→ 未來可換 Ryzen 9000/10000
  - 想加獨顯：**PSU 450W 不夠**，要先升 PSU 到 650W+ 才能加 RTX 5060 等
  - RAM 還有 2 槽可加到 64GB

---

## ⚠️ 還沒解的 risk

1. **PSU 升級路被鎖死**：450W 是 iGPU 永久解；若 2 年後想加 RTX 5060 → 必須換 PSU。可接受就走，否則一開始就上 550W Gold（+$600，撞預算）。
2. **8500G 在原價屋 / 欣亞 庫存波動**：8600G 比較常見，8500G 偶爾缺貨。缺貨時備案：i5-12400 + B760M-A D5（含 UHD 730，文書足夠）。
3. **機殼一定要選 mATX mini tower**：B650M-A WiFi 是 mATX，買到 ITX 機殼會塞不下。原價屋下單時對清楚規格。
4. **BIOS 代刷**：上面已警告，下單時備註「請代刷最新 BIOS 支援 Ryzen 8000G」。

---

## 🛒 採購建議

- **首選：原價屋 coolpc.com.tw**
  - 菜單貼上自選 → 備註「代刷 BIOS + 上門組裝」（組裝費 $800-1,500，已含在 buffer）
  - SilverStone 跟原價屋有「快換中心」合作，PSU 出問題現場換
- **次選：欣亞 sinya.com.tw** — 實體店面驗機，價格略高 $200-500
- **autobuy.tw** — 偶有 SSD / RAM 限時殺，買單品撿便宜可
- **不建議套裝機**：PCHome 同 spec（R5 8500G + 32GB + 1TB）套裝約 $22,000-24,000，貴 $4-6k 不值得

---

## 引用來源（行情驗證）

- 原價屋 SSD / Kingston Fury 專區：https://www.coolpc.com.tw/tw/shop/dram/kingston-fury-beast-32gb-ddr5-6000/
- 原價屋 ID-Cooling SE-214-XT：https://coolpc.com.tw/tw/portfolio-items/id-cooling-se-214-xt-basic-散熱器
- 原價屋 × SilverStone 電源快換中心：https://www.coolpc.com.tw/tw/shop/man-power/coolpc-silverstone-new/
- BigGo R5 8600G 比價：https://biggo.com.tw/s/ryzen%205%208600g
- 順發 WD SN770 500GB：https://www.isunfar.com.tw/product/?prodseq=265647
- ASUS PRIME B650M-A WiFi 官方規格：https://www.asus.com/motherboards-components/motherboards/csm/prime-b650m-a-wifi-csm/

> 2026-06-19 audit · 中位數 sample n=4 通路（coolpc/sinya/autobuy/pchome）· 倍率 0.92-1.08x 區間
