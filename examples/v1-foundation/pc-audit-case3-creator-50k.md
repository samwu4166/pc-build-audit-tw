# PC Build Audit — case3-creator-50k

**Persona**: 28 歲影像剪輯師,主跑 DaVinci Resolve Studio + Premiere + 4K H.265 export
**Budget**: NT$ 50,000

---

## 🚨 必修 BLOCKER

**沒有硬性 compatibility BLOCKER**(socket / RAM gen / case form factor / cooler TDP 全對),但有**預算嚴重超標 (~+30%)** 與**配置失衡**問題,等同於另一種 BLOCKER —— 照原單下去買單會破預算 NT$15k 以上,且錢花在不該花的地方。

### 原菜單估價拆解 (2026-06 原價屋中位數)

| 項目 | 原選 | 中位價 |
|---|---|---|
| CPU | R7 7800X3D 盒裝 | $11,500 |
| MB | Gigabyte X670 AORUS Elite AX | $9,500 |
| RAM | Corsair Vengeance DDR5-6400 64GB (2×32) | $8,000 |
| SSD | WD Black SN850X 2TB | $7,450 |
| Cooler | Be Quiet! Dark Rock 4 | $2,200 |
| GPU | MSI RTX 4070 Super 12G VENTUS 2X OC | $21,990 |
| Case | Lian Li Lancool 216 | $2,400 |
| PSU | Seasonic Focus GX-850 ATX 3.1 金牌 | $4,290 |
| **TOTAL** | | **≈ $67,330** |

**超預算 ~$17,330 (+34%)**,且以下三點是純浪費,不解掉省不下:

- **PSU 850W 嚴重過剩**:7800X3D 120W + RTX 4070 Super 220W + 30% = **442W**,750W 金牌足夠,850W 多花 ~$1,300 無感
- **X670 chipset 對 7800X3D 太奢侈**:7800X3D 不超頻 (X3D 鎖頻),用 X670 高 VRM + 雙 chipset 完全浪費;B650 / B850 一張 $5k 內就能完全發揮
- **DDR5-6400 64GB 在 AM5 反而扣分**:AM5 EXPO 甜蜜點是 **DDR5-6000 CL30**,因為 FCLK 1:1 同步上限約 2000~2100 MHz。6400 會自動掉到 2:1 mode,latency 變高、實測效能比 6000 還差。剪輯場景吃 capacity > speed,改 DDR5-6000 64GB 更划算

### Fix path A — 守 50k 預算 (recommended,見下方 final spec)
Downgrade 上述三點 + 機殼小調,GPU 維持 4070 Super 12GB(剪輯 4K H.265 對 12GB VRAM 可接受,DaVinci Resolve 主要吃 GPU 算力 + RAM)。

### Fix path B — 預算彈到 60k 換真正 creator-tier GPU
若可加 ~$10k → 換 **RTX 5070 Ti 16GB (~$33k)**,16GB VRAM 對 DaVinci Studio + 8K timeline 更穩。但 50k 預算下不建議。

---

## 💰 [預算 $50,000] 內 final spec

