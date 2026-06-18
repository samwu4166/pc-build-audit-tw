# 🚨 必修 BLOCKER

這份菜單有 **3 個會直接燒掉預算或開不了機的問題**，買之前一定要解。

## BLOCKER 1：Tesla M40 是「**被動散熱 + EPS 8pin 供電**」的伺服器卡，不能直接塞桌機

- M40 原廠**沒有風扇**，靠機架伺服器的暴力風扇吹過散熱片。塞進 NX800 這種一般 ATX 機殼 → 10 分鐘內溫度衝到 90°C+ 開始 throttle，跑 LLM 推論長時間負載直接過熱降頻 / 掛掉。
- 供電是 **CPU EPS 8pin（4+4）**，不是顯卡 PCIe 8pin。兩者**接腳定義不同，直插會燒板**（PTT / 對岸論壇有實例）。
- Cooler Master MWE 750W Bronze 只有一條 EPS（給 CPU 用），給 M40 就沒得餵 CPU 了；要嘛買 PCIe→EPS 轉接線（注意極性），要嘛 PSU 要有第二條 EPS。

**Fix path A（推薦）**：
- 加購**渦輪暴力扇改裝套件**（淘寶 / 蝦皮「M40 散熱 涡轮 9cm L型」，$300-600）—— 強制風冷
- 加購 **PCIe 8pin → EPS 8pin 轉接線**（注意：要買「給 Tesla 卡用」的反向定義線，$150-300），或直接用主機板 CPU EPS 線分接
- 確認 PSU 至少能輸出兩條 EPS（既有 MWE 750W Bronze 只有 1 條 → 用轉接）

**Fix path B（最保險，但破預算）**：
- 換 RTX 3060 12GB 二手（$5,500-6,500，VRAM 少 12GB 但驅動現役、消費卡規格、即插即用）→ 走正路，少踩坑
- 24GB 對 7B Q4 / 13B Q4 inference 夠用，12GB 可跑 7B Q4 / Q5，差距沒想像中大

## BLOCKER 2：Cooler Master MWE 750W Bronze 不適合餵 M40 24GB（同時是 NVIDIA 計算卡）

- M40 TDP 250W（FP32 滿載），加上 5600 65W → 約 315W 峰值。PSU math：
  ```
  required_watt = 65 (5600) + 250 (M40) + 30% headroom
                = 315 × 1.3 = 410W → 推 550W+
  ```
  瓦數本身 750W 夠（綽綽有餘），但**問題在三點**：
  1. MWE Bronze 是 CM 入門等級，**+12V rail 穩定度與單路電流**對「持續 250W 高負載 LLM 推論」這種 server 級工況勉強（不是電競短瞬負載）
  2. **只有 1 條 EPS**，不夠同時餵 CPU + M40
  3. 已使用年資不明 → 電解電容老化會直接拖垮計算卡穩定度

**Fix path A**：頂多撐著用，但備 $1,800-2,500 預算隨時要換 80+ Gold 雙 EPS PSU（e.g., 全漢 HYDRO G PRO 750W、海韻 FOCUS GX-750）
**Fix path B**：直接換 → $25,000 預算就要重排

## BLOCKER 3：B550M Pro4 不一定支援 R5 5600 開機（BIOS 版本問題）

- B550M Pro4 **沒有 BIOS FlashBack 按鈕**（這板**沒這功能**，跟 ASRock 的 PG / Steel Legend 系列不同）
- 需要 **BIOS P2.30 以上**才支援 Ryzen 5000（5600 / 5600X 等）
- 2021 後出廠的板**通常**已更新到支援，但**蝦皮 / PChome 庫存板可能是老貨**

**Fix path A**：跟賣家明問「貼紙有沒有寫 Ryzen 5000 Ready / BIOS 已更新到 P2.30+」，沒回答的不買
**Fix path B**：請原價屋 / 欣亞代刷 BIOS（多帶一顆舊 3000 系列 CPU 過去，或請店家用測試平台代刷，通常免費）
**Fix path C**：改買 **ASRock B550M PG Riptide / Steel Legend**（有 BIOS FlashBack），或 MSI B550M MORTAR MAX WiFi

---

# 💰 NT$ 25,000 內 final spec（含 Fix）

## 🟡 2026 SSD / RAM HBM 紅利期 baseline

> 2026 因 HBM3e + AI 訓練卡需求佔走 NAND / DRAM 產能，SSD / DDR5 / DDR4 相對 2023 **+30~50%**。DDR4-3200 32GB kit 已從 $2,200 漲到 $3,200-3,500、Gen3 1TB NVMe ≈ $1,800-2,200。**這份 build 在 DDR4 + Gen3 SSD 已經是相對抗漲的選擇**，符合「洋垃圾 + 二手」省錢路線。

