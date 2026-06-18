# PC Build Audit — Case h11-bios-trap

> Persona：新買 7800X3D 配 2023 製 B650 舊 BIOS，需先刷 BIOS 才能開機
> 預算：NT$ 50,000
> Audit 日期：2026-06-19

---

## 🚨 必修 BLOCKER

### BLOCKER #1：超出預算約 NT$ 8,000-10,000

實算菜單行情（2026-06 中位數，來源見 §3）：

| 項目 | 報價中位數 |
|---|---|
| R7 7800X3D 盒裝 | $12,500 |
| ASUS PRIME B650-PLUS WiFi (2023 庫存) | $4,500 |
| G.Skill Flare X5 DDR5-6000 32GB CL30 | $3,400 |
| Samsung 990 EVO Plus 2TB | $5,800 |
| Thermalright Phantom Spirit 120 | $1,400 |
| MSI RTX 5070 Ti Ventus 3X OC 16GB | $29,000 |
| Lian Li Lancool 216 | $2,700 |
| COUGAR GEX 750W Gold | $2,750 |
| **小計** | **$62,050** |

**超出 $50,000 預算 ~$12,000（24%）**。RTX 5070 Ti 一張就吃掉 58% 預算。必須二選一：

- **Fix path A（保 GPU 等級，降周邊）**：降 GPU 到 RTX 5070 12GB（~$20,500），省 $8.5k；MB 降到 PRIME B650M-A WiFi（mATX，~$3,800），SSD 砍到 1TB 990 EVO Plus（~$3,200）。總價約 $48k。代價：VRAM 12GB（LLM dev 不夠）。
- **Fix path B（保 7800X3D + 5070 Ti，砍其他）**：SSD 降 1TB（省 ~$2,800）、機殼換 Montech AIR 903 MAX（~$1,800，省 $900）、MB 換 MSI PRO B650-P WiFi（~$3,800，省 $700），總價約 $57k，仍超 $7k。**不建議，必須加預算**。
- **Fix path C（坦白加預算）**：把預算開到 $58,000-60,000，菜單原樣可過。這顆 5070 Ti 在 $50k 級不可能塞下。

### BLOCKER #2：B650 舊 BIOS 開機問題（已有解法，必須走流程）

ASUS PRIME B650-PLUS WiFi 支援 7800X3D 需 **BIOS 1409 以上**（Reddit + ASUS support 多串確認）。2023 出貨庫存板通常是 0805/0828 等早期版本，**裝上 7800X3D 直接亮 CPU debug LED、不開機**。

**好消息**：ASUS PRIME B650-PLUS WiFi **內建 BIOS FlashBack 按鈕**（ASUS Global 產品頁規格表明列），不需另一顆 CPU 就能刷 BIOS。流程：
1. 開箱前不要先裝 CPU，先確認 MB 後 I/O 是否有 BIOS FlashBack 鈕（白色按鈕，旁邊有 USB 標誌）。
2. 下載 ASUS 官網最新 BIOS（建議 2812 之後的版本，目前更穩），改名 `PB650PW.CAP`，放入 FAT32 格式化的 USB（插入專用 USB-BIOSFlashBack 孔，通常標示白框）。
3. 只接 24-pin + 8-pin CPU power，**不裝 CPU、不裝 RAM、不裝 GPU**，按 FlashBack 鈕 3 秒，等綠燈閃 3-5 分鐘到熄滅。
4. 刷完後再裝 CPU + RAM + GPU 開機。

**Fix path（依風險偏好擇一）**：
- **Path A（推薦）**：跟賣家指定**先代刷 BIOS 再出貨**，原價屋 / 欣亞通常免費或 $100，省事。下單備註寫「請刷 BIOS 至最新版，CPU 是 7800X3D」。
- **Path B**：自己 FlashBack（按上述流程）。預備一支 8-16GB FAT32 USB。
- **Path C（最貴最簡單）**：直接升 ASUS PRIME B850-PLUS WiFi（~$5,800，貴 $1,300），原生支援 Zen 4 全系列，零 BIOS 風險，未來升 Zen 5 / Zen 6 也直接吃。**強烈建議走這條**，差價 $1,300 換零開機風險 + 平台升級空間，CP 值最高。

