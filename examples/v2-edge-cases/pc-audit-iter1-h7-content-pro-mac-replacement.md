# PC Build Audit · h7-content-pro-mac-replacement

> Persona：影視導演，Mac Pro 換 Windows 工作站，要 32-ch RAM + 多 GPU 渲染
> Budget：NT$ 180,000

---

## 🚨 必修 BLOCKER

### BLOCKER 1：散熱器列了兩個，且 SFF AIO 規格不夠壓 7960X 350W

菜單同時列 **Noctua NH-U14S TR5-SP6**（air, 140mm 塔散）與 **Asetek 645LT TR5**（92mm SFF AIO）。一顆 CPU 只能裝一個散熱器。更嚴重的是：

- **Asetek 645LT 是 92mm 單冷排 SFF AIO**，原廠定位是小機殼工作站，sustained 350W TR 渲染負載會撞 thermal limit 降頻
- **Noctua NH-U14S TR5-SP6 雖然有官方背書到 TR 7000，但 7960X 350W 全核渲染**仍會逼到 89-92°C，沒有 thermal headroom

→ **Fix path A（推薦）**：改 **Silverstone XE360-TR5 / Arctic Liquid Freezer III Pro 420 (sTR5 bracket)** 360-420mm AIO，壓 350W 才有空間
→ **Fix path B**：保留 NH-U14S TR5-SP6（air，可靠不漏液），接受 sustained render 約 -5% 性能；機殼風扇要全裝滿（前 3×140 / 頂 3×140 / 後 1×140）

### BLOCKER 2：預算超支 ~14% (~NT$25,000)

依 coolpc / autobuy 2026-06 真實報價推估：

| 項目 | 真實價（NT$） |
|---|---|
| TR 7960X | 54,700 (coolpc) |
| TRX50-SAGE WIFI | 29,990 (coolpc) |
| G.Skill Zeta R5 128GB DDR5-6400 ECC R-DIMM | ~26,000 (TW 平輸) |
| Samsung 990 Pro 4TB | ~16,000 |
| Crucial T700 2TB Gen5 | 11,999~13,000 |
| 散熱（取一個 AIO 360） | ~8,500 |
| RTX 5080 16GB | ~42,000 (均價) |
| Asetek 645LT（重複，拿掉） | — |
| Phanteks Enthoo Pro 2 | ~6,000 |
| Seasonic Prime PX-1300 ATX 3.1 | ~10,000 |
| **合計** | **~204,190** |

→ 超支約 **NT$24,000**。三條路：
- **Fix path A**：CPU 降階 → **TR 7960X → TR 7960X 維持**，但把 RAM 降到 **64GB (2×32)** + RTX 5080 改 **RTX 5070 Ti 16GB**（省 ~NT$15k）
- **Fix path B**：用 **Threadripper 7960X PRO** 退一階到 **TR 7960X 不變**，**PSU 降 1000W ATX 3.1 Gold** 省 NT$4k、SSD 改單顆 4TB Gen4（拿掉 T700）省 NT$13k → 剛好回到預算內
- **Fix path C**（最佳 CP）：**直接放棄 sTR5 平台**，改 **AM5 Ryzen 9 9950X (16C/32T) + X870E**，省 NT$50k+ 給 GPU 升級到 **RTX 5090 32GB**（影視導演 GPU 渲染 VRAM 比 CPU 核心更關鍵）

### BLOCKER 3：Persona 是「多 GPU 渲染」但只配 1× RTX 5080

TRX50-SAGE 有 **7×PCIe 5.0 x16 slots**，是為了 2-4 GPU 渲染農場存在。只配 1 張 5080 完全浪費這個 platform 的特性——形同花 NT$30k 買頂級 workstation 板只用 1 條 slot。

更糟：**RTX 5080 只有 16GB VRAM**，對影視導演用 DaVinci Resolve / Unreal / Octane / Redshift 渲染高解析素材是硬瓶頸（4K RAW / 8K timeline 常吃 20GB+ VRAM）。

→ **Fix path A**：單卡升 **RTX 5090 32GB**（~NT$95,000）→ 全預算炸裂，建議調高 budget 到 NT$ 240,000
→ **Fix path B**：保持單卡但選 **RTX 5080 SUPER 24GB**（若 2026 H2 已上市，待查確認）
→ **Fix path C**：**2× RTX 5070 Ti 16GB**（~NT$56,000 兩張），多 GPU 渲染 Octane / Redshift 線性 scale，但單卡 VRAM 仍 16GB

---

## 💰 修正版 final spec（採 Fix path B 路線：保留 sTR5 平台 + 單 5080 起步，留升 2nd GPU 空間）

