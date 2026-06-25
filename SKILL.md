---
name: pc-build-audit-tw
description: Use when Sam (or任何 user) 傳台灣 PC 菜單 (image 截圖 or text)—通常從原價屋 / 欣亞 / autobuy / PCHome—要做 CP 值 audit、抓相容性 bug、對 2026 市場行情驗價、產出 use-case-tuned 推薦。輸出繁中 final spec table + 預算拆解 + reasoning。
type: procedural
---

# PC Build Audit (Taiwan)

繁中 audit 流程，給 Sam 或任何使用者貼台灣菜單時，產出 CP 值最佳 + 無相容性陷阱 + 對 2026 真實行情的 build 建議。

## 1. 觸發場景

- Sam 傳 PC 菜單圖（原價屋報價單、欣亞 / autobuy 購物車截圖）
- Text：「幫我看這台 build」「這菜單 ok 嗎」「升級 X 划算嗎」
- 任何含 CPU / MB / RAM / SSD / GPU / PSU / Case 清單的 input
- 套裝機詢價（PCHome 24h、momo），要對比自組

## 2. 5-step audit algorithm

### Step 1 — Parse parts list

從 image 用 vision parse 出每行 component：CPU / MB / RAM / SSD / Cooler / GPU / Case / PSU / Display / Peripherals。

Internal JSON：
```json
{
  "cpu": {"brand":"AMD|Intel", "model":"...", "socket":"AM5|AM4|LGA1700|LGA1851", "tdp":105, "price":7990},
  "mb":  {"brand":"...", "model":"...", "chipset":"B650|B760|...", "socket":"...", "ram_type":"DDR4|DDR5", "form_factor":"ATX|mATX|ITX|E-ATX", "m2_slots":2, "price":4990},
  "ram": {"gen":"DDR4|DDR5", "capacity_gb":32, "speed":6000, "price":3290},
  "ssd": {"model":"...", "interface":"PCIe Gen4|Gen5|SATA", "capacity_tb":1, "price":2390},
  "gpu": {"model":"...", "vram_gb":12, "tdp":250, "connector":"8pin|12V-2x6|12VHPWR", "price":17990},
  "psu": {"watt":750, "rating":"80+ Gold", "cable":"ATX 3.0|3.1", "price":2990},
  "case":{"form_factor":"ATX|mATX|ITX|E-ATX", "price":1990},
  "cooler":{"type":"air|AIO", "tdp_support":220, "price":1290}
}
```

不確定的欄位寫 `null`，Step 3 用 Brave 補。

### Step 2 — Compatibility validation（BLOCKER level）

#### CPU socket → chipset 矩陣

| Platform | Socket | 相容 chipset |
|---|---|---|
| AMD Ryzen 7000/8000/9000 | AM5 | A620 / B650 / B650E / B850 / X670 / X670E / X870 / X870E |
| AMD Ryzen 1000-5000 | AM4 | A320 / B450 / B550 / X470 / X570 |
| Intel Gen 12/13/14 | LGA 1700 | H610 / B660 / B760 / H670 / Z690 / Z790 |
| Intel Core Ultra 200 (Arrow Lake) | LGA 1851 | B860 / H810 / Z890 |

**Mismatch → 🚨 BLOCKER**，立刻在輸出最上方提示，給兩條 fix path：
- Path A：換 CPU（同 socket 等級替代）
- Path B：換 MB（同 CPU socket 的合理 chipset）

實際案例參考（Sam 2026-06-19 真實遇到）：R5 7500F（AM5）配 B760M（LGA 1700）→ 完全不能用，PTT PC_Shopping 看版半年至少出現 3 次。

#### RAM gen check

- AM5：**DDR5 only**
- AM4：**DDR4 only**
- LGA 1700：DDR4 或 DDR5（看 MB 型號最末，如 `B760M-A D4` 才是 DDR4）
- LGA 1851：**DDR5 only**

#### PSU 瓦數（math line 必須印在 audit 報告裡）

