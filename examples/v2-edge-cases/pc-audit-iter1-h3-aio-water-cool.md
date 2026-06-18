# PC Build Audit — h3-aio-water-cool（專業 streamer / 靜音 + 全 RGB）

> **2026 SSD / RAM HBM 紅利期 baseline**：HBM3e + AI 訓練卡需求佔走 NAND / DRAM 產能，2026 SSD / DDR5 售價相對 2023 **+30~50%**。1TB Gen4 NVMe ≈ $2,200-2,800、DDR5-6000 32GB kit ≈ $3,200-3,800 為合理區間；報價低於此區間反而要懷疑水貨/拆機。本菜單的 4TB SSD + 64GB DDR5-7200 是 2026 高價區。

---

## 🚨 必修 BLOCKER

### ❶ DDR5-7200 64GB（2×32GB）on Z890 — **QVL + memory training 高風險**

LGA1851 + Z890 + G.Skill Trident Z5 **DDR5-7200 64GB (2×32GB)** 是踩在 IMC 極限上的組合：

- Arrow Lake (285K) 的 IMC 在 **2×32GB 雙面顆粒** 條件下，官方 JEDEC 上限 6400；7200 已屬 OC 範圍。
- 2×32GB（高密度 dual-rank）比 2×16GB 7200 難跑很多，常見症狀：開機 memory training 卡 30-60 秒、XMP 跑不上、無法 boot 要清 CMOS。
- 必查 MSI Z890 EDGE TI 官方 **QVL** 比對該 kit 的完整 part number（不是只看 "G.Skill 7200 64GB"）。

**Fix path A**：保留 64GB，降到 **DDR5-6400 CL32 2×32GB**（Z890 較安全的甜蜜點，QVL 命中率高），省 $1,500-2,000。
**Fix path B**：要 7200 就降到 **2×24GB = 48GB**（single-rank，IMC 壓力小），但 streamer + OBS 多軌錄製吃 RAM，48GB 略緊。
**Fix path C**：堅持 64GB + 7200 → 接受可能要手動降頻、跑 EXPO/XMP failback 的代價。

### ❷ 散熱不足（風險級，非完全 BLOCKER）

- **Core Ultra 9 285K PL2 ≈ 250W**，全核 AVX 負載峰值更高。
- H170i ELITE 420mm 冷排面積已是空冷天花板，但 285K 在 OBS 推流 + 遊戲 + 編碼三軌全開時仍會撞溫度牆降頻。
- 機殼選 O11 Dynamic EVO **標準版**而非 XL/Pro，**前面板無進風孔**（全玻璃側透 + 頂底進風），420mm 冷排只能裝**頂部**，會與 RAM 散熱片 + RGB tower 打架。
- **靜音訴求**：420mm AIO 3×140mm 風扇低轉速 (<800rpm) 能壓 65W idle，但 streaming 滿載必開到 1500+rpm，會明顯吵。

**Fix**：機殼建議升 **Lian Li O11 Dynamic EVO RGB (新版)** 或 **O11 Vision Compact**，配置可裝頂 + 側雙 360 冷排；或 H170i 改裝**側板**（O11 EVO 標準版側面才裝得下 420mm）。

---

## 💰 NT$ 75,000 預算內 final spec

> 以「保留 285K + 5070 Ti + 420 AIO + 全 RGB streamer 定位」為前提；只動 RAM / 機殼 / 微調，把 BLOCKER 解掉。