PSU math line（含未來 2nd GPU 餘裕）：
```
TR 7960X 350W + RTX 5080 360W = 710W × 1.3 = 923W → 950W 起跳
未來加 2nd RTX 5070 Ti 300W → 1010W × 1.3 = 1313W → 1300W 剛好
```
→ Prime PX-1300 ATX 3.1 留作多 GPU 升級用 **合理**。

| 項目 | 推薦 | 價格 NT$ | 為何選 |
|---|---|---|---|
| CPU | AMD Ryzen Threadripper 7960X 24C/48T | 54,700 | sTR5 平台、32ch RAM 必要條件、DaVinci/Premiere CPU 多核解碼吃滿、影視導演 case 合理 |
| MB | ASUS Pro WS TRX50-SAGE WIFI | 29,990 | 4×R-DIMM ECC、7×PCIe 5.0、10GbE+2.5GbE+Wi-Fi 7、CEB form factor、保留多 GPU 升級 |
| RAM | G.Skill Zeta R5 Neo 128GB (4×32) DDR5-6400 ECC R-DIMM | 26,000 | **必查 TRX50-SAGE QVL**；R-DIMM ECC 是 TRX50 強制規格（一般 UDIMM 不能用） |
| SSD ① OS/系統 | Samsung 990 Pro 2TB (改 2TB 省預算) | 8,300 | Gen4 7450/6900、五年保、4TB 太貴改 2TB |
| SSD ② 素材 | Crucial T700 2TB Gen5（含散熱片） | 13,000 | Gen5 12400MB/s、影視 8K RAW timeline scrub 用、含散熱片避免降速 |
| GPU | NVIDIA RTX 5080 16GB（先單卡，預留 2nd 升級） | 42,000 | 影視 GPU 渲染、NVENC 9th gen、未來可加 2nd 5070 Ti 16GB 走 Octane/Redshift 多卡 |
| PSU | Seasonic Prime PX-1300 ATX 3.1 Platinum | 10,000 | 1300W 留給 dual GPU 升級用；原生 12V-2x6；ATX 3.1 spec |
| Cooler | **Silverstone XE360-TR5（360 AIO sTR5 專用）** | 8,500 | 取代菜單原本同時列的 NH-U14S + 645LT；360mm 冷排壓 350W 7960X 才有 thermal headroom |
| Case | Phanteks Enthoo Pro 2（Full Tower） | 6,000 | E-ATX/CEB 支援 TRX50-SAGE、4×PCIe slot 多 GPU、頂部 420mm AIO 位 |
| 風扇補強 | Arctic P14 PWM PST ×3 | 1,500 | 機殼前 / 頂全裝滿，sustained render 散熱不能省 |
| **TOTAL** | | **~199,990** | 仍超支 NT$ 20k，建議調 budget 到 200k 或再砍 |

### 若要硬壓進 NT$180,000：
- SSD ② 拿掉 Crucial T700（改 Samsung 990 Pro 4TB 一顆 ~16,000 取代雙 SSD 配置）→ 省 ~5,000
- RAM 降 **64GB (2×32) DDR5-6400 ECC R-DIMM** ~14,000 → 省 12,000
- PSU 降 **Seasonic Vertex PX-1000 ATX 3.1** ~7,000 → 省 3,000，但放棄 2nd GPU 升級空間

合計再省 ~NT$ 20,000 → **NT$ 179,990**，剛好入界。

---

## 📊 Use-case 適配度

### Primary use：影視導演（DaVinci Resolve / Premiere / Octane / Unreal）+ 32ch RAM + 多 GPU 渲染

| 需求 | 配置對應 |
|---|---|
| 4K/6K/8K timeline scrub | T700 Gen5 + 128GB ECC RAM + 24C CPU |
| GPU 渲染（Octane/Redshift） | RTX 5080 起跳，**未來 slot 5070 Ti 第二張**走多卡 scale |
| ECC 資料安全（重要素材） | TRX50 R-DIMM ECC，影視 RAW 資料防 bitflip |
| 長時間 sustained render | 360 AIO + Phanteks 大塔 thermal capacity |
| 32-channel RAM（需求） | ⚠️ **澄清需求**：TRX50 是 **4-channel R-DIMM**，不是 32-channel；用戶若真要 32-channel 要走 **TR PRO 7965WX + WRX90**（NT$ 87,900 CPU 起跳，預算遠遠不夠）。建議跟用戶確認「32ch」是否誤寫「32GB」或「4-channel 128GB」 |