## 規格表

| 項目 | 推薦 | 價格 | 中位數驗證 | 為何選 |
|---|---|---|---|---|
| CPU | AMD Ryzen 5 5600（新，盒裝） | $3,200 | sinya $3,290 / coolpc $3,250 → 中位 $3,250 (1.00x) | AM4 末代甜蜜點，6C12T 跑 LLM data pipeline / tokenization 夠用；TDP 65W 散熱輕鬆。**但 AM4 是死路平台**，未來只能升到 5800X3D 上限 |
| MB | ASRock B550M Pro4 ⚠️ **必須驗 BIOS** | $2,800 | sinya $2,890 / coolpc $2,750 (1.00x) | B550 chipset 撐 PCIe 4.0 給 M40（雖然 M40 只跑 Gen3 x16）；mATX 可裝 NX800（NX800 是 E-ATX 機殼，吃 mATX 沒問題）。**注意**：沒 BIOS FlashBack，要驗版本 |
| RAM | Kingston FURY Beast DDR4-3200 32GB (16×2) | $3,200 | coolpc $3,099(蝦皮)~$3,299 / sinya $3,250 (0.99x) | LLM inference 用 RAM offload（M40 24GB 不夠跑 13B Q4 全載入時要分層）→ 32GB 必要；CL16，AM4 5600 IMC 跑 3200 穩 |
| SSD | **改推 WD SN580 1TB Gen4**（NM610 是 Gen3 DRAMless）| $2,000 | coolpc $1,990 / sinya $2,090 (1.00x) | NM610 Gen3 DRAMless 跑 LLM 模型權重載入（10GB+ 檔）會掉速；SN580 雖 DRAMless 但 HMB 設計、Gen4 3500MB/s 對 LLM cold load 體感差很多。差價只 $200 |
| Cooler | ID-Cooling SE-214-XT BASIC | $690 | coolpc $690 / momo $690 (1.00x) | TDP 180W ≫ 5600 65W，過剩沒事；高度 150mm，NX800 限高 180mm 沒問題 |
| GPU | **Tesla M40 24GB（二手）+ 渦輪扇套件 + EPS 轉接線** | $5,000 + $500 + $200 = $5,700 | 蝦皮 $4,500-6,000 / 對岸閒魚 RMB 1,200(~$5,200) | 24GB VRAM 是 $5k 內**唯一**選項；FP16 6.8 TFLOPS 跑 Llama 3.1 8B Q4 約 8-15 tok/s（FitMyLLM 數據），夠 dev 用 |
| 機殼 | Antec NX800 | $2,390 | 巴哈姆特 / 紐頓 $2,390 (1.00x) | E-ATX、玻璃側透、前 2×20cm + 上 2 + 後 1 風扇位（M40 散熱救星）、顯卡限長 350mm（M40 是 267mm，沒問題）|
| PSU | **既有 CM MWE 750W Bronze** ⚠️ | $0 | — | 暫用，省 $2,500；但長期 LLM 滿載要換 80+ Gold 雙 EPS |
| EPS 轉接線 | PCIe→EPS 8pin（M40 專用） | $200 | 蝦皮 $150-300 | 餵 M40 用 |
| 渦輪扇改裝 | 9cm L 型 暴力扇 + 風罩 | $500 | 蝦皮 / 淘寶 $300-700 | 把 M40 從被動散熱改主動，**這不是 optional** |
| **小計（買新的部分）** | | **$20,680** | | |
| **+ 上門組裝 / 散熱膏 / SATA 線 / 雜項 buffer** | | **$1,500** | | |
| **TOTAL** | | **~$22,180** | | **剩 $2,820 預備換 PSU 或補風扇** |

---

# 📊 Use-case 適配度

- **Primary use**：本地 LLM 推論（dev / 玩票），預算極限走洋垃圾路線
- **適配亮點**：
  - **24GB VRAM**：可載入 Llama 3.1 8B fp16、13B Q4、Mistral 7B fp16、Qwen2.5 14B Q4
  - **32GB RAM**：CPU offload 跑 30B Q4 / 70B Q2 慢但能跑（每秒 1-2 tok）
  - **AM4 + B550**：PCIe 4.0 x16 給 M40（雖然卡本身只到 Gen3，但留升級空間）
- **不適合的事**：
  - **遊戲**：M40 連 GTX 980Ti 都打不過，1080p 中畫質都吃力（CC 5.2 不支援新 DX12 feature level）
  - **訓練 / fine-tune**：FP16 6.8 TFLOPS 太慢，QLoRA 一個 7B model 可能要跑一整晚
  - **影像 AI（Stable Diffusion XL）**：Maxwell 架構沒 Tensor Core，SDXL 一張 1024² 要 2-3 分鐘
  - **新版 PyTorch / CUDA 12+**：M40 是 Compute Capability 5.2，**CUDA 12.x 已 drop support**，被綁在 PyTorch ≤ 2.1 + CUDA 11.8。Linux only。