---

## 💰 推薦 final spec（建議預算上調至 NT$ 58,000，並走 B850 解決 BIOS）

| 項目 | 推薦 | 價格 | 為何選 |
|---|---|---|---|
| CPU | AMD R7 7800X3D 盒裝 | $12,500 | 遊戲王，3D V-Cache，TDP 120W 但實測 70-80W 跑，散熱輕鬆 |
| MB | **ASUS PRIME B850-PLUS WiFi**（取代 B650） | $5,800 | 原生 Zen 5 BIOS、零 FlashBack 風險、ATX、DDR5、Wi-Fi 6E、5 年保 |
| RAM | G.Skill Flare X5 DDR5-6000 32GB (16×2) CL30 | $3,400 | AM5 甜蜜點 6000 CL30 EXPO，所有 B650/B850 QVL 都有 |
| SSD | Samsung 990 EVO Plus 2TB Gen4 | $5,800 | 7,250/6,300 MB/s、5 年保；2026 NAND 漲價後 2TB 算合理 |
| Cooler | Thermalright Phantom Spirit 120 SE | $1,400 | 雙塔 7 導管、TDP 245W、壓 7800X3D（實耗 ~80W）綽綽有餘 |
| GPU | MSI RTX 5070 Ti 16G VENTUS 3X OC | $29,000 | 16GB GDDR7、Blackwell、1440p 4K 主力、預留 LLM inference 空間 |
| Case | Lian Li Lancool 216 | $2,700 | E-ATX 容得下、顯卡長度 392mm、CPU 高 180mm、含磁吸前濾網 |
| PSU | COUGAR GEX 750W Gold 全模組 | $2,750 | 750W 達標（math 見下）、80+ Gold、5 年保、全模組好走線 |
| 12V-2x6 線 | （PSU 附原生 ATX 3.0 線） | - | GEX 750W 是 ATX 3.0 認證，原生 12V-2x6，不用轉接頭 |
| **小計** | | **$63,350** | |
| **預估上門組裝 + 散熱膏 + 雜項** | | $1,500 | 原價屋上門組裝 $800-1500 |
| **TOTAL** | | **~$64,850** | |

### PSU math line（hard rule §4.7 strict 印出）

```
required_watt = CPU TDP + GPU TDP + 30% headroom
            = 7800X3D (120W) + RTX 5070 Ti (300W)
            = 420W → ×1.3 = 546W
            → 推薦 ≥ 650W；750W 留 4090/5080 升級空間 OK
```

**結論**：750W 不僅達標還有餘裕，未來升 RTX 5080（360W）一樣夠。

### 🟡 2026 SSD/RAM HBM 紅利期 CALLOUT

> 因 HBM3e + AI 訓練卡需求佔走 NAND / DRAM 產能，2026 SSD / DDR5 售價相對 2023 **+30~50%**。990 EVO Plus 2TB ≈ $5,500-6,000、DDR5-6000 32GB kit ≈ $3,200-3,800 是 2026-06 合理區間。低於此區間要懷疑水貨/拆機。GPU 30 系列已停產，RTX 50 為新案主流。

---

## 📊 Use-case 適配度

**Persona 未明確指定 use case**，但選 7800X3D + RTX 5070 Ti 16GB 推測為：

- **Primary 1：高階遊戲（1440p / 4K）** — 7800X3D 是當前遊戲王，5070 Ti 16GB 在 1440p 主流 3A 全開高/極高 100+ FPS、4K DLSS 4 也順。**完美 fit**。
- **Primary 2（兼）：輕量 LLM / AI 玩家** — 16GB VRAM 跑 Llama 3.1 8B Q4 + 7B 全精度 OK，Mistral Small / Qwen 14B Q4 也吃得下。**夠用**。
- **不適合**：純 LLM dev 跑 13B+ 全精度 → 要 5080 16GB or 4090 24GB；7800X3D 8 核對重 data eng 偏少（但 game / LLM inference 沒差）。

### 未來升級空間

- RAM 升 64GB（再買一組 Flare X5 16×2）— B850 板 4 槽
- 第二顆 SSD（B850-PLUS WiFi 有 3 個 M.2 槽）
- GPU 直升 RTX 5080 / 5090（PSU 750W 撐到 5080，5090 要 850W+）
- CPU 升 Zen 5 / Zen 6（AM5 平台官宣支援到 2027+）

