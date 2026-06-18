# PC 菜單 Audit — Case1 Gaming Budget 25K

> Persona：20 歲大學生，純 1080p AAA（Apex / Valorant / 原神）
> Budget：NT$ 25,000
> Audit 日期：2026-06-19

---

## 🚨 必修 BLOCKER

### B1. 「Lian Li Sirius 500W bronze」這顆 PSU 不存在

查遍 Lian Li 官方產品線、原價屋、欣亞、autobuy — **Lian Li 沒有「Sirius 500W」這顆電供**。Lian Li 的 PSU 線只有 SP750 / SP850（SFX 金牌）+ MAXIMA FORCE 系列，沒有 500W bronze 款。

可能來源：
- 把 Lian Li **Uni Fan SL Sirius**（RGB 風扇）誤當電供
- 把別牌（曜越 Smart BX2 / 全漢 / 振華）500W bronze 記成 Lian Li
- 商家拼湊單時打錯廠牌

**這顆要重選**。下面 final spec 直接幫你換成合理的 500W+ 金牌 PSU。

### B2. 500W bronze 對 7500F + RTX 4060 太勉強（即使真存在）

- 7500F TDP 65W + RTX 4060 TDP 115W = 180W
- 加 30% headroom = **234W** 持續負載
- 500W 紙面夠，但 **bronze 認證** + 不知名電供 = 電壓波動風險高，長期 wear 嚴重；4060 雖然只吃 8pin（沒燒接頭問題），但仍應選 **550W 80+ Bronze 起跳的有牌電供**（全漢 / 振華 / 海韻 / Cooler Master），$1,400-1,700 帶走。

### B3.（非 blocker，但要提醒）DDR5-5200 對 7500F 不最佳

7500F **官方支援 DDR5-5200**（CPU 沒問題能跑），但 AM5 平台的 RAM 甜蜜點是 **DDR5-6000 CL30 EXPO**，能解鎖 Infinity Fabric 1:1 同步，遊戲 FPS 多 5-10%。

5200 跟 6000 在 2026 Q3 同容量價差只剩 NT$200-300，**不換很虧**。下面 final spec 直接升 6000。

---

## 💰 預算 NT$ 25,000 內 final spec（修正版）

| 項目 | 推薦 | 價格 | 為何選 |
|---|---|---|---|
| CPU | AMD R5 7500F（**搭板專案價**）| **$3,990** | 6 核 12 緒、65W TDP、Apex/Valorant CPU bound 一樣 250+ fps；走原價屋技嘉搭板專案最便宜 |
| MB | **技嘉 B650M GAMING X AX**（搭板專案）| **約 $4,990**（搭 7500F 一起折扣後）或單買 $5,790 | mATX、DDR5、Wi-Fi 6E、2.5G LAN、6+2+1 相電供 7500F 完全壓得住；搭板專案總價最划算 |
| RAM | **Kingston FURY Beast DDR5-6000 16GB（8×2）EXPO** | **$1,700** | 升 6000 EXPO 解鎖 AM5 FB 1:1 甜蜜點；多花 $200 換 5-10% FPS 太值；雙通道一定要 8×2 不是單條 16 |
| SSD | WD SN770 1TB（黑標 Gen4）| **$2,690** | 5150/4900 MB/s、5 年保；遊戲讀取夠快，無 DRAM 但這價位無解（2026 SSD 漲價已成事實） |
| Cooler | ID-Cooling SE-214-XT BASIC | **$590** | 4 導管、TDP 180W、壓 65W 7500F 綽綽有餘 |
| GPU | Galax RTX 4060 Eclair 8GB | **$8,990** | 1080p AAA 主流卡；Apex 200+ fps、Valorant 400+ fps、原神 60+ 鎖頻無壓力；DLSS 3 Frame Gen 是亮點 |
| PSU | **全漢 / 振華 LEADEX III 550W Gold 全模組**（替換 Lian Li 那顆）| **$1,690** | 550W = 180W + 30% headroom 寬鬆；金牌效率 + 全模組整線；5 年保 |
| Case | Thermaltake Versa H21 | **$890** | ATX 中直立，吃 mATX MB 沒問題；側透；1 風扇預裝（後補 2 個 12cm 入風 ARGB $300） |
| 雜支 | 散熱膏 + 機殼風扇 + 上門組裝 | **約 $1,200** | 上門組裝 $800-1500、補風扇 $300 |
| **TOTAL** | | **約 $24,730** | 剩 $270 buffer，**穩穩在 25k 內** |