```
required_watt = CPU TDP + GPU TDP + 30% headroom
例：9700X (65W) + RTX 5070 Ti (300W) = 365W → ×1.3 = 475W → 推 550W~650W
例：9800X3D (120W) + RTX 5080 (360W) = 480W → ×1.3 = 624W → 推 750W~850W
```

每份 audit 報告**必須**有這一行 math，不准只丟「建議 750W」沒解釋。

PSU 80+ Gold 起跳；RTX 4070 Ti Super 以上必須 ATX 3.0 / 3.1（原生 12V-2x6），不要用轉接頭。

#### Case form factor

- ATX 機殼吃 ATX / mATX / ITX MB
- mATX 機殼吃 mATX / ITX
- ITX 機殼**只**吃 ITX
- E-ATX 要 full tower（部分 ATX 機殼擋線材槽）

#### BIOS update 需求（AM5 / LGA1851 必檢查）

- **AM5 新 CPU（Ryzen 9000 系列 / X3D）裝舊 B650 / X670 板**：通常需先刷 BIOS 到 AGESA 1.2.0.2+ 才能開機。賣場板若沒貼「Ryzen 9000 Ready」標籤，要警告用戶：
  - Path A：請賣家**先代刷 BIOS** 再出貨（原價屋 / 欣亞 通常免費）
  - Path B：選有 **BIOS FlashBack 按鈕**的板（不用 CPU 就能刷，e.g., ASUS TUF B650-PLUS、MSI Tomahawk）
  - Path C：升 B850 / X870 新板（原生支援 Ryzen 9000）
- **Intel Core Ultra 200（Arrow Lake）裝早期 Z890**：同理，2025 早出板要查 BIOS 版本。

#### RAM QVL（高速 DDR5 必查）

- DDR5-6400 以上 kit（especially LGA1700/1851 平台 7200+、AM5 6400+）必須查 MB 廠的 **QVL (Qualified Vendor List)**。
- 不在 QVL 上的 kit 跑得起來只是運氣，常見症狀：開機 memory training 卡 30 秒、無法開 EXPO/XMP、藍屏。
- 查 QVL：MB 廠官網 → support → memory support list → 比對 RAM 型號 part number（不只 brand + 容量 + 速度）。
- 不確定 → 建議降到 AM5 **DDR5-6000 CL30** 甜蜜點（幾乎所有 AM5 板 QVL 都有），LGA1700/1851 走 **DDR5-6400 CL32**。

#### Cooler TDP

塔散 / AIO 散熱規格 TDP 必須 ≥ CPU 標稱 TDP。Intel K 後綴 / AMD X3D 建議 240mm AIO 以上。

### Step 3 — Price 驗證 against 2026 TW spot market

> ⚠️ **CRITICAL — Sam 2026-06-25 教訓**: 抓網路上的「Coolpc 商品介紹頁」(`coolpc.com.tw/tw/shop/...` 或 `coolpc.com.tw/tw/portfolio-items/...`) **常常是 2021-2023 的 marketing copy**,內含的「促銷價 $X,XXX」是當年活動價,**不是今日 spot price**。 直接信會慘 (我幹過,Sam 抓包)。

#### 3a. Live shopping site 才有 spot price

對每個 component,**先跑這 4 個 live 比價站**(它們會 scrape 多通路 + 顯示今日成交):

```
site:biggo.com.tw <part name>            # BigGo 多通路比價,有歷史曲線
site:feebee.com.tw <part name>           # 飛比價格,蝦皮 / PChome / momo 集中
site:24h.pchome.com.tw <part name>       # PChome 24h spot
site:m.momoshop.com.tw <part name>       # momo spot
```

**只有 BigGo / 飛比 / PChome / momo 的價可以當 spot price 引用**。 其他都當「baseline 估算」要明寫。

#### 3b. 通路抓 spot (sinya / coolpc / autobuy)

要看大型通路 spot,只信這幾個頁面:

