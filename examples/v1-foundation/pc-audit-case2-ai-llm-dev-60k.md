# PC 菜單 Audit — case2-ai-llm-dev-60k

> Persona: 30 歲 senior data eng / Llama 3.1 8B local + dbt-core + Jupyter / 8 月 portfolio build
> Budget: NT$ 60,000
> 日期: 2026-06-19 (TW 行情)

---

## 🚨 必修 BLOCKER

### BLOCKER 1：原菜單總價已 **嚴重超預算**（估 NT$76,000–82,000，超 25–37%）

主因是 2026 Q2–Q3 NAND/HBM 大缺貨，**Samsung 990 Pro 2TB 在台已飆到 NT$18,000+**（去年同期 ~NT$8,300，漲 2 倍以上）。RAM 64GB 也比歷史價漲 30–50%。原菜單沒對到當下行情。

原菜單估價（2026-06-19 行情）：

| 項目 | 原選 | 估價 | 來源 |
|---|---|---|---|
| Intel Core Ultra 7 265K | LGA1851 | **9,300–11,225** | BenchLife 2026 調降後價、原價屋 |
| ASUS PRIME B860M-K | B860 mATX | **3,690** | 原價屋 |
| Kingston Fury Beast DDR5-6000 64GB (2×32) | KF560C40BBK2-64 | **7,688–8,888** | 原價屋活動 |
| Samsung 990 Pro 2TB | Gen4 | **18,353**（PChome）/ 18,000+ 各通路 | PChome 24h / 飛比 |
| Noctua NH-D15 | 雙塔風冷 | **3,615** | 原價屋 |
| MSI RTX 5070 Ti 16G Ventus 3X OC | GDDR7 16GB | **28,000–32,000** | TW 通路（MSRP $2699 漲價中）|
| Fractal Design Pop Mini Air RGB | mATX | **3,190** | 原價屋 |
| Corsair RM850e | 850W Gold ATX 3.1 | **3,890** | 原價屋 |
| **TOTAL** | | **~77,700–94,851** | 嚴重爆預算 |

**Fix path**：見下方 60k final spec（必要刪 / 換的件已標 ⚠️）。

### BLOCKER 2：265K + B860M-K 是 **奢侈晶片配廢板**的錯配

- 265K 是 K 後綴解鎖版（125W TDP / PL2 ~250W），**B 系列晶片組根本不允許 CPU OC**，只能 OC 記憶體 → 多花的 K 費用 100% 浪費。
- B860M-K 是 ASUS PRIME 最入門 SKU（**單 8-pin EPS、無 Wi-Fi、VRM 散熱片陽春、僅 1× M.2、無第二 PCIe 5.0 x16**），對 265K 那種 250W 峰值會 VRM 過熱降頻，長 dbt 跑批或 fine-tune 持續高負載會 throttle。
- 對 LLM dev / Jupyter / dbt 來說 CPU 不是熱點（GPU 才是），上 K-SKU 沒意義。

**Fix path A（推薦）**：CPU 換 **Core Ultra 7 265**（非 K，TDP 65W，省 ~NT$2,000 且 NH-D15 壓力大降），MB 同 B860M-K 還能撐。
**Fix path B**：保留 265K，MB 升 **B860M-PLUS / TUF B860M-PLUS WiFi**（~NT$5,000–5,500），但這條會更貴。

對 60k 預算 + LLM dev，**Path A 是正解**。

---

## 💰 NT$60,000 內 final spec（重排版）