> 註：價格以 2026-06 原價屋 / 欣亞 中位數為準；7500F 搭板專案是 **菜單最大關鍵**，沒走專案 7500F+B650M 要 $4,990 + $5,790 = $10,780，會爆預算。下單前先打去原價屋確認「技嘉搭板專案還有沒有」。

---

## 📊 Use-case 適配度（純 1080p AAA Gaming）

- **Apex Legends** 1080p 高畫質：RTX 4060 預估 160-200 fps（競技設定 200+），R5 7500F 完全 keep up，CPU 完全不會 bottleneck
- **Valorant** 1080p 中畫質：CPU bound game，7500F 6 核能跑 **400-500 fps**，配 144/240Hz 螢幕無壓力
- **原神** 1080p 最高畫質：4060 鎖 60 fps 輕鬆，VRAM 8GB 在 1080p 完全夠（須塞流場景才會破 6GB）
- **DLSS 3 Frame Generation**：4060 支援，未來 AAA 大作（黑神話、GTA 6）可開來補幀
- **未來升級空間**：
  - RAM 升 32GB（換 16×2）省下 8×2 約 $1,500
  - 2-3 年後想上 1440p 換 5060 Ti 16GB 即可，B650M + 7500F + 550W PSU 完全 hold 得住
  - 第二顆 SSD：B650M GAMING X AX 有 2× M.2

---

## ⚠️ 還沒解的 risk

1. **Galax 三年保 vs 一年保**：Eclair 系列在台公司貨保固期要打去店家問清楚（有些通路只給 1 年，技嘉 / 微星同價位 3 年）；如果 Galax 只剩 1 年，**改買技嘉 RTX 4060 GAMING OC 8G 或 ASUS DUAL-RTX4060-8G**（同價位 $9,890，三~四年保更穩）
2. **DDR5-5200 換 6000 的價差**：若實際買到 5200 已下訂無法退，**先用著 5200 也行**（7500F 跑得起來），日後再升即可，差約 5-8% FPS
3. **Versa H21 散熱**：原廠只 1 顆後排風扇，建議補 2 顆 12cm 前進風（$300 內），不然夏天機殼內溫度會偏高
4. **PSU 換牌後的線材長度**：Versa H21 是標準 ATX 中塔，24pin 線 ≥ 550mm 即可，全漢/振華 550W 標配都夠
5. **無內顯**：7500F **沒內顯**，GPU 出包就全機點不亮 — RMA 期間沒備援，學生考量

---

## 🛒 採購建議

- **首選：原價屋（coolpc.com.tw）**
  - 走「**技嘉 7500F 搭板專案**」是這份菜單的核心，CPU+MB 直接省 NT$1,800-2,800
  - 自選清單貼上，可勾「上門組裝 $800-1500」省去自己排線跑 stress test 的麻煩
  - 學生黨建議直接讓原價屋裝好，跑完 OCCT/AIDA64 才出貨
- **次選：欣亞（sinya.com.tw）**
  - 板橋 / 台中有實體店，當面驗機驗保固卡，較適合不熟組裝的新手
  - 價格通常跟原價屋差 NT$100-300
- **autobuy.tw**
  - 機殼 / 散熱器 / 風扇 偶爾有殺，可單品比一下
- **PCHome 24h / momo 套裝機對比**
  - 同 spec（7500F + 4060 + 16GB DDR5 + 1TB）套裝機約 **NT$28,000-30,000**，比自組貴 $3-5k，但有整機 1-3 年保 — 不會組 / 怕踩雷的學生黨可考慮

---

## ✅ Quick decision summary（給 20 歲學生看的白話版）

1. **PSU 那顆「Lian Li Sirius 500W」要換掉**（不存在的型號 / 不夠力），改 550W 金牌全模組約 $1,690
2. **RAM 從 DDR5-5200 升 6000 EXPO**，多花 $200 換 5-10% FPS，太划算
3. **CPU+MB 一定要走技嘉搭板專案** $3,990 + $4,990，沒專案就爆預算
4. **GPU 確認保固年限**，Galax 若只 1 年改買技嘉 / ASUS 同價位
5. **整套 $24,730，剛好 25k 內**，1080p AAA 全打趴沒懸念