### 適配亮點
1. sTR5 R-DIMM ECC 跟 Mac Pro 工作流最接近（Mac Pro Intel Xeon W 也是 ECC R-DIMM）
2. 7×PCIe 5.0 slot 將來可塞 2-3 張 GPU 做 Redshift / Octane 多卡渲染農場
3. 24C/48T 對 DaVinci Resolve Fusion / Premiere ProRes 解碼線性 scale

### 升級空間
- 第二張 RTX 5070 Ti / 5090（PSU 已留 buffer）
- RAM 升到 256GB / 512GB（4×64 / 4×128 R-DIMM）
- 第三顆 NVMe 走 PCIe Gen5 M.2 卡

---

## ⚠️ 還沒解的 risk

1. **「32-channel RAM」需求澄清** — TRX50 platform 是 4-channel；32-channel 是 EPYC 9004 / Threadripper PRO 9000 WRX90 等級（CPU 9 萬起，板 6 萬起）。**先跟用戶確認需求**，可能是溝通誤差。
2. **G.Skill Zeta R5 DDR5-6400 在 TRX50-SAGE QVL** — 必查 ASUS 官網 memory support list 比對 part number `F5-6400R3239G32GQ4-ZR5NK`。若不在 QVL，降到 **DDR5-5600 ECC R-DIMM** 100% 保穩。
3. **RTX 5080 只 16GB VRAM 對影視 GPU 渲染偏吃緊** — 4K Octane 場景常爆 VRAM；若預算允許強烈建議 RTX 5090 32GB（要拉到 NT$ 240k 預算）。
4. **Phanteks Enthoo Pro 2 對 TRX50-SAGE CEB form factor 相容性** — CEB 比 E-ATX 還寬，需確認機殼 MB tray 標 CEB 支援（Enthoo Pro 2 spec sheet 標 SSI-EEB / E-ATX，CEB 通常可裝但部分鎖點需自行錯位）。
5. **Asetek 645LT** 若用戶堅持留用，請確認他是不是要放 SFF 機殼（如 Streacom DA6XL）而不是 Phanteks Enthoo Pro 2——兩者用途完全衝突。

---

## 🛒 採購建議

- **原價屋（coolpc.com.tw）**：TR 7960X、TRX50-SAGE、PSU、機殼一站購齊；可指定上門組裝（sTR5 平台組裝費 ~NT$2,000-3,000，建議付，TR 散熱壓 IHS 力道與 RAM training 較複雜）
- **欣亞（sinya.com.tw）**：實體可現場驗 CPU 邊角是否完整（TR 大尺寸 LGA 容易彎針）
- **G.Skill Zeta R5 ECC R-DIMM**：TW 通路稀少，可能要走 **Amazon 平輸**（保固територ 限美國，但 G.Skill 終身保多半接受 RMA）或 **GH3C 國際物流**
- **Silverstone XE360-TR5**：原價屋有貨，比 Asetek 645LT 適合大塔
- **套裝機對比**：Puget Systems / BIZON 同 spec 報價 USD $5,500-7,000（~NT$ 175,000-220,000）含 3 年到府保固，自組省 NT$ 20-40k 但要自己負責 RMA 跑流程
- **不建議走水貨 5080**：保固在台灣只剩 1 年（原廠 3 年），影視工作站不值得省這筆

---

## 📝 引用來源

- TR 7960X 報價 NT$54,700：PCDIY! online [`http://www.pcdiy.com.tw/detail/27457`](http://www.pcdiy.com.tw/detail/27457)
- TRX50-SAGE WIFI 報價 NT$29,990：原價屋開箱文 [`https://www.coolpc.com.tw/tw/shop/motherboard/asus-pro-ws-trx50-sage-wifi/`](https://www.coolpc.com.tw/tw/shop/motherboard/asus-pro-ws-trx50-sage-wifi/)
- RTX 5080 均價 NT$42,000+：原價屋 5090/5080 上市文（均價超過 4 萬元）
- TR 7960X TDP 350W：TechPowerUp CPU database
- Crucial T700 2TB Gen5 NT$11,999~13,000：原價屋促銷文

> 🟡 **2026 SSD/RAM HBM 紅利期 baseline**：因 HBM3e + AI 訓練卡需求佔走 NAND/DRAM 產能，2026 SSD/DDR5 售價相對 2023 +30~50%。990 Pro 4TB NT$16k、T700 2TB NT$13k 屬合理區間；ECC R-DIMM 128GB ~NT$26k 是 TRX50 平台特有溢價（一般 DDR5 UDIMM 128GB 約 NT$14-16k，但不能用在 TRX50）。
