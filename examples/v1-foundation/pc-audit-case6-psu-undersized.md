# 🚨 PC Build Audit — Case 6：PSU 嚴重 underpowered

> 22 歲玩家、預算 NT$ 38,000、GPU 升 RTX 4080 Super 但 PSU 沒跟上

---

## 🚨 必修 BLOCKER（兩個，必須先解）

### BLOCKER 1 — PSU 嚴重 underpowered + 沒有 12V-2x6 原生線（火災級風險）

**問題**：
- **Corsair CV550** = 550W、80+ **Bronze**（不是 Gold）、**非模組化**、**沒有原生 12VHPWR / 12V-2x6 接頭**。
- 你這台的功耗預算：
  - i7-14700KF：基礎 TDP 125W，但 **PL2 / MTP 實際可拉到 253W**（Intel K 系列旗艦不設防）
  - RTX 4080 Super：TDP 320W，**transient spike 可衝到 400W+**
  - 主機板 / RAM / 風扇 / SSD：~50W
  - **最低需求**：(253 + 320 + 50) × 1.30 = **約 810W** → 必須 **850W 起跳**
- CV550 連 baseline 都不夠，會直接 OCP 跳機 / PSU 燒掉，最糟糕情況：4080 Super 用轉接頭吃 4×8pin 轉 12VHPWR → **重演 4090 燒接頭事件**。
- CV550 規格用途是辦公機 / GTX 1660 等級，**不該出現在這份菜單**。

**Fix path A（推薦，留 4080 Super）**：換 **MSI MAG A850GL PCIE5 850W**（ATX 3.1、原生 12V-2x6、80+ Gold）= 約 **NT$ 2,990**
- 或 **Corsair RM850x (2024) ATX 3.1** ≈ NT$ 4,290（10 年保、安靜，貴 1.3k）
- 或 **Seasonic Focus GX-850 ATX 3.1** ≈ NT$ 3,990（10 年保）

**Fix path B**（看 BLOCKER 2 — 預算根本不夠）：降 GPU 到 RTX 5070 12GB 或 RTX 5060 Ti 16GB，PSU 用 750W 即可。

---

### BLOCKER 2 — 預算嚴重超支（菜單總價 ≈ NT$ 67,000，預算只有 NT$ 38,000）

**菜單實際抓 2026 行情**：

| 項目 | 菜單型號 | 2026 行情 (NTD) |
|---|---|---|
| CPU | i7-14700KF | ~12,500 |
| MB | MSI PRO Z790-A（非 WiFi 版） | ~6,500 |
| RAM | Corsair Vengeance DDR5-6000 32GB | ~3,500 |
| SSD | Samsung 980 Pro 1TB | ~2,800 |
| Cooler | DeepCool AK620 | ~1,900 |
| GPU | Gigabyte RTX 4080 Super 16GB | **~36,000+** |
| Case | Lian Li O11 Mini | ~3,200 |
| PSU | Corsair CV550 | ~1,600 |
| **合計** | | **~68,000** |

**超支 NT$ 30,000**（180% over budget）。**這份菜單不可能用 38k 達成**。22 歲玩家如果硬刷下去，PSU 還會燒。

**Fix path**：把 GPU 從 4080 Super 降到 **RTX 5060 Ti 16GB**（NT$ 14,900）或 **RTX 5070 12GB**（NT$ 19,900），整台才壓得進 38k。下面 final spec 用這條路重組。

---

## 💰 NT$ 38,000 預算內 final spec（重組版）

> 留 GPU 主力，但換成預算 sweet spot；CPU 降階換省下的錢去買對的 PSU + 維持遊戲體驗。