| 項目 | 推薦 | 預估價 | 為何選 |
|---|---|---|---|
| CPU | **Intel Core Ultra 7 265** (非 K) | **8,800** | LGA1851 20 核（8P+12E）/ TDP 65W、PL2 ~182W；data eng dbt-core 多執行緒夠；省熱量、NH-D15 輕鬆壓 |
| MB | ASUS PRIME B860M-K | **3,690** | 同原選；265 非 K 沒 VRM 壓力，B860M-K 撐得起。**缺點：無 Wi-Fi**（用網路線或加 USB Wi-Fi $300） |
| RAM | Kingston Fury Beast DDR5-6000 64GB (2×32) CL36 | **7,688**（原價屋限量 $7,688，否則 $8,888）| 64GB 為 Llama 8B Q4/Q8 load + Jupyter notebook + dbt cache 提供足夠 headroom；DDR5-6000 是 LGA1851 甜蜜點 |
| SSD | ⚠️ **改 WD Black SN850X 2TB**（含散熱片）或 **Crucial T500 2TB** | **8,500–9,500** | 990 Pro 2TB 在 2026 漲到 NT$18k+ 是「現在不買」標的；SN850X 2TB Gen4 7300MB/s 同等性能、TW 通路 ~$9,000，省一萬 |
| GPU | MSI RTX 5070 Ti 16G Ventus 3X OC | **28,990** | **16GB VRAM 是 Llama 3.1 8B 跑 Q8/FP16 + 留 KV cache headroom 的下限**；Blackwell FP4 / CUDA 12.8 對 vLLM / llama.cpp / Ollama 都有加速；NVENC 也順便有 |
| PSU | Corsair RM850e ATX 3.1 | **3,890** | 265 TDP 65W + 5070 Ti TDP 300W + 30% buffer = ~475W，850W 過剩但留升級空間（未來換 5080）；ATX 3.1 原生 12V-2x6 對 5070 Ti 安全 |
| Cooler | ⚠️ **改 Thermalright Phantom Spirit 120 EVO** | **1,290** | NH-D15 對 265 非 K 過剩；PS120 雙塔壓 65W TDP 綽綽有餘，省 NT$2,300。**若堅持 NH-D15 → 必加 LGA1851 offset mount NM-IMB8** |
| Case | Fractal Design Pop Mini Air RGB | **3,190** | mATX 配 B860M-K 剛好；顯卡長度 365mm 容得下 5070 Ti Ventus 3X（~330mm）；U 高 170mm 容得下 PS120 / NH-D15 |
| **TOTAL** | | **~66,028** | 仍略超 60k；下面有「真正壓 60k」方案 |

### 真正壓進 NT$60,000 的方案（必砍項）

如果是硬卡 60k，要再做這幾刀（任選組合）：

| 替代 | 省多少 | 取捨 |
|---|---|---|
| RAM 64GB → **32GB DDR5-6000**（2×16） | ~4,500 | Llama 8B 在 GPU VRAM 跑，CPU RAM 32GB 對 dbt + Jupyter 已夠；未來再加 32GB 升 64GB |
| SSD 2TB → **1TB Gen4**（SN850X / T500 1TB） | ~4,000 | 1TB 對 dataset cache 緊；建議「先 1TB，撐到 2027 NAND 降價再加裝第二顆」 |
| PSU 850W → **750W**（RM750e） | ~400 | 5070 Ti + 265 真實耗電 ~480W，750W 夠；但未來升 5080 就不夠 |
| GPU 5070 Ti → **5070 12GB** | ~5,000 | ⚠️ 對 LLM dev 是 **退路**：12GB VRAM 跑 Llama 8B FP16 會 OOM，只能跑 Q4/Q6；portfolio 用真的有限制 |

**推薦砍法**：RAM 降 32GB（−4,500）+ SSD 降 1TB（−4,000）→ TOTAL **~57,528**，留 ~2,500 給組裝費 / Wi-Fi USB dongle / 散熱膏。**GPU 16GB 不要砍**，這是這 build 的命根子。

#### 最終 60k 內推薦定版

| 項目 | 型號 | 價格 |
|---|---|---|
| CPU | Intel Core Ultra 7 265 (非 K) | 8,800 |
| MB | ASUS PRIME B860M-K | 3,690 |
| RAM | Kingston Fury Beast DDR5-6000 **32GB (2×16)** | 3,200 |
| SSD | WD Black SN850X **1TB** (Gen4 含散熱片) | 4,500 |
| GPU | MSI RTX 5070 Ti 16G Ventus 3X OC | 28,990 |
| PSU | Corsair RM850e ATX 3.1 | 3,890 |
| Cooler | Thermalright Phantom Spirit 120 EVO | 1,290 |
| Case | Fractal Design Pop Mini Air RGB | 3,190 |
| **TOTAL** | | **~57,550** |
| Buffer | 組裝 $800 + 散熱膏 + USB Wi-Fi | ~2,500 |