```
site:sinya.com.tw/prod/<id>              # 欣亞單品頁有當日價
site:coolpc.com.tw/evaluate.php          # 原價屋線上估價單(只有這個頁面是 today)
site:autobuy.tw/3c/prod_<id>             # autobuy 單品頁
```

**禁止當 spot 用**:
- `coolpc.com.tw/tw/shop/dram/...` 或 `coolpc.com.tw/tw/portfolio-items/...` (商品介紹文,常含舊文案)
- 商品 spec 介紹頁(沒「立即購買」按鈕的那種)
- 任何 dateline 看不到的價格快照

#### 3c. 跨 spot vs baseline 嚴格分流

每個 component 都跑兩張表,**不能混**:

**Spot 表** (引用 BigGo / 飛比 / PChome / momo / sinya 單品頁 / autobuy 單品頁 / coolpc 估價單):

| 通路 | URL | 今日價 | 抓取日期 |
|---|---|---|---|
| PChome 24h | https://24h.pchome.com.tw/prod/... | $X,XXX | 2026-MM-DD |
| momo | https://m.momoshop.com.tw/... | $X,XXX | 2026-MM-DD |
| BigGo (多通路均) | https://biggo.com.tw/s/... | $X,XXX | 2026-MM-DD |

**Baseline 估算表**(用 TrendForce / 報紙 / 4Gamers 報導當參考):

| Source | 文章日期 | 推估區間 |
|---|---|---|
| TrendForce / DRAM Spot | YYYY-MM | $X,XXX-X,XXX |
| 4Gamers / Cool3c 報導 | YYYY-MM | $X,XXX-X,XXX |

最後**中位數只算 spot 表的**(min 2 個有效通路才算),baseline 只用來做「合理性 sanity check」。

#### 3d. 倍率判定

- 倍率 = 賣家報價 / spot 中位數
- > 1.25× → ⚠️ 偏高
- > 1.5× → 🚨 嚴重虛標
- < 0.85× → 注意水貨 / 平輸 / 缺保固
- spot 表 < 2 個通路 → 標 **「N/A — spot 不足以判定」**,不假裝有答案

#### 3e. 大局 sanity check —— 2026 Q2-Q3 必須知道的市況

**先跑 2 個查詢確認大局,再評個別零件**:

```
site:trendforce.com.tw <component>       # 大趨勢
site:technews.tw <component> 漲價         # 新聞報導
"<component> PTT 漲價" OR "PCDIY 漲價"     # 看版近一個月
```

**2026 Q2-Q3 已知事實 (Sam 2026-06-25 case 學到)** — 用 search 確認最新版本後寫進報告:

- 🚨 **DDR5 32GB 32x2 飆破萬元** (金士頓 FURY Beast 32GB DDR5-5600 從 2025-10 NT$2,500 → 2026-04~06 NT$14,000,5x 漲幅)
- 🚨 **DDR4 反而比 DDR5 便宜** (DDR4 32GB PChome 還有 $2,059-3,099),AMD 推 5800X3D 10 週年紀念版正是給「不想踩 DDR5 萬元」的人
- 🚨 **SSD HBM 紅利仍在**: 1TB Gen4 NVMe ~$2,200-2,800,但 2TB+ Gen4 / Gen5 也跟著漲
- ✅ **GPU**: 30 系列已停產,新案 RTX 50 主流。 5060 Ti 16GB budget LLM 甜蜜點,5070 Ti / 5080 主流 gaming
- ⚠️ **大局短期沒緩解**: AI/HBM 排擠 DRAM 產能 + 原廠控產,2026 Q3-Q4 預期繼續漲

**這些事實 ≠ 全部** — 每次 audit 還是要跑 trendforce / technews search 確認最新版本。 大局每 1-2 個月會更新。

#### 3f. 引用規範 (hard rule)

- 講「PCDIY / PTT 說 XXX」必須附**具體 thread URL**(或 PTT post ID):
  - `https://forum.gamer.com.tw/C.php?bsn=60030&snA=<thread_id>` (巴哈 PCDIY 串)
  - PTT: `ptt.cc/bbs/PC_Shopping/M.<timestamp>.A.XXX.html` 或 `#1cXxXxXx (PC_Shopping)` post ID
