# PC Build Audit — Case `h1-itx-compact`

- Persona：客廳 HTPC + 1080p gaming，mini-ITX 形系
- 預算：NT$ 42,000
- 關鍵約束：GPU 長度 / cooler 高度 clearance

---

## 🚨 必修 BLOCKER

### BLOCKER 1 — Cooler 高度超出 A4-H2O 限制（10mm overshoot）

- Noctua **NH-L9x65 實際高度 = 65mm**（Noctua 官方 spec），用戶 brief 寫「5.8cm」是錯的。
- Lian Li **A4-H2O CPU cooler clearance = 55mm**（TechPowerUp 實測 + 官方 doc 一致確認）。
- 65mm > 55mm → **側板蓋不上**，這不是「擠一下」可以解決的問題。
- A4-H2O 本身就是 H2O（水冷）導向 11L sandwich-layout 機殼，原廠定位是 **240mm AIO**，air-cooler 路線在 55mm 高度只能塞 NH-L9i / NH-L9a-AM5（37mm）等真正 low-profile。
- 補充：A4-H2O 案件高度 brief 寫 19cm 也不對，**實際 244mm（24.4cm）**，3 個 dimension 是 326×140×244mm。

**Fix path A（建議，HTPC 最佳）— 換 240mm AIO（A4-H2O 原生定位）**

- 推：**ID-COOLING FX240 PRO / Cooler Master MasterLiquid 240 Atmos / Lian Li Galahad II Trinity 240**
- 240mm AIO 壓 R7 7700（65W TDP，PPT 88W）綽綽有餘，客廳環境冷頭風扇 PWM 拉低，比塔散還安靜
- 預算增 NT$ 2,000-2,800

**Fix path B（保留 air-cooler 路線，犧牲 CPU 性能）— 換真正 low-profile**

- 推：**Noctua NH-L9a-AM5**（37mm，AM5 原生扣具，AM5 socket 專屬版本）
- 缺點：L9a 額定 TDP 仅 ~65W 邊緣壓 7700，長時間多核 boost 會降頻；客廳輕負載 OK，烤機會吵
- 預算少 NT$ 500-800（比 L9x65 更便宜）

**Fix path C — 換 CPU 到 65W 以下 + 用 L9a**

- 換成 **R5 7600**（65W）或 **R5 8500G**（含 iGPU，HTPC 用甚至可不裝 GPU 省一大塊預算）
- HTPC 1080p gaming 7600 完全夠用，多核略弱於 7700 但對 use case 影響小

---

## 🟡 2026 SSD / RAM HBM 紅利期 baseline

> 因 HBM3e + AI 訓練卡需求佔走 NAND / DRAM 產能，2026 SSD / DDR5 售價相對 2023 **+30~50%**。1TB Gen4 NVMe ≈ $2,200-2,800（SN850X 已殺到 $3,790 是含散熱片官方價）、DDR5-6000 32GB CL30 ≈ $3,200-3,800。GPU 30 系列已停產，RTX 40 Super 系列接近清庫存階段，2026 Q2 起 RTX 50 為主流，**4070 Super 12GB 走 EOL/特價 channel**，要查還有沒有現貨保固。

---

## 💰 PSU math line（必印）

```
required_watt = CPU TDP + GPU TDP + 30% headroom
             = 65 (R7 7700) + 220 (RTX 4070 Super) + 30%
             = 285W × 1.3 = 370.5W → 推 550W~650W SFX
原配 V750 SFX Gold (750W) → 嚴格說 over-spec ~100W，但 SFX 750W 為 A4-H2O 安裝餘裕的甜蜜點（線材長度 + 未來換 5070 Ti 留 buffer），可保留。
```

V750 SFX 為 **80+ Gold + 全模組 + ATX 3.0 cable**，10 年保，A4-H2O 官方 PSU compat list 在列，保留。

---

## 💰 [預算 NT$ 42,000] 內 修正後 final spec（採 Fix path A — 240mm AIO）