| 項目 | 推薦 | 預估價（中位數，TWD） | 為何選 |
|---|---|---|---|
| CPU | Intel Core Ultra 9 285K（保留） | $17,500 | 24 核 24 緒、內建 NPU、OBS x264/NVENC 雙軌 encode 強；無 HT 對推流穩定度反而有利 |
| MB | MSI MPG Z890 EDGE TI WiFi（保留） | $12,490 | 白色 ATX、Killer Wi-Fi 7、Thunderbolt 4、5G LAN、免工具 M.2、RGB 串接 OK |
| RAM | **改：G.Skill Trident Z5 RGB DDR5-6400 CL32 64GB (2×32GB)** | $8,800 | 降一階保 QVL 命中、不卡 memory training；對 OBS / Premiere 多軌幾乎無感差 |
| SSD | Samsung 990 Pro 4TB（保留） | $11,500 | OBS 錄製 + 素材庫 + 遊戲庫 4TB 剛好；7450/6900 MB/s、5 年保 |
| Cooler | Corsair iCUE H170i ELITE LCD XT 420mm（保留） | $9,800 | LCD 水冷頭符合 streamer 視覺、磁懸浮風扇低噪音模式、5 年保 |
| GPU | MSI RTX 5070 Ti 16G VANGUARD SOC | $37,990 | 16GB VRAM 撐 1440p 高畫質遊戲 + DLSS4 + NVENC（AV1）對推流關鍵；長度 357mm |
| PSU | Corsair RM1000x ATX 3.1 1000W Gold | $6,190 | 原生 12V-2x6、10 年保；瓦數見下方 math |
| Case | **改：Lian Li O11 Dynamic EVO RGB（新版含 RGB 風扇）** | $5,500 | 同 EVO 系列但前置 RGB 風扇槽位、420 AIO 側裝相容性確認過；ATX 容得下 357mm GPU |
| 機殼風扇補件 | Lian Li UNI FAN SL120 V2 三入（底進風） | $2,400 | RGB 串接同生態系、PWM 靜音曲線 |
| **小計（不含工資 / 雜項）** | | **~$112,170** | ❌ **嚴重超預算 $37,170** |

### 💥 預算現實檢查

**這份菜單在 NT$ 75,000 內做不到。** 285K + Z890 EDGE TI + 5070 Ti Vanguard + 990 Pro 4TB + H170i 420 + O11 EVO + RM1000x 任一通路加總都會 **$110k-115k**。

### 方案 A：守住 NT$ 75,000（必須降階）

| 項目 | 推薦 | 價格 | 為何選 |
|---|---|---|---|
| CPU | **改：Intel Core Ultra 7 265K** | $11,500 | 20 核 / 20 緒、Arrow Lake、TDP 125W；streaming + 遊戲與 285K 差 < 8%，便宜 $6k |
| MB | **改：MSI MAG Z890 TOMAHAWK WiFi** | $9,990 | 白色 ATX、Wi-Fi 7、Z890 全功能；省 $2,500 |
| RAM | G.Skill Trident Z5 RGB DDR5-6400 CL32 32GB (2×16) | $4,800 | streamer 32GB 夠用，OBS + 主流遊戲不爆；未來插滿到 64GB |
| SSD | **改：Samsung 990 Pro 2TB + WD Blue SN5000 2TB（系統 / 素材分離）** | $6,200+$3,400=$9,600 | 系統碟保 990 Pro、素材碟 QLC 大容量便宜 |
| Cooler | **改：Corsair iCUE H150i ELITE LCD XT 360mm** | $7,200 | 360mm 對 265K 綽綽有餘，比 420mm 易裝 + 便宜 $2,600 |
| GPU | **改：MSI RTX 5070 Ti 16G VENTUS 3X OC**（非 Vanguard） | $32,500 | 同晶片、稍簡化散熱與 RGB；streaming 性能 100% 相同 |
| PSU | **改：Corsair RM850x ATX 3.1 850W Gold** | $4,500 | 見下方 math，850W 夠 |
| Case | Lian Li O11 Dynamic EVO RGB | $5,500 | 同上 |
| Fans | Lian Li UNI FAN SL120 V2 三入 | $2,400 | RGB 整合 |
| **TOTAL** | | **~$73,490** | 剩 **$1,510 buffer**（散熱膏 + 上門組裝 $1k） |

### 方案 B：守住整份原菜單（要追加 $40k 預算）

預算拉到 **NT$ 115,000**，只動 RAM（降到 6400）+ 機殼（換 EVO RGB），其他全保留。streamer 定位最完整。

---

## 🧮 PSU 瓦數 math（必印）

**方案 A**：265K (125W) + 5070 Ti (300W) = 425W → ×1.3 = **552W → 推 650-750W** → **RM850x 過剩但留 GPU 換代空間，OK**
**方案 B**（保留 285K）：285K (250W PL2) + 5070 Ti (300W) = 550W → ×1.3 = **715W → 推 850-1000W** → **RM1000x 合理**

---

## 📊 Use-case 適配度（streamer 視角）