- 講「通路價 $X」必須附**具體單品 URL** (見 3b 的禁止清單,Coolpc 商品介紹文不算)
- 沒辦法附 → 寫「[未驗證 — 待 spot 查證]」,不要假稱「PCDIY 實測」或「Coolpc 標 $X」

#### 🟡 CALLOUT (每份 audit 都必須寫進報告)

> **2026 Q2-Q3 RAM HBM 紅利期 baseline**: 因 HBM3e + AI 訓練卡需求佔走 DRAM 產能,**DDR5 32GB 多數品牌已飆破萬元,DDR4 反而比 DDR5 便宜**(產線砍 → 供需局面意外 = DDR4 缺貨高位 PChome 仍有 $2-3k 區間)。 1TB Gen4 NVMe ~$2,200-2,800 合理,GPU 以 RTX 50 系列為主流。 **AMD 5800X3D 10 週年復刻版 2026-06-25 上市 (NT$11,790),AMD 自定義為「DDR5 漲價救命包」**。 ← 每次 audit 前先 search 確認此 callout 是否需要更新 (大局每 1-2 個月會動)。

### Step 4 — Use-case fit

不確定先問。常見 use case：

| Use case | 重點 spec |
|---|---|
| Gaming-only 1080p / 1440p | 主推 FPS；GPU 8-12GB VRAM；CPU 6-8 核夠用 |
| AI / LLM dev | **VRAM ≥ 16GB**（Llama 3.1 8B Q4 起跳）；RAM 32GB+；多核 CPU；NVMe Gen4+ 1TB+ |
| Content creator (Premiere / DaVinci) | VRAM ≥ 16GB；RAM 64GB；快速 NVMe；CPU 多核 |
| Data engineering | 多核 CPU（Ryzen 7700+ / i7+）；RAM 32-64GB；NVMe Gen4+；GPU 可選 |
| 3D render (Blender / Unreal) | 高 VRAM + CUDA cores（NVIDIA 偏好）；CPU 多核 |
| Family / office | 內顯（780M / iGPU）可；SSD 500GB+；RAM 16GB |
| 無獨顯預算 build / 待升級 | **Ryzen 5 7600 / 7700 + 內建 Radeon 780M**：1080p Low-Medium 玩主流遊戲可用，先省 GPU 預算等之後加裝（AM5 平台保留升級路），比 Intel F 後綴（無內顯）安全 |
| Streamer | NVENC GPU；多核 CPU（OBS encoding）；RAM 32GB |

Spec mismatch → 直接 upgrade 對應零件（e.g., 「AI dev」但 GPU 5060 Ti 8GB → 升 5060 Ti 16GB）。

### Step 5 — Generate final spec table

繁中 + 表格 + 為何選 reasoning + buffer 提示。Sam style：短句、直接、不寒暄。

## 3. Knowledge sources（什麼情況查哪個）

| 情境 | Source |
|---|---|
| 專有名詞 / 縮寫 / 行話（套水、ESS、12V-2x6、PBO、EXPO） | **巴哈姆特 PCDIY (ba.com.tw)** + **PTT PC_Shopping** |
| 即時行情 / 折扣 / 限時殺 | **原價屋 coolpc.com.tw**、**欣亞 sinya.com.tw**、**autobuy.tw** |
| 套裝機定價 benchmark（對比自組省多少） | **PCHome 24h**、**momo 購物** |
| 國外行情對照（Reddit / Tom's Hardware） | r/buildapc, r/Amd, r/intel, Tom's Hardware, TechPowerUp |
| 真實 benchmark（gaming FPS, render time） | TechPowerUp, Gamers Nexus, **巴哈 PCDIY 實測串** |
| 二手 / 撿便宜 | PTT PC_Shopping「買賣」、蝦皮、巴哈 PCDIY 交易區（自負風險） |

## 4. Hard rules（不可違反）