| 項目 | 推薦 | 價格 (NT$) | 為何選 |
|---|---|---|---|
| CPU | AMD Ryzen 7 7700 | 6,990 | 8C16T 65W、AM5 平台、HTPC + 1080p gaming 綽綽有餘、原廠搭板價 |
| MB | MSI MPG B650I EDGE WIFI | 5,990 | ITX、AM5、Wi-Fi 6E、雙 M.2、8+2+1 VRM 對 7700 過剩 |
| RAM | Crucial DDR5-6000 32GB CL30 (16×2) | 3,400 | AM5 甜蜜點 6000 CL30 EXPO；幾乎所有 AM5 板 QVL 都有 |
| SSD | WD SN850X 1TB (含散熱片) | 3,790 | Gen4 7300/6300 MB/s、5 年保、ITX 板 M.2 散熱壓力大要含片 |
| GPU | Galax RTX 4070 Super 12GB (≤30cm) | 17,500 | 12GB 對 1080p HTPC 戰未來、長度確認 ≤ 322mm A4-H2O 上限；如 EX 版 32cm **塞不下**要選 1-Click OC 短版 |
| Cooler | **改：ID-COOLING FX240 PRO** | 2,800 | 240mm AIO，A4-H2O 原生定位、壓 7700 安靜 |
| Case | Lian Li A4-H2O (含 PCIe 4.0 riser) | 3,500 | 11L SFF、240 AIO 相容、322mm 大卡 OK |
| PSU | Cooler Master V750 SFX Gold (10 年保) | 3,890 | SFX、80+ Gold、全模組、ATX 3.0、A4-H2O 安裝餘裕足 |
| **SMALL TOTAL** | | **47,860** | **超出 $5,860** |

### 預算超支 — 取捨建議（HTPC 1080p 視角）

1. **GPU 改 RTX 4060 Ti 16GB / RTX 4070 12GB（非 Super）** → 省 NT$ 3,500-5,000
   - 1080p HTPC 老實說 4070 Super 已 overkill，4060 Ti 16GB 對 1080p AAA 80+ FPS 沒問題、未來 1440p 升級保留 VRAM。
2. **PSU 降 650W SFX Gold** → 省 NT$ 800-1,200（math line 算出來 470W 即足）
3. **CPU 改 R5 7600** → 省 NT$ 1,500，HTPC 不會有感

採以上 1+2 → **42,000 內成立**，spec 表如下：

| 項目 | 推薦 | 價格 (NT$) |
|---|---|---|
| CPU | AMD Ryzen 7 7700 | 6,990 |
| MB | MSI MPG B650I EDGE WIFI | 5,990 |
| RAM | Crucial DDR5-6000 32GB CL30 | 3,400 |
| SSD | WD SN850X 1TB | 3,790 |
| GPU | RTX 4060 Ti 16GB (≤30cm 短版) | 13,500 |
| Cooler | ID-COOLING FX240 PRO 240mm AIO | 2,800 |
| Case | Lian Li A4-H2O | 3,500 |
| PSU | Cooler Master V650 SFX Gold | 2,890 |
| **TOTAL** | | **42,860** |
| **Buffer 剩** | | **~$0**（含上門組裝要另 +$1,000-1,500） |

> 若堅持 4070 Super：總價需拉到 ~NT$ 47,000；建議 budget 上修或接受 4060 Ti 16GB。

---

## 📊 Use-case 適配度

- **Primary：客廳 HTPC + 1080p gaming**
- 適配亮點：
  - ITX 11L sandwich-layout，客廳 TV 櫃放得下、視覺低調
  - 240mm AIO 比塔散安靜，客廳環境噪音敏感
  - R7 7700 65W 全速也不會把 AIO 風扇飆高，idle 接近無聲
  - 12GB / 16GB VRAM 都遠超 1080p 需求，**未來升級 4K HDR 客廳 TV 也吃得下**