| 項目 | 推薦 | 價格 | 為何選 |
|---|---|---|---|
| CPU | AMD Ryzen 7 7800X3D 盒裝 | $11,500 | 維持原選;8C16T + 96MB 3D V-Cache,剪輯 timeline scrubbing + 預覽流暢,功耗 120W 散熱壓力小 |
| MB | **Gigabyte B650 AORUS Elite AX** (或 MSI B650 Tomahawk WiFi) | $5,490 | 改 B650:7800X3D 鎖頻不需 X670;VRM 14+2+2 phase 壓 7800X3D 綽綽,Wi-Fi 6E + 2.5G LAN 保留,**省 $4,000** |
| RAM | **Corsair Vengeance DDR5-6000 CL30 64GB (2×32)** | $6,800 | 改 6000 CL30 EXPO:AM5 甜蜜點、FCLK 1:1、實測比 6400 還快;64GB capacity 不變,剪輯 + 多軌音訊夠用,**省 $1,200** |
| SSD | WD Black SN850X 2TB Gen4 (含散熱片) | $7,450 | 維持;Gen4 7300/6600 MB/s,4K H.265 proxy + cache 夠用;影像剪輯 2TB 是底線 |
| Cooler | **Thermalright Phantom Spirit 120 SE ARGB** | $1,290 | 改塔散:雙塔六熱管 TDP 245W,壓 7800X3D (120W) 比 Dark Rock 4 (200W) 更強更便宜,**省 $900** |
| GPU | MSI RTX 4070 Super 12G VENTUS 2X OC | $21,990 | 維持原選;DaVinci Resolve CUDA + NVENC AV1/H.265 硬編,4K timeline OK;VRAM 12GB 對 4K creator 屬底線(8K 不夠),預算內最佳解 |
| PSU | **Seasonic Focus GX-750 ATX 3.1 金牌** | $3,790 | 改 750W:120W + 220W + 30% = 442W,750W 餘裕 40%;原生 12V-2x6 接 4070 Super 直插,**省 $500** |
| Case | Lian Li Lancool 216 (黑/非 RGB) | $2,400 | 維持;mesh 前面板高 airflow、雙 14cm 預裝風扇、顯卡長 392mm 容下所有卡、E-ATX 也吃,剪輯機散熱友善 |
| **TOTAL** | | **≈ $60,710** | 仍超 ~$10k,見下方 Path A2 |

### Path A2 — 進一步壓到 50k 預算內的取捨方案

50k 預算 + 影像剪輯 + 64GB RAM + 2TB SSD + 主流 GPU,**數學上幾乎不可能同時滿足**(光 CPU + GPU 就 $33,490)。三個取捨擇一:

#### 選項 1:RAM 降 32GB(最推薦,影響最小)
- Corsair Vengeance DDR5-6000 CL30 **32GB (2×16)**:**$3,400**(省 $3,400)
- TOTAL ≈ **$57,310**
- 影響:DaVinci Resolve 4K 剪輯 32GB 仍可運作,但多軌 + Fusion + Color page 同開會吃緊;後續加裝兩條湊 64GB 約 $3.4k

#### 選項 2:SSD 降 1TB + 換平價 Gen4
- WD SN770 1TB / KIOXIA EXCERIA Pro 1TB Gen4:**$2,500**(省 $4,950)
- TOTAL ≈ **$55,760**
- 影響:1TB 對影像剪輯太緊,通常 2-3 個案子就爆;**不建議**,除非另有大容量 HDD/外接 SSD 放素材

#### 選項 3:GPU 降 RTX 4060 Ti 16GB
- MSI RTX 4060 Ti 16GB VENTUS 2X:**$14,990**(省 $7,000)
- TOTAL ≈ **$53,710**
- 影響:**VRAM 16GB 反而對 creator 更友善**(8K timeline / DaVinci Studio noise reduction OK),但純算力比 4070 Super 弱 ~25%、4K render 時間多 20-30%;若 daily driver 是 4K **而非** 8K、出片時間不趕,這是 **creator skill 規則最對齊**的選項(VRAM ≥ 16GB)

**Sam style recommendation**:若 client deliverable 是 4K H.265 → **走選項 3**(4060 Ti 16GB,符合 creator VRAM ≥16GB 鐵則,渲染時間多一點換 capacity 與穩定);若主要做 1080p/2K commercial、剪完就出 → **走選項 1**(留 4070 Super 算力,RAM 先 32GB 之後升 64GB)。

---

## 📊 Use-case 適配度

- **Primary use**: 影像剪輯 (DaVinci Resolve Studio + Premiere + 4K H.265 export)
- **適配亮點**:
  - **7800X3D**:剪輯 timeline 即時預覽、Fusion 節點運算靠 cache 命中率,3D V-Cache 96MB 有顯著實測幫助
  - **64GB DDR5-6000**(若走原 spec): DaVinci 多 page (Edit + Color + Fusion + Fairlight) 同開無壓力,4K proxy cache 不爆
  - **SN850X 2TB Gen4**:H.265 long-GOP decode 對 SSD random read 敏感,7300 MB/s 順序讀 + 高 IOPS 撐得住
  - **NVENC (RTX 4070 Super)**:DaVinci Studio + Premiere 都支援 NVENC H.265 / AV1 硬編,export 比純 CPU 快 5-10×