1. **CPU-MB 不相容 = BLOCKER**，先講再說後面。Sam 真實案例 2026-06-19 R5 7500F（AM5）+ B760M（LGA1700）。
2. **必查 2026 TODAY spot price,不准用過時 reference 價格**:
   - **2026-06-19 教訓**: 被 Sam 親口糾正過 (SSD/RAM HBM 漲價 baseline)
   - **2026-06-25 教訓**: 我抓了 Coolpc 商品介紹頁的 2021-2023 marketing copy 當 spot price,推薦給 Sam 結果完全錯方向。 **禁止信 `coolpc.com.tw/tw/shop/...` 或 `/portfolio-items/...` 介紹文價格** (見 Step 3a-3b)
   - **每次** audit 都要 trendforce / technews 跑大局 query (DDR5 萬元化 / DDR4 反便宜 / GPU stop 等)
   - 內部 baseline 認知過期 1-2 個月就會錯
3. **use case 不確定先問**。假設錯會推 8GB VRAM 給 LLM dev 就慘。
4. **推薦永遠帶「為何」**，不單列 spec —Sam 要看 reasoning 才能 push back。
5. **buffer 留 budget 5-10%** for 上門組裝（原價屋 $800-1500）、散熱膏、機殼風扇、滑鼠、Wi-Fi 天線、雜項。
6. **不要 fabricate part 規格**（socket / TDP / VRAM）。不確定 → Brave search 驗，失敗 → 跟用戶說「待查」，不要編造。
7. **PSU = CPU TDP + GPU TDP + 30% headroom**，strict，不投機。
8. **GPU 12V-2x6 / 12VHPWR**：RTX 40+ 系列才有。RTX 4090 燒接頭事件後，新 PSU 一律 ATX 3.0 / 3.1 原生線。

## 5. Common edge cases / 已知坑

- **chipset 命名易混**：B760 是 Intel；X670 是 AMD；B650 是 AMD；B860 是 Intel LGA1851 新世代。光看開頭字母不能判斷。
- **MB 型號末綴 D4 / D5**：`B760M-A D4` = DDR4 版；`B760M-A` = DDR5 版。買錯 RAM 全廢。
- **Cooler TDP 一定要對得上 CPU TDP**：散熱不夠長期降頻，不是裝起來能開就 ok。
- **mATX MB 可裝 ATX 機殼，反之不行**。ITX 機殼**只能**裝 ITX MB。
- **DDR5 profile**：AMD 叫 **EXPO**、Intel 叫 **XMP**。菜單常寫錯，買 RAM 看是否兩種 profile 都支援。
- **套裝機 SKU 隱藏**：PCHome / momo 套裝機 MB 寫「B760M」可能是 `B760M-K` / `B760M-A` 等低階 SKU，2-3 條 SATA、無 Wi-Fi、無第二 M.2。要點開賣場詳細 spec。
- **12V-2x6 vs 12VHPWR**：RTX 4090 燒接頭事件後規範，PSU 要 ATX 3.0 / 3.1 原生線，不要用轉 4×8pin 轉接頭。
- **記憶體頻率上限**：AM5 甜蜜點 DDR5-6000 CL30（EXPO）；LGA1700 DDR5-6400 起跳；超過 MB 規格會跑不起來 / 不穩。
- **NVMe Gen5 散熱**：Gen5 SSD 發熱大，MB 自帶散熱片 or 加裝，否則降速。
- **GPU 長度 vs 機殼**：5070 Ti / 5080 / 5090 普遍 320-360mm，小機殼塞不下，買前對長度。
- **PSU 線長**：背線機殼 + 大塔 PSU 24pin 線材長度要 ≥ 600mm，否則拉不過去。

## 6. Output template（繁中，可直接複製給用戶）

