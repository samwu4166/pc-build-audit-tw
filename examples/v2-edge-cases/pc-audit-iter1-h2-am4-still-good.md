# PC Audit — AM4 平台 GPU-only 升級 (h2-am4-still-good)

> Persona: 32 歲老用戶，留 AM4 平台、只升 GPU，預算 NT$22,000
> 現有: R5 5600X + B550 + DDR4-3200 16GB + WD SN550 1TB + Cougar VTX 600W

---

## 🚨 必修 BLOCKER

### BLOCKER #1 — GPU 選擇：RX 7600 XT 16GB 在 2026-06 已不是 CP 值最佳解

RX 9060 XT 16GB (RDNA4，2025-06 上市) **直接取代** RX 7600 XT 16GB：

- 原價屋上市報價：**NT$12,490 起** (RX 9060 XT 16GB)
- 對比 RX 7600 XT 40 款遊戲 2K 解析度**領先 46%** (來源：原價屋上市報價文)
- 對比 RTX 5060 Ti 8GB 也領先 15%
- 同樣 16GB VRAM、同價格帶 → **沒有理由選 7600 XT**

> 來源：原價屋 Coolpc《【上市報價】FHD/2K 主流市場新霸主！AMD Radeon RX 9060 XT 8/16GB》

**Fix path A（推薦）**：改買 **ASRock / PowerColor RX 9060 XT Challenger 16GB**，預算約 NT$12,490–13,990
**Fix path B**：若市場缺貨堅持 7600 XT，砍到 NT$11,500 以下才合理（已是上一代尾貨）

### BLOCKER #2 — Cougar VTX 600W 撐 RX 9060 XT 邊緣值，要評估換 PSU

PSU math：
```
5600X (65W TDP) + RX 9060 XT (~180W TGP) + 30% headroom
= 245W × 1.3 = 318W → 推 500W 起跳
```
帳面上 600W 夠，但：
- Cougar VTX 是 **80+ Bronze**（非 Gold），效率 ~85%
- 已用數年（5600X + B550 + SN550 是 2020-2021 配置 → PSU 至少 4-5 年）
- 電容老化後實際輸出衰減 10-15%

**Fix path A**：先量測 PSU 年齡 / serial，若超過 5 年強烈建議換
**Fix path B（安全）**：預算內塞 **海韻 Focus GX-650 / 全漢 Hydro G PRO 650W 80+ Gold ATX 3.1**，約 NT$2,790–3,290，順便拿到 12V-2x6（未來升 NVIDIA 50 系列備用）
**Fix path C（最省）**：維持現有 PSU，但接受未來無法升 RX 9070 / 5070 Ti

---

## ⚠️ Hard truth: AM4 平台是 dead-end upgrade path

- AM4 socket 已 EOL (Ryzen 5700X3D 是最後一波 BIOS 釋出)
- 升頂規 CPU 也只能到 **5800X3D / 5700X3D**（gaming 甜蜜點），data eng / 多核需求受限
- 你這次升 GPU 是「續命 2-3 年」決策，**不是長期投資**
- 接下來下一次升級就是**整平台換 AM5**（CPU + MB + DDR5 RAM 全換）

→ 這次只投錢在「最值得」的零件：GPU + 散熱 + (可能) PSU

---

## 💰 預算 NT$22,000 內 final spec（修正版）

### 方案 A：保守續命（換 GPU + 散熱，PSU 賭一把）

| 項目 | 推薦 | 價格 | 為何選 |
|---|---|---|---|
| CPU | R5 5600X（現有） | $0 | 6C12T、65W TDP、AM4 主流甜蜜點，1080p gaming 不瓶頸 |
| MB | B550（現有） | $0 | 支援 PCIe 4.0 x16，9060 XT 滿速跑 |
| RAM | DDR4-3200 16GB（現有） | $0 | 主流 1440p gaming 夠用；如做 LLM dev 才考慮升 32GB |
| SSD | WD SN550 1TB（現有） | $0 | Gen3 NVMe，2026 標準偏低但夠 OS + 遊戲 |
| GPU | **ASRock RX 9060 XT Challenger 16GB OC** | $12,990 | 16GB VRAM、RDNA4、比 7600 XT +46% (2K)、原生 DP 2.1 |
| Cooler | **DeepCool AK620**（你寫「ID-Cooling AK620」應為筆誤，AK620 是 DeepCool 家） | $2,190 | 雙塔 6 熱管、TDP 260W、壓 5600X 過剩，未來升 5800X3D 也 ok |
| Case | Antec NX410 ATX | $1,790 | 前 mesh 風流佳、附 3×ARGB 風扇、GPU 長度支援 405mm（9060 XT ~280mm 綽綽有餘） |
| PSU | Cougar VTX 600W（現有） | $0 | 帳面夠用；**接受老化風險** |
| **小計** | | **$16,970** | 餘 **$5,030** buffer |

### 方案 B：穩健續命（連 PSU 一起換，這次到位）— **強烈推薦**