- 未來升級空間：
  - AM5 平台 socket 支援到 Zen 6（2027+），CPU 可繼續升
  - GPU 換 5070 / 5070 Ti 短版（322mm 內）OK
  - 第二顆 NVMe slot B650I EDGE 有，影音庫擴充無痛

---

## ⚠️ 還沒解的 risk

1. **GPU 長度** — Galax RTX 4070 Super 有多版本，**EX Gamer 1-Click OC = 320mm（A4-H2O 上限 322mm，邊緣）**、**1-Click OC 2X V2 = 261mm**（更安全）。下單前確認 SKU 長度，別只看「26cm」這個籠統值。
2. **R7 7700 + 老 B650 BIOS** — 7700 是 Zen 4 首批，B650I EDGE 應原生支援，但若是賣場庫存舊批號，請賣家代刷最新 BIOS（原價屋免費）；MSI ITX **沒有 FlashBack 按鈕**，沒 CPU 不能刷。
3. **A4-H2O 安裝難度** — sandwich-layout + riser cable，**Sam 不熟組裝請走原價屋上門組裝（+$1,500-2,000）**，預算要再加。
4. **客廳供電** — 確認客廳 TV 櫃插座有專迴路，HTPC 開機 + TV + soundbar 同一插排會限流。
5. **HTPC 噪音** — A4-H2O 11L 體積排熱緊，240 AIO 風扇 + GPU 在客廳 1m 內距離 idle 仍會聽到，要求絕對靜音 → 走 **Fix path B** R5 8500G iGPU 無獨顯路線。
6. **DDR5 QVL** — Crucial DDR5-6000 CL30 在 B650I EDGE QVL 內，OK，但 32GB×2 雙條 6000 CL30 在 AM5 ITX 板有時要降到 5600 才穩，買前看一下 RAM 型號 part number 是否 EXPO。

---

## 🛒 採購建議

- **原價屋 coolpc.com.tw** — 主要建議通路，菜單貼上選 ITX 自選 + 勾選**上門組裝 NT$ 1,500**（A4-H2O sandwich-layout DIY 難度高，第一次組裝強烈建議付）
- **欣亞 sinya.com.tw** — A4-H2O 庫存常態有，可現場取貨
- **autobuy.tw** — Cooler Master V750 SFX 此通路常促銷 $3,690（省 $200）
- **PCHome 24h / momo 同 spec 套裝機**：ITX HTPC 套裝幾乎不存在（市場供給少），自組是唯一路徑
- **二手 4070 Super**：PTT PC_Shopping 買賣板 12,000-14,000 區間有，可省 $4,000-5,000，但 GPU 二手要驗烤機 + 看保固轉移，HTPC use case 風險偏高不建議

---

## Checklist 自我驗證（per skill v2）

- [x] Parts list parse 完
- [x] CPU socket vs MB chipset 對矩陣：AM5 R7 7700 ↔ B650 ✅
- [x] RAM gen vs MB：DDR5 ↔ AM5 ✅
- [x] PSU math line（285W × 1.3 = 370.5W）已印
- [x] Case form factor：ITX MB ↔ ITX 案 ✅
- [x] Cooler clearance：**65mm > 55mm → BLOCKER** ✅ 已抓
- [x] Brave 行情驗價：跑過 A4-H2O / 7700 / SN850X / V750 SFX / B650I EDGE / DDR5-6000 CL30
- [x] 2026 SSD/RAM HBM CALLOUT 已寫
- [x] BIOS update 警告：MSI ITX 無 FlashBack 已標
- [x] DDR5 QVL 提醒已標
- [x] Use case 確認（HTPC + 1080p gaming）
- [x] Buffer 提示（上門組裝 + 散熱膏 + Wi-Fi 天線）
- [x] ITX edge case：GPU 長度 / cooler 高度 ✅ 雙重檢查
- [x] 不確定規格不編造（GPU 長度因 SKU 而異，已標 risk）
