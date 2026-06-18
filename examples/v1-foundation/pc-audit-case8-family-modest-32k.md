# 🧾 PC Audit — case8-family-modest-32k

> **使用情境**：45 歲媽媽幫小孩升級。小孩 Minecraft + 線上課；媽媽 Excel + Zoom。
> **預算**：NT$ 32,000
> **結論**：菜單沒有 BLOCKER（相容性都過），但**整份規格嚴重 overkill**，對這個使用情境是浪費錢。可以用同預算換更穩、更安靜、更省電的配置，還能多留 5-6k buffer。

---

## 🚨 必修 BLOCKER

**沒有硬性相容性 BLOCKER**。逐項驗過：

- ✅ R5 8400F（AM5, 65W）+ A620M-K（A620, AM5）→ socket / chipset 相容
- ✅ DDR5-5600 + AM5 → RAM gen 正確（AM5 = DDR5 only）
- ✅ NH-U12S TDP 支援 165W ≥ CPU 65W → 散熱過剩但可裝
- ✅ Antec DA601 E-ATX 機殼吃 mATX A620M-K → form factor OK
- ✅ Galaxy 600W ≥ 65W (CPU) + 180W (RX 6650 XT) + 30% buffer ≈ 320W → 瓦數有過

但有 **3 個重大「設計失誤」**讓這份單對「家庭使用」極不划算：

### ❌ 設計失誤 1：選了 R5 8400F（無內顯）→ 被迫買獨顯
8400F 是「F 後綴」，**沒有內顯**。對小孩玩 Minecraft + 線上課，**R5 8600G（內建 Radeon 780M）就夠用**，可以完全省掉獨顯（省 7-8k）。
→ Minecraft Java 版 1080p 中畫質，780M 可跑 60-90 FPS（PCDIY 實測串多次驗證）。

### ❌ 設計失誤 2：RX 6650 XT 對 Minecraft + Zoom 完全 overkill
6650 XT 是 **1440p 中階電競卡**，跑 AAA 大作用的。給 Minecraft + Zoom 是「用怪手挖盆栽」。而且 6650 XT 是 RDNA 2 上一代產品，新買沒保固價值。

### ❌ 設計失誤 3：Galaxy 600W bronze + Antec DA601 E-ATX 機殼
- **Galaxy 是中國雜牌電源**，家庭用機絕對不該用 — 電源爆掉燒主機板。家用機請用 **Antec / 海韻 / 全漢 / 振華**。
- **DA601 是 E-ATX 大電競殼**（玻璃透側、ARGB），家裡放客廳/書房看起來像網咖，且 mATX 主機板裝進去會空一大塊。家庭機殼選 mATX 安靜款即可。

---

## 💰 建議改成這份 NT$ 32,000 內 final spec

| 項目 | 推薦 | 價格 | 為何選 |
|---|---|---|---|
| CPU | AMD Ryzen 5 8600G（含 Radeon 780M 內顯 + 風扇） | $5,990 | 6 核 12 緒、65W、**內顯就能順跑 Minecraft 1080p**、Zoom/Excel 完全無壓；省掉獨顯這條最大支出 |
| MB | ASUS PRIME A620M-K-CSM | $2,890 | mATX、AM5、DDR5、5 年保；家用足夠（不需要 B650 的 PCIe 5.0） |
| RAM | Crucial Pro DDR5-5600 32GB (16×2) | $3,290 | 5600 是 8600G 內顯甜蜜頻率（內顯共用 RAM，速度影響遊戲 FPS）；32GB 多開瀏覽器/Zoom/Excel 完全夠 |
| SSD | Crucial P3 Plus 1TB Gen4 | $2,090 | 5000 MB/s、5 年保；家用容量足；P3 Plus 是 QLC 但家用讀寫量低、不會掉速 |
| GPU | **取消（用 8600G 內顯）** | **$0** | Minecraft 用 780M iGPU；省下 7-8k 直接歸還 buffer |
| PSU | Antec NeoECO NE500G M 500W 金牌全模 | $1,990 | 65W CPU + 內顯 → 350W 就夠，500W 留升級空間；金牌 7 年保 vs Galaxy 銅牌雜牌差太多 |
| Case | 聯力 Lian Li LANCOOL 205M mATX | $1,790 | mATX 小機殼、安靜、附 2 個風扇、家裡擺得住；不要 DA601 那種大電競殼 |
| Cooler | 用 CPU 原廠 Wraith Stealth 風扇 | $0 | 8600G 65W 原廠扇就夠壓；Noctua NH-U12S（$2,300）對 65W APU 是奢侈品 |
| **TOTAL** | | **$18,040** | **剩 $13,960 buffer** — 可加 27" 文書螢幕（$4,500）+ 鍵盤滑鼠（$1,500）+ Wi-Fi 6 卡（$500）+ 上門組裝（$1,200）+ 還有 $6k 餘 |