---

## 📊 Use-case 適配度（LLM dev / data eng）

- **Primary use**: 本地 Llama 3.1 8B inference + LoRA fine-tune 嘗試 / dbt-core ETL / Jupyter notebook / 8 月 portfolio
- **適配亮點**：
  - **RTX 5070 Ti 16GB VRAM**：Llama 3.1 8B FP16 ~16GB、Q8 ~9GB、Q4 ~5GB，16GB 是「FP16 推理 + KV cache 8K context」可行下限；fine-tune 走 QLoRA 也 ok（不能 full fine-tune，那需 24GB+）
  - **20 核 (8P+12E) CPU**：dbt-core 平行 model build、pandas / polars groupby 多執行緒受惠
  - **64GB（或 32GB）DDR5**：Jupyter kernel 開大 dataset、duckdb in-memory query 不爆
  - **Gen4 NVMe**：parquet / arrow 讀寫 5GB/s+，dataset I/O 不卡
  - **NVENC**：portfolio demo 錄製 GPU 編碼不吃 CPU
- **未來升級空間**：
  - RAM slot 還 2 條空位 → 升 64GB / 128GB
  - 第二顆 M.2 PCIe 4.0（B860M-K 有 2 個 M.2 slot）→ 加 4TB cache disk
  - PSU 850W 容得下未來換 5080（360W TDP）
  - **不能升** CPU 到更高（265 / 265K 已是 LGA1851 高階段）

---

## ⚠️ 還沒解的 risk

1. **NAND 2026 行情持續飆**：SSD 2TB 可能 8 月還更貴，現在買 1TB 是被市場逼的次優選；若 portfolio 真的吃硬碟，先 1TB + 用外接 USB 4 NVMe 暫存
2. **B860M-K 無 Wi-Fi**：portfolio demo 場景若需移動，加買 TP-Link AXE5400 USB Wi-Fi（~NT$1,500）；或 build 時直接升 B860M-A WiFi（~NT$4,500，+800）
3. **5070 Ti TW 通路缺貨且漲價**：MSRP $2699 USD，但實價在 1000–1300 美元區間（XFastest 報導），TW 通路 NT$28k–33k 浮動；可能要等檔期或上原價屋蝦皮搶
4. **B860M-K 單 M.2 PCIe 5.0 沒散熱片**：建議 SSD 直接買「含散熱片版」，否則 Gen4 持續寫入會降速
5. **Llama 8B FP16 + 8K context** 在 16GB 邊緣（~15.5GB），若要拉到 32K context 要降到 Q8 / Q6；對 portfolio 跑 RAG demo 影響不大
6. **265 非 K 對 LLM inference 沒差**（GPU bound），但若 portfolio 想 show 「CPU-only Llama on AVX-512」會比 K 慢 ~10%

---

## 🛒 採購建議

| 通路 | 適合 | 註 |
|---|---|---|
| **原價屋 coolpc.com.tw** | 主菜單 + 上門組裝（$800–1,500）| 5070 Ti 用其蝦皮商城首賣搶 |
| **欣亞 sinya.com.tw** | 實體店面驗機 | 適合不熟組裝 / 怕點不亮跑保固 |
| **autobuy.tw** | 折扣檔追 SSD / RAM 殺價 | 卡 NAND 漲價檔，autobuy / momo 偶有 990 Pro 2TB 跌破 NT$15k 的限時 |
| **PChome 24h / momo** | 套裝機對比 | 同 spec 套裝機 ~NT$72k，貴 ~NT$12k 但整機保固，data eng 趕 deadline 可考慮（時間成本）|
| **Reddit r/LocalLLaMA / 巴哈 PCDIY** | 確認 Llama 8B 真實 throughput | 開 build 前查 5070 Ti + Ollama 跑 8B Q8 的 tok/s benchmark |

**買的時序**：
1. 6 月底前先卡 **5070 Ti**（最大漲價風險件）
2. 7 月初看 SSD 行情，等檔期下手 SN850X
3. 7 月中拼一波組裝 → 8 月 portfolio 上線