```markdown
## 🚨 必修 BLOCKER（若有）

- [描述問題]
- Fix path A：[替代方案 1]
- Fix path B：[替代方案 2]

## 💰 [預算 $XX,XXX] 內 final spec

| 項目 | 推薦 | 價格 | 為何選 |
|---|---|---|---|
| CPU | AMD Ryzen 7 9700X | $X,XXX | 8 核 16 緒、AM5 平台、TDP 65W 散熱壓力小 |
| MB | ASUS TUF B650-PLUS WiFi | $X,XXX | B650 chipset、ATX、DDR5、Wi-Fi 6E、5 年保固 |
| RAM | Kingston FURY Beast DDR5-6000 32GB (16×2) | $X,XXX | AM5 甜蜜點 6000 CL30 EXPO、雙通道 |
| SSD | WD Black SN850X 1TB Gen4 | $X,XXX | Gen4 7300 MB/s、含散熱片、5 年保 |
| GPU | NVIDIA RTX 5070 Ti 16GB | $XX,XXX | 16GB VRAM 撐得住 AI inference + 1440p 高畫質 |
| PSU | Corsair RM850x ATX 3.1 | $X,XXX | 850W = 65W + 285W + 30% buffer；原生 12V-2x6 |
| Case | Fractal Design Pop Air ATX | $X,XXX | ATX、3×120mm 風扇預裝、走線 OK |
| Cooler | Thermalright Phantom Spirit 120 | $X,XXX | 雙塔、TDP 245W、壓 9700X 綽綽有餘 |
| **TOTAL** | | **$XX,XXX** | （剩 $X,XXX buffer，可加組裝費 / 散熱膏 / Wi-Fi 天線） |

## 📊 Use-case 適配度

- Primary use：[gaming / AI dev / content / data eng / 3D / office / stream]
- 適配亮點：[列 2-3 點 spec 對應 use case 的設計]
- 未來升級空間：[RAM 升 64GB / 第二顆 SSD / 換 5080]

## ⚠️ 還沒解的 risk

- [若有] e.g., 機殼風扇位置可能擋 GPU 第三槽
- [若有] e.g., PSU 線長要再確認背線 600mm

## 🛒 採購建議

- **原價屋（coolpc.com.tw）**：菜單貼上自選，可指定上門組裝（$800-1500）
- **欣亞（sinya.com.tw）**：實體店面，可現場驗機
- **autobuy.tw**：促銷檔常有殺
- **套裝機對比**：PCHome 24h / momo 同 spec 套裝約 $XX,XXX，貴 $X-X,XXX 但有整機保固
- 自組省 $1-2k 但要會排線 + 跑 stress test
```

## 7. 執行 checklist（每次 audit 前自我檢查）

- [ ] Parts list parse 完，每個 component 都有 model 字串
- [ ] CPU socket vs MB chipset 對過矩陣
- [ ] RAM gen vs MB 支援對過
- [ ] PSU watt ≥ CPU TDP + GPU TDP + 30%
- [ ] Case form factor 容得下 MB + GPU 長度
- [ ] Cooler TDP ≥ CPU TDP
- [ ] 每個 component 跑過 spot 驗價:**BigGo + 飛比 + PChome + momo** 4 站,不只看 Coolpc/sinya/autobuy
- [ ] **沒抓 Coolpc 商品介紹頁 (`/shop/` 或 `/portfolio-items/`) 當 spot price** — 那些是 2021-2023 marketing copy
- [ ] 跑過 trendforce / technews 確認 2026 大局 (DDR5 漲價 / DDR4 反便宜 / GPU 等)
- [ ] 巴哈 PCDIY / PTT PC_Shopping 查過近期討論
- [ ] Use case 確認過或主動問
- [ ] Buffer 留 5-10%
- [ ] 不確定的規格寫「待查」，不編造
- [ ] PSU math line（CPU TDP + GPU TDP + 30%）有印出來
- [ ] 2026 SSD/RAM HBM CALLOUT 有寫進報告
- [ ] AM5 新 CPU 配舊板 → BIOS update 警告有講
- [ ] 高速 DDR5 kit → QVL 提醒有講
- [ ] 引用 PCDIY/PTT 有附具體連結或 post ID，不寫「PCDIY 實測」這種無 source 句
