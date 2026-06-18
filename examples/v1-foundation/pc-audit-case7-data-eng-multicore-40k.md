# PC Build Audit — case7-data-eng-multicore-40k

> Persona：36 歲 data engineer，家裡跑 Spark/Airflow local dev + 偶爾 ML notebook，multi-core priority
> Budget：NT$ 40,000
> 評估日期：2026-06-19

---

## 🚨 BLOCKER

**沒有相容性 BLOCKER**（AM5 + B650 chipset ✓、DDR5 ✓、mATX MB 進 mATX 機殼 ✓、750W Gold 充裕 ✓、塔散 TDP 對得上 R9 7900 65W ✓）。

但有一個**嚴重預算 BLOCKER**：

- 原菜單估算總價 **約 NT$ 49,800**，超出預算 **約 NT$ 10,000（+25%）**
- 主要超支來自 Crucial T700 Gen5 SSD（$6,499）+ Sapphire RX 7700 XT（$13,500）兩件
- 對 Spark/Airflow/notebook 工作流，這兩件都過頭 — Gen5 SSD 對 ETL pipeline 無感（瓶頸在 CPU/RAM/網路），RX 7700 XT 對偶爾 ML 而言 ROCm 生態仍不成熟（PyTorch 主流仍 CUDA）

### Fix path（推薦走 A）

- **Path A（保 R9 7900 + 64GB RAM，砍 GPU + SSD）**：T700 Gen5 → SN850X Gen4 1TB；RX 7700 XT → RTX 5060 Ti 8GB 或無獨顯走內顯 → 進 $40k 內
- **Path B（保 GPU 走 ML 路線）**：CPU 降 R7 7700（8C/16T）、RAM 降 32GB、SSD 改 Gen4 → 但 multi-core priority 矛盾，不建議

---

## 💰 NT$ 40,000 內 final spec（Path A — Data Eng 取向）

| 項目 | 推薦 | 價格 | 為何選 |
|---|---|---|---|
| CPU | **AMD Ryzen 9 7900 MPK**（含風扇盒裝）| $12,470 | 12C/24T，65W TDP，Spark/Airflow local executor 多核全開最甜；MPK 盒裝原廠扇可救急 |
| MB | ASRock B650M PG Lightning WiFi（保留原選）| ~$4,200 | mATX、AM5、DDR5、Wi-Fi 6E、2× M.2，配 R9 7900 65W 無 VRM 壓力 |
| RAM | G.Skill Flare X5 DDR5-6000 64GB (2×32) CL30 EXPO（保留）| ~$7,000 | 64GB 給 Spark local executor + Docker + JVM heap 不卡；AM5 甜蜜點 6000 CL30 |
| SSD | **WD Black SN850X 1TB Gen4**（**改換**）| ~$3,200 | Gen4 7,300MB/s 對 Spark shuffle / parquet I/O 已飽和；省 $3,300 進預算 |
| Cooler | Thermalright Peerless Assassin 120（保留）| ~$1,300 | 雙塔 TDP 245W，壓 R9 7900 65W 綽綽有餘，全核 boost 不降頻 |
| GPU | **無獨顯 / 暫不買**（**改換**）| $0 | R9 7900 內建 RDNA2 iGPU 可亮機；ML notebook 用 Colab/雲端，省下 $13k 進預算 |
| Case | MSI MAG Forge M100R（保留）| ~$1,790 | mATX 玻璃側、支援 240mm AIO（之後升級用）、走線 OK |
| PSU | MSI MAG A750GL PCIE5 750W Gold 全模（保留）| ~$2,890 | ATX 3.1、原生 12V-2x6、10 年保；未來加 GPU 也撐得住 |
| **TOTAL** | | **~NT$ 32,850** | 留 **~$7,150 buffer**，可加：(1) RTX 5060 Ti 8GB ~$11k 當未來升級頭金，或 (2) 第二顆 SSD 做 raw data，或 (3) 留現金等 GPU 跌價 |