- **未來升級空間**：
  - PSU → 海韻 FOCUS GX-750 ($2,500)
  - 之後 GPU 升 RTX 3060 12GB 二手 ($5-6k) 或 RTX 4060 Ti 16GB 新 ($13k)
  - **CPU/MB 升不上去**：AM4 死路，要升只能整套換 AM5

---

# ⚠️ 還沒解的 Risk

1. **M40 二手卡 VRAM degradation**：挖礦 / 24x7 推論退役品，GDDR5 顆粒可能已老化。**買前要求賣家跑 MemtestG80 或 gpu-burn 證明**，不接受不退。
2. **M40 驅動 deadline**：NVIDIA 已在 2024 stop production driver；2026 還能用是因為 470 LTS 驅動延長到 2026-09，**之後新 kernel 自己編譯**。CUDA stuck on 11.8.
3. **M40 不支援 Windows 11 桌機驅動好幾年了** → **Linux only（Ubuntu 22.04 LTS + driver 470）**。如果想雙開 Win11 玩遊戲，遊戲時等於沒 GPU（只能靠 5600 內顯 → **5600 沒內顯！**）→ 這台**只能跑 Linux**，遊戲完全不能玩。
4. **B550M Pro4 BIOS** 沒驗到 P2.30+ 直接點不亮，自己沒備援 CPU 救機很麻煩。
5. **NX800 機殼前 2×20cm 風扇** 跟改裝後的 M40 渦輪扇可能風流互打，要實際裝完看散熱。
6. **CM MWE 750W Bronze 持續 LLM 滿載**：電容老化會先 sag → 系統重啟 / 黑屏，這條 PSU 是「先用著」不是「長期方案」。
7. **PCIe→EPS 轉接線品質**：劣質線 24/7 過 250W 會發燙融化。買「實心 16AWG」線，不要 18AWG。

---

# 🛒 採購建議

| 通路 | 買什麼 | 備註 |
|---|---|---|
| **原價屋（coolpc.com.tw）** | 5600 + B550M Pro4 + DDR4 32GB + SSD + Cooler + 機殼 | 一次菜單貼上，可順便請店家**代刷 BIOS** 並現場驗一次 POST。組裝費 $800-1,500 值得 |
| **欣亞（sinya.com.tw）** | 同上（價差 $100 內）| 實體店可現場驗 BIOS 版本 |
| **蝦皮 / 露天 / FB 社團「Tesla M40 / 計算卡交流」** | M40 24GB 二手 | **務必當面試卡**：跑 `nvidia-smi`、跑 `gpu-burn` 10 分鐘、看溫度曲線。**保固：3-7 天私保**是常態，**沒保固的不買** |
| **淘寶 / 蝦皮（M40 散熱套件）** | 渦輪扇 + L 型風罩 + EPS 轉接線 | 搜「M40 涡轮 散热 套件」一次到位，$500-800 |
| **不要碰** | PChome 24h 的低階套裝機 | 同預算 $25k 套裝機 GPU 通常只給 GT 1030 / GTX 1650，VRAM 4GB，LLM 完全跑不動 |

---

# 📝 給 Sam 的決策摘要

- **走 M40 路線 = 接受 Linux only + 不能玩遊戲 + 折騰散熱與供電 + 驅動被綁死**，換來 **$25k 預算內唯一 24GB VRAM** 的方案
- **如果折騰意願低**：直接 RTX 3060 12GB 二手 ($5.5k) + 同 build，少 12GB VRAM 但**完全沒坑**，還能玩遊戲
- **如果預算可拉到 $32k**：5600 換 5600G（有內顯救援）+ RTX 4060 Ti 16GB 新卡 ($13k) → 完整 16GB VRAM 消費卡 + 新卡保固
- **不建議走 P40 24GB 取代 M40**：P40 比 M40 強但二手 $8-12k，預算更緊；M40 是「真便宜」的甜蜜點

> ⚠️ 引用標註：M40 規格（FP16 6.8 TFLOPS / 288 GB/s / CC 5.2）來源 FitMyLLM、GPUDojo 2026 benchmark（見 Brave 搜尋結果，有附原連結）。改裝散熱方案來源知乎「Tesla M40\P40 训练机组装与散热改造」（已驗證但非 PTT，標 [對岸社群實作]）。B550M Pro4 沒 BIOS FlashBack 來源 r/buildapc thread（已驗證 ASRock 官方 spec page）。