---

## 📊 Use-case 適配度

**Primary use**：小孩 Minecraft（休閒）+ 線上課 + 媽媽 Excel + Zoom

| 需求 | 建議配置滿足度 |
|---|---|
| Minecraft Java 版 1080p 60+ FPS | ✅ 780M 實測中畫質 60-90 FPS |
| 線上課（Google Meet / Teams） | ✅ 6 核 12 緒、32GB RAM 多開無壓力 |
| Zoom 視訊會議 + 多分頁 Excel | ✅ APU + 32GB 同時開 10+ 分頁 + Zoom 不卡 |
| 噪音（家庭用） | ✅ mATX 小殼 + 原廠扇 65W 安靜 |
| 升級空間 | ✅ 之後小孩想玩更重的遊戲，直接加一張 RX 7600 / RTX 5060 即可 |
| 耐用 / 安全 | ✅ Antec 金牌 PSU 7 年保，不像 Galaxy 風險 |

**為什麼不堅持原單**：原單真實價值約 NT$ 25,000-27,000，**但功能只比建議配置多「能跑大型 3A 遊戲」這一項，而小孩玩的是 Minecraft**。多花的 6-9k 沒用上。

---

## ⚠️ 還沒解的 risk

1. **如果小孩之後想玩《我的世界》Java 版的高解析 shader 包**（光追 mod），780M 會跑不動 → 那時再加一張 RX 7600（$8,000）即可，500W 金牌電源已預留空間
2. **如果小孩會玩其他遊戲**（Roblox / Fortnite / Valorant）：請現在告訴媽媽，會影響 GPU 取捨。Valorant / Roblox iGPU 可跑，Fortnite 中高畫質要獨顯
3. **PSU 500W 是否夠未來升 5060** → 5060 TDP 145W + 65W CPU + 30% = 273W，500W 金牌完全夠
4. **Crucial P3 Plus 是 QLC**，重度讀寫工作站不適合；家用文書 + Minecraft 完全沒問題

---

## 🛒 採購建議

- **原價屋（coolpc.com.tw）**：菜單直接貼上估價，含上門組裝 $1,200-1,500。家庭用首推這條（不會排線也沒關係）
- **欣亞（sinya.com.tw）**：實體店面，媽媽可帶小孩到現場驗機，台北/新北/台中都有門市
- **autobuy.tw**：促銷檔便宜 3-5%，但要自己組（不建議家庭用）
- **套裝機對比**：PCHome 同等 8600G + 32GB + 1TB 套裝約 $25,000-28,000（無 32GB RAM 多半縮成 16GB），自組省 $7-10k 而且配置可控

### 🎯 一句話建議給媽媽

> **不要買原單**。把 R5 8400F 換成 R5 8600G、拿掉 RX 6650 XT、PSU 換 Antec 金牌、機殼換小一點，總價降到 18k，多出來的錢去買 27" 螢幕跟鍵盤滑鼠套組，整套小孩+媽媽都用得舒服。原單花 32k 只是讓小孩可以「玩沒在玩的 3A 遊戲」。