| 項目 | 推薦 | 價格 | 為何選 |
|---|---|---|---|
| GPU | ASRock RX 9060 XT Challenger 16GB OC | $12,990 | 同上 |
| Cooler | DeepCool AK620 | $2,190 | 同上 |
| Case | Antec NX410 ATX | $1,790 | 同上 |
| **PSU** | **海韻 Focus GX-650 ATX 3.1 80+ Gold** | $2,990 | 650W、ATX 3.1 / 12V-2x6 原生線、10 年保 |
| **小計** | | **$19,960** | 餘 **$2,040** buffer（組裝 / 散熱膏 / 雜項） |

---

## 📊 Use-case 適配度

- **Primary use（推測）**：1080p / 1440p gaming + 偶爾生產力（32 歲老用戶 + AM4 留用 → 多半是 gaming + 日常）
- **適配亮點**：
  - 9060 XT 16GB → 1440p 主流 3A 大作 60+ FPS，VRAM 不會卡（Hogwarts、Cyberpunk 2.x 都吃 12GB+）
  - AK620 → 5600X 全核 boost 不降頻，未來升 5800X3D 也接得住
  - NX410 mesh 前面板 → 5600X + 9060 XT 雙烤溫度可控
- **不適合**：
  - LLM dev / inference → 16GB VRAM 夠，但 16GB RAM 不夠，要加到 32GB（AM4 DDR4 還算便宜）
  - 4K gaming → 這顆 GPU 不到 4K 等級
- **未來升級空間**：
  - CPU 可升 5700X3D / 5800X3D（gaming +15-25%）約 NT$7-9k
  - RAM 加滿到 32GB 約 NT$1,500
  - **不要再升 GPU 更高階** → 會被 5600X 拖死

---

## ⚠️ 還沒解的 risk

1. **Cougar VTX 600W 年齡**：若 >5 年 + 重度使用，2026 接 9060 XT 高負載時可能跳機 / 重啟。買回來先在 PSU 標籤拍 serial 查製造日。
2. **B550 BIOS 版本**：9060 XT 不需要新 BIOS（PCIe 4.0 標準支援），但建議升到 MB 廠最新 AGESA ComboPI 1.2.0.x（順便讓未來換 5700X3D 也能用）。
3. **B550 PCIe lane sharing**：9060 XT 用主 x16 槽，若同時插第二顆 M.2 在 chipset lane 上沒影響；但若 M.2_2 走 CPU lane（看 MB 型號）會降 GPU 到 x8。9060 XT x8 損失 <2%，可忽略。
4. **DDR4-3200 16GB**：1440p gaming 沒問題，但若同時開 Chrome 50 分頁 + 遊戲會吃緊。加錢升 32GB 約 NT$1,500（同型號雙通道）。
5. **散熱膏**：5600X 重新拆裝要新散熱膏（信越 7921 / MX-6 約 NT$200-300）。
6. **筆誤確認**：你寫「ID-Cooling AK620」— **AK620 是 DeepCool 家的型號**，ID-Cooling 對應級距是 **SE-226-XT / FROZN A620** 之類。如果你確實是要 ID-Cooling，列「待查 — ID-Cooling 沒 AK620 這型號」。

---

## 🛒 採購建議

- **原價屋（coolpc.com.tw）**：菜單貼上自選，9060 XT 上市文已公開報價 NT$12,490 起；可指定上門組裝（$800-1500）
- **欣亞（sinya.com.tw）**：實體現場驗 9060 XT 風扇 / 燈效
- **autobuy.tw**：散熱器（AK620）促銷檔常有殺到 NT$1,990
- **PSU 別買水貨**：海韻 / 全漢 一律本島代理保固（10 年）；蝦皮平輸保固只 1-3 年差很多
- **9060 XT 品牌建議優先序**：ASRock Challenger > PowerColor Hellhound > Sapphire Pulse；Acer 那批通常便宜但保固通路偏弱

---

## 📌 結論一句話

**改買 RX 9060 XT 16GB 取代 7600 XT、PSU 順便換掉，總價 NT$19,960，留 2K buffer。** AM4 平台只剩 2-3 年壽命，這次當「續命投資」，下次升級直上 AM5。

---

### Audit checklist
- [x] CPU socket vs MB chipset：AM4 5600X + B550 ✓
- [x] RAM gen：DDR4 ✓ (B550 only DDR4)
- [x] PSU math 印出：5600X 65W + 9060 XT 180W = 245W × 1.3 = 318W → 500W+
- [x] Case form factor：ATX NX410 容得下 ATX MB + 9060 XT ~280mm
- [x] Cooler TDP：AK620 260W ≥ 5600X 65W ✓
- [x] 2026 行情驗價（Brave）：9060 XT NT$12,490 起、AK620 NT$2,190、NX410 NT$1,790
- [x] 2026 SSD/RAM HBM callout：本案不換 RAM/SSD，跳過
- [x] AM4 dead-end upgrade path 警告
- [x] PSU 老化風險 callout
- [x] Used / 水貨警告（PSU 段）
- [x] 引用具體連結：原價屋 9060 XT 上市報價文