- **不夠完美的地方**:
  - **VRAM 12GB** 對 8K / 大量 Fusion 節點 / DaVinci noise reduction 偏緊(creator skill 標準是 ≥16GB)
  - **未含螢幕**:剪輯機螢幕色準關鍵,50k 預算內無法含 calibrated monitor;假設 Sam 已有 / 另編預算
- **未來升級空間**:
  - RAM 兩條 → 四條湊 128GB(B650 AORUS Elite AX 4 DIMM)
  - 第二顆 SSD 4TB 放素材
  - GPU 換 RTX 5070 Ti 16GB / RTX 5080(PSU 750W 仍夠)

---

## ⚠️ 還沒解的 risk

- **VRAM 12GB 在 DaVinci Studio noise reduction / 8K timeline 會爆**:若 client 開始要 8K deliverable,GPU 需升級;此 build 是「2026 4K creator 底線」
- **DDR5-6000 64GB Kit 在 AM5 4 DIMM 全插時可能掉到 5200 MHz**:這 build 用 2 DIMM 沒問題,但未來升 128GB 要查 MB QVL
- **無 calibrated monitor**:影像剪輯後製色準關鍵,50k 預算內未含,假設另編預算 ~$8-15k(BenQ SW270C / Dell U2724D)
- **無 dedicated audio interface**:若收音/混音工作流複雜,Fairlight 內建夠用但 ASIO 延遲 >10ms;非預算範圍但要知道
- **Lancool 216 顯卡支架對 4070 Super 雙風扇 24cm 卡不必要**:可省略;若日後換 32cm+ 的 5080 再用
- **上門組裝費 $800-1500 未計入**:若走原價屋線上估價,勾「現場組裝」自動加;預算內請另外抓 $1k buffer

---

## 🛒 採購建議

- **原價屋 (coolpc.com.tw)**:菜單線上估價可一鍵改 chipset / PSU 瓦數比價,適合這次「替換 3 樣壓預算」的情境;勾「現場組裝」+ $1,200 含跑機
- **欣亞 (sinya.com.tw)**:7800X3D + 主機板組合常有套裝折扣,實體店面可現場驗 CPU 盒裝封條
- **autobuy.tw**:Corsair Vengeance + Thermalright 散熱常有限時殺,可單品比價
- **套裝機對比**:PCHome 24h / momo 同等級 7800X3D + 4070 Super 套裝機約 $68-72k(雜牌 B650M + 32GB RAM + 1TB SSD + 550W 銅牌),貴 $10-15k 且 spec 全面縮水,**強烈不推薦套裝**
- **自組 vs 上門**:自組省 $1.2k,但 7800X3D 散熱膏 + RAM EXPO BIOS 設定 + PSU 線材長度測試,首次組建議走原價屋上門

---

## 📋 採購單(走 Path A2 選項 3 — creator VRAM 優先版,合計 $53,710)

```
CPU     R7 7800X3D 盒裝                              $11,500
MB      Gigabyte B650 AORUS Elite AX                $ 5,490
RAM     Corsair Vengeance DDR5-6000 CL30 64GB 2x32  $ 6,800
SSD     WD Black SN850X 2TB Gen4 含散熱片            $ 7,450
Cooler  Thermalright Phantom Spirit 120 SE ARGB      $ 1,290
GPU     MSI RTX 4060 Ti 16GB VENTUS 2X              $14,990
PSU     Seasonic Focus GX-750 ATX 3.1 金牌           $ 3,790
Case    Lian Li Lancool 216 黑                       $ 2,400
                                                    -------
                                                    $53,710
buffer  上門組裝 + 散熱膏 + 雜項                      ~ $1,500
```

若 Sam 堅持 50k 硬上限 → 把 SSD 降 1TB ($2,500) 並另接外接 4TB HDD/SSD 存素材,合計剛好 $48,760。