| 項目 | 推薦 | 價格 (NTD) | 為何選 |
|---|---|---|---|
| CPU | **Intel Core i5-14400F** 或 **AMD Ryzen 5 7500F** | 5,990 | 22 歲玩家 1080p/1440p gaming 6 核夠用；i7-14700KF 對純玩家是過剩（多花 6k 換 5% FPS） |
| MB | **MSI PRO B760M-A WiFi DDR5**（若選 14400F）或 **ASUS PRIME B650M-K**（若選 7500F） | 4,290 | mATX、DDR5、Wi-Fi 6；不需要 Z790 因為 14400F 不能超頻 |
| RAM | **Kingston FURY Beast DDR5-6000 32GB (16×2)** CL36 | 3,290 | 32GB 雙通道、EXPO/XMP 雙支援；比 Corsair 同規便宜 ~200 |
| SSD | **WD Black SN770 1TB Gen4** 或 **Crucial P3 Plus 1TB** | 2,290 | Gen4、5000+ MB/s；980 Pro 在 2026 已被 990 Pro 取代且偏貴 |
| Cooler | **Thermalright Peerless Assassin 120 SE** | 990 | 雙塔 TDP 245W、壓 14400F / 7500F 綽綽有餘；AK620 對 65W CPU 過剩 |
| GPU | **NVIDIA RTX 5060 Ti 16GB**（華碩 / 微星 雙風扇版） | 14,900 | **16GB VRAM**（撐 1440p + 未來 LLM 試水）；4080 Super 漲了 22k 但 FPS 差距在 1440p 只多 30%，CP 不划算 |
| Case | **Montech Air 903 MAX** 或 **庫力士 Stack 1**（mATX） | 1,990 | ATX/mATX 通用、3 風扇預裝、走線網孔；O11 Mini 雖漂亮但價格貴 1.2k 又限 GPU 長 |
| PSU | **MSI MAG A750GL PCIE5 750W** ATX 3.1 | 2,490 | 80+ Gold、**原生 12V-2x6**、5060 Ti (180W) + 14400F (148W) × 1.3 ≈ 425W，750W 留 1.5× 升級空間 |
| **TOTAL** | | **~36,230** | 剩 **~1,770** buffer（散熱膏、組裝費 $800、Wi-Fi 天線）|

---

## 📊 Use-case 適配度

- **Primary use**：純玩家 1080p / 1440p gaming（22 歲、無提到 AI / streaming / 內容創作）
- **適配亮點**：
  1. **5060 Ti 16GB** 在 1440p 主流 AAA（Cyberpunk DLSS、霍格華茲、艾爾登法環）穩定 80-120 FPS
  2. **i5-14400F / R5 7500F** 跟 5060 Ti 是平衡組合，不 bottleneck，省下的錢全進 GPU + PSU
  3. **16GB VRAM** 撐未來 3-4 年新遊戲，不會像 8GB 卡兩年就吃緊
- **未來升級空間**：
  - PSU 750W 留 1.5× headroom，未來換 RTX 5070 Ti（285W）還夠
  - mATX MB 有 2 條 M.2，後續可加第二顆 SSD
  - 若三年後想跑 LLM dev，5060 Ti 16GB 也撐得住 Llama 3.1 8B Q4

---

## ⚠️ 還沒解的 risk

1. **若你真的執著要 4080 Super**：預算要拉到 **NT$ 65,000-70,000** 才合理（換 850W Gold PSU + 留 4080 Super + 維持 14700KF）。38k 內絕對放不下。
2. **如果 use case 其實有 LLM dev / 影片剪輯**：5060 Ti 16GB 邊緣堪用，但若要跑 13B+ LLM 或 4K 剪輯，得加預算上 5070 Ti 16GB（~26,000，全套要拉到 48k）。
3. **CV550 別硬上**：就算只搭 5060 Ti，CV550 非模組 + Bronze + 老設計仍不推薦，必換 750W ATX 3.1。
4. **14700KF 散熱**：若你最後選 14700KF 不降階，AK620（TDP 260W）僅勉強壓，建議改 **240mm AIO**（NZXT Kraken 240 或 Arctic Liquid Freezer III 240）。

---

## 🛒 採購建議

- **原價屋（coolpc.com.tw）**：菜單貼線上估價單，可加購上門組裝（$800-1,500），對新手最省事
- **欣亞（sinya.com.tw）**：實體店面在台北 / 台中，可現場驗 PSU + 看 case
- **autobuy.tw**：5060 Ti / PSU 常有限時殺，比原價屋便宜 200-500
- **PCHome 24h 對比**：同等級套裝機（i5 + 5060 Ti + 750W）通常開 NT$ 42,000-46,000，自組省 ~6-9k 但要會排線
- **PTT PC_Shopping 二手**：5060 Ti / PSU 不建議二手（PSU 老化 + GPU 礦渣風險）；CPU / RAM / SSD 二手相對安全

---

## 給 22 歲玩家的話

你菜單最大的問題不是哪個零件選錯，是 **GPU 一升上去就忘了重算整台的功耗 + 預算**。i7-14700KF + RTX 4080 Super 是 NT$ 70,000 級的旗艦組合，硬塞 38k 預算 + CV550 是會出事的。先把 use case 想清楚：

- **只玩遊戲** → 上面這份 i5 + 5060 Ti 是 sweet spot，38k 內最強
- **要 4080 Super** → 預算拉到 65k+，PSU 必須 850W ATX 3.1
- **要 AI / 創作** → 直接跳 5070 Ti 16GB，48k 起跳

別用 CV550 配 4080 Super，**真的會燒**。