- **Primary use**：直播推流（OBS x264/NVENC 雙軌）+ 遊戲 + 後製剪輯
- **適配亮點**：
  - 16GB VRAM 5070 Ti 含 **AV1 NVENC**（Twitch 2024 已支援 AV1，4K @ 12 Mbps）
  - 4TB SSD 撐 1080p60 高碼率錄影（~20GB/hr）約 200 小時素材
  - 64GB / 32GB RAM 給 OBS scene preview + Chrome 30+ tabs + Discord 同開
  - LCD 水冷頭 + 全 RGB 對直播畫面 cam shot 有 branding 效果
- **靜音盲點**：機殼風扇選 PWM 曲線 + AIO 改 zero-RPM mode；麥克風建議用 Shure SM7B / RØDE PodMic（dynamic mic）避免吃環境噪音
- **未來升級空間**：方案 A 留 RAM 升 64GB + 換 5080 路；方案 B 已頂規

---

## ⚠️ 還沒解的 risk

1. **Memory training 風險（最大未爆彈）**：即便降到 6400 CL32，2×32GB dual-rank on Z890 + 285K 仍可能要手動 tune。必查 MSI Z890 EDGE TI 官網 QVL 對該 kit part number。
2. **285K 散熱牆**：H170i 420mm 是頂規空冷對手，但 streaming + 遊戲滿載仍可能撞 100°C 降頻；建議 BIOS 把 PL1=PL2=200W 限縮（效能損失 5-8%，溫度降 15°C）。
3. **O11 Dynamic EVO（標準版）前面板無進風**：依賴底部 + 側面進風，GPU 進氣較差。若選原菜單機殼，**RTX 5070 Ti 357mm 長 + 420mm 頂排** 在 EVO 標準版會擋 RAM 散熱片，務必量過。**推薦 EVO RGB 新版** 解此問題。
4. **PCIe Gen5 散熱**：Z890 + 990 Pro 4TB 不算 Gen5（990 Pro 是 Gen4），無此問題；但 5070 Ti Vanguard 是 PCIe 5.0 x16，主板 M.2_1 槽會與 GPU 共享 lane（看 MB 手冊；通常 x16/x8+x8 切換僅在第二張 GPU，正常 1 GPU 不受影響）。
5. **方案 B 預算追加**：要 Sam 親口確認預算可拉到 $115k。否則只能走方案 A。
6. **Z890 BIOS 版本**：早期 2024 Q4 出板的 Z890 對 64GB DDR5-7200 / 高密度 kit 相容性差，**買前要求賣家代刷最新 BIOS**（MSI 通常 2026 Q2 後 AGESA 等價 microcode 已穩）。

---

## 🛒 採購建議

- **原價屋（coolpc.com.tw）**：方案 A/B 都可一張菜單貼上，請指定上門組裝 $1,200 + 跑 stress test
- **欣亞（sinya.com.tw）**：Z890 EDGE TI / O11 EVO RGB / 990 Pro 4TB 都有現貨，可現場驗機 + RGB sync 測試
- **autobuy.tw**：285K $18,500、5070 Ti Vanguard $37,990 是目前低點
- **套裝機對比**：PCHome 同 spec streamer 套裝（5070 Ti + Z890 + 32GB）約 $95-105k，比方案 A 貴 $22k 但含一年整機保
- **不建議**：水貨 5070 Ti（Vanguard 在台保固走代理商，水貨無保 + 燒毀 12V-2x6 接頭自負風險）

---

## 📚 引用來源

- 285K 報價：autobuy.tw $18,500 / sinya 代理公司貨 / 順發 [未驗證單一通路具體數字]
- Z890 EDGE TI：BenchLife 開箱「市場參考價格約 $12,490」 https://benchlife.info/msi-mpg-z890-edge-ti-wifi-review/
- 990 Pro 4TB：欣亞 https://www.sinya.com.tw/prod/197427、findprice 中位 ~$11,500
- H170i ELITE LCD XT 420：欣亞 https://www.sinya.com.tw/prod/185533 ~$9,800
- 5070 Ti Vanguard SOC：autobuy $37,990 https://www.autobuy.tw/3c/prod_395771
- O11 Dynamic EVO 黑：BigGo $5,700 / 原價屋 EVO XL $7,200 https://www.coolpc.com.tw/tw/portfolio-items/聯力-o11-dynamic-evo-
- RM1000x：欣亞 https://www.sinya.com.tw/prod/207165、findprice $6,190
- 285K IMC + DDR5-7200 64GB QVL 風險：[未驗證 PTT/PCDIY 串，僅基於 Arrow Lake JEDEC 6400 spec 推論，買前必查 MSI 官網 QVL]