> 替代方案：若**真的**想保獨顯（出機就要 ML 試水）→ 把預算拉到 ~$42-43k 加 **RTX 5060 Ti 16GB ~$13.5k**（CUDA 生態 + 16GB VRAM 跑 Llama 3.1 8B Q4），比 RX 7700 XT 對 ML dev 實用太多。RX 7700 XT 對 Spark/Airflow workload 一秒都用不到，買它純浪費。

---

## 📊 Use-case 適配度

- **Primary use**：Data engineering（Spark/Airflow local dev）+ 偶爾 ML notebook
- **適配亮點**：
  - **12C/24T R9 7900 + 64GB DDR5-6000**：Spark local mode 多 executor 平行、Airflow DAG backfill、pandas/Polars 大資料 in-memory 全部吃滿
  - **Gen4 SN850X 1TB**：parquet/orc 讀寫 + Docker volume + WSL2 layered fs 速度感無差，Gen5 的 12,400MB/s 對 Spark shuffle 無實質意義（瓶頸在 CPU/序列化）
  - **65W R9 7900**：在家長時間 burn-in，電費 + 散熱壓力都小，PA120 全核穩定不降頻
- **取捨**：捨 RX 7700 XT 換 12C CPU + 64GB RAM，符合 "multi-core priority" 明確需求。ML 短期走 Colab Pro ($10/月)、Lightning AI、或 Kaggle 免費 T4，比硬塞 RX 7700 XT 划算
- **未來升級空間**：(1) 加 RTX 5060 Ti 16GB 進 ML local；(2) PSU 750W 已留瓦數預算；(3) MB 還有 1 條 M.2 + 4 條 SATA 可擴展冷儲

---

## ⚠️ 還沒解的 risk

- **R9 7900 MPK 盒裝原廠扇**：MPK 版（Multi-Pack）拆裝原廠 Wraith Prism 扇壓 65W 沒問題但吵，**不要用原廠扇**，直接上 PA120
- **B650M PG Lightning WiFi 實際價**：原價屋 / 欣亞當前報價需現場確認，估 ~$4,000-4,500 區間；若 > $4,500 可換技嘉 B650M GAMING X AX（同級）
- **無獨顯時 iGPU 輸出**：B650M PG Lightning WiFi 帶 HDMI + DP，R9 7900 iGPU 只能 4K@60Hz 文書，不能玩遊戲；若有雙螢幕需求要確認 MB 同時點亮兩個輸出 OK
- **DDR5 2026 漲價**：64GB CL30 EXPO 套裝 2026 Q2 比 2024 漲 ~40%，現估 $7,000 但近期可能再上下浮動 $500
- **RAM EXPO profile**：BIOS 開 EXPO I 才能跑 6000 CL30，不開 default JEDEC 4800 損失 20% Spark 效能

---

## 🛒 採購建議

- **原價屋（coolpc.com.tw）**：菜單貼上自選介面，**指定 Path A 配置**，加購上門組裝 $800-1,500（在家自組 R9 7900 + PA120 不難但 PA120 扣具略硬）
- **欣亞（sinya.com.tw）**：板橋 / 中和 實體店，現場驗 MB 盒（B650M PG Lightning WiFi 確認 WiFi 版而非無 WiFi 版差 $400）
- **autobuy.tw**：MSI MAG Forge M100R 白色款常促銷 $1,790；MSI A750GL 偶爾 $2,690 限時殺
- **GPU 緩買策略**：先出機跑 Spark/Airflow 驗工作流是否真用得到 GPU，1-2 個月後再決定 5060 Ti 16GB（NV LLM 路）或繼續走雲端
- **PCHome 24h 套裝對比**：同 spec 套裝（不含 GPU）約 $36-38k，自組省 $3-5k 但要會排線 + 跑 memtest86 + Cinebench 全核 stress 30 分鐘確認散熱

---

**結論**：原菜單方向對（multi-core CPU + 64GB RAM）但預算超支 $10k 主因塞了用不到的 Gen5 SSD + RX 7700 XT。砍這兩件改 Gen4 SSD + 暫無獨顯，總價 ~$32.8k 進預算，留 $7k buffer 等 GPU 跌價或補 5060 Ti 16GB 走 LLM dev 路。