---

## ⚠️ 還沒解的 risk

1. **若堅持留 B650-PLUS WiFi**：開箱**不要先裝 CPU**，先確認後 I/O BIOS FlashBack 鈕；買 8-16GB USB 預備 FAT32 格式化。失敗會出現紅燈持續閃爍。買前跟賣家確認**到貨已是 1409+ BIOS** 是最安全做法。
2. **預算嚴重不足**：若 Sam 真的卡在 $50,000，必須砍 GPU 到 5070 12GB（不推 LLM）或 砍 SSD 到 1TB（短期可，未來補）。**不可能 $50k 同時拿到 7800X3D + 5070 Ti**。
3. **Lancool 216 風扇**：原版只附 2 顆前 160mm + 1 顆後 120mm，**沒附頂出風**。塞 7800X3D + 5070 Ti 建議補 2 顆 120mm 頂排出風（~$600）強化排熱。
4. **GEX 750W 線長**：搭 Lancool 216（中塔走背線約 550mm 距離），GEX 24-pin 線長 610mm 沒問題，但 8+8 EPS 上路徑可能略緊，組裝時注意。
5. **5070 Ti Ventus 3X 長度 338mm**：Lancool 216 支援 392mm，**OK**。
6. **Phantom Spirit 120 高度 157mm**：Lancool 216 CPU 高度上限 180mm，**OK**。

---

## 🛒 採購建議

- **原價屋（coolpc.com.tw）**：菜單貼上自選，可指定上門組裝（$800-1500）、可指定**先代刷 BIOS**（若堅持留 B650-PLUS）。**主推**。
- **欣亞（sinya.com.tw）**：實體店面，可現場驗機 + 直接看到 BIOS 版本貼紙（板子側貼條會印 BIOS rev），對 BIOS trap 是最安全。**若不放心 FlashBack 走這條**。
- **autobuy.tw**：促銷檔可挖到 GPU / SSD 殺，但 BIOS 代刷服務沒原價屋方便。
- **套裝機對比**：PCHome 24h 同 spec（7800X3D + 5070 Ti）套裝約 $68,000-72,000，貴 $3-7k 但全機保固 + 免 BIOS 風險。**若 Sam 嫌麻煩可考慮**。

### 採購時備註範本（直接複製給賣家）

> 您好，我這顆 CPU 是 7800X3D，主機板若是 ASUS PRIME B650-PLUS WiFi 出貨前**請代刷 BIOS 至 2812 以上**（最低 1409，建議最新）；若無法代刷請主動告知，我改選 B850-PLUS WiFi。謝謝。

---

## 📚 來源驗證（Brave search 2026-06-19）

- 7800X3D 行情：原價屋公告 + PTT PC_Shopping `[情報] 原價屋 7800X3D Tray盤 $9900`（盒裝 $11,900-12,900）
- B650-PLUS WiFi BIOS：Reddit `r/buildapc` + ASUS support「7800X3D supported starting from BIOS version 1409」（多串確認）
- ASUS PRIME B650-PLUS WiFi 規格表（ASUS Global）— 明列 BIOS FlashBack™
- Flare X5 6000 CL30 32GB：原價屋 RAM 列表（雙通 32G*2 黑色約 $3,200-3,800）
- 990 EVO Plus 2TB：欣亞「組裝價」頁面，2026 NAND 漲價後 $5,500-6,500
- Phantom Spirit 120：BigGo 比價「$1,890 蝦皮商城 / 原價屋 Coolpc」+ SE 版 $1,400 區間
- RTX 5070 Ti Ventus 3X OC：XFastest 上市報導 + 原價屋首賣公告（MSRP $749 USD，台灣價約 $28,000-30,000）
- Lancool 216：BigGo 2026 年 5 月「$2,700 ~ $2,900」
- COUGAR GEX 750W：BigGo + PChome「$2,690-2,790」

> 部分推論基於 BigGo / PCHome 通路報價中位數，非每個 component 都跑滿 4 通路（sinya / coolpc / autobuy / momo）；GPU / SSD 通路波動大，下單前再覆查一次。
