## 積體電路 (Integrated Circuit, IC) 的基礎概念
- **定義**: 積體電路 (Integrated Circuit, 簡稱 IC) 是將大量的電子元件如電晶體 (Transistor) 與互連線路 (Interconnects)，共同製造在一小塊半導體基板 (Semiconductor substrate) 上的技術。
- **與傳統離散電路的差異**:傳統由獨立零件組成的離散電路 (Discrete circuit) 會佔用較多電路板空間、導線較長，且有較多的寄生效應 (Parasitics)。相反地，IC 具備體積極小、走線短、高密度、高速度與低功耗等優勢，這也是它能改變電子產業的原因。
##  電晶體 (Transistor) 的開關原理
- **數位核心功能**: 在數位晶片設計中，電晶體主要扮演「可控制的開關 (Controllable switch)」：關閉 (OFF) 狀態代表邏輯 0，導通 (ON) 狀態代表邏輯 1。
- **NMOS (N型金氧半導體)**: 當控制端，也就是閘極 (Gate) 接收到高電位 (邏輯 1) 時，電晶體會導通。它非常擅長傳遞邏輯 0 (強下拉能力)，因此常被連接到接地端 (Ground)，作為電路中的「下拉網路 (Pull-down networks)」。
- **PMOS (P型金氧半導體)**:  當閘極 (Gate) 接收到低電位 (邏輯 0) 時會導通。它擅長傳遞邏輯 1 (強上拉能力)，通常會連接到電源端 (VDD)，作為電路中的「上拉網路 (Pull-up networks)」。
## 超大型積體電路 (VLSI) 的演進與定義
- **整合度演進**: 晶片發展的核心趨勢，就是將越來越多的電晶體塞進單一晶片中。規模從早期的小型積體電路 (Small-Scale Integration, SSI，單片約 1~10 個邏輯閘)，一路發展到現代的超大型積體電路 (Very-Large-Scale Integration, VLSI) 與極大型積體電路 (Ultra-Large-Scale Integration, ULSI)。現代極大型晶片單片甚至可包含十萬至超過十億個邏輯閘 (Logic gates)。
- **VLSI 定義**: VLSI 意指將極大量的電晶體整合在單一晶片上，藉此設計並實現複雜的電子系統 (Electronic systems)。
- **應用範疇**: 現代的處理器 (Processor)、人工智慧加速器 (AI accelerator)、記憶體 (Memory)、圖形處理器 (GPU) 以及系統單晶片 (System-on-Chip, SoC) 皆屬於 VLSI 的範疇。這項技術綜合了元件物理 (Device physics)、數位邏輯 (Digital logic)、架構 (Architecture)、驗證 (Verification)、佈局 (Layout) 與製造限制 (Manufacturing constraints) 等多面向的專業。
## 什麼是 CMOS?
- **定義**: CMOS 的全名是互補式金屬氧化物半導體 (Complementary Metal-Oxide-Semiconductor, CMOS)。
- **互補動作 (Complementary action)**: 它是將 PMOS 與 NMOS 兩種電晶體元件結合在一起，用來實現數位邏輯閘 (Logic gates)
- **工作原理 (以反相器 Inverter 為例)：**
    - 當輸入端為邏輯 0 時，控制上拉的 PMOS 會導通，而下拉的 NMOS 關閉，將輸出端拉高至電源端 (VDD)，產生邏輯 1。
    - 當輸入端為邏輯 1 時，PMOS 會關閉，而 NMOS 導通，將輸出端往下拉至接地端 (GND)，產生邏輯 0。
- **優勢：** 因為這種互補的開關特性，CMOS 電路具備低功耗運作 (Low power operation) 的優良特質。
## VLSI 與 CMOS 的差異與關聯 (VLSI vs CMOS)
- **VLSI (超大型積體電路)**: 代表的是「設計與整合的層次 (Design and integration level)」。它指的是將極大量的電晶體組合成複雜數位系統的概念，涵蓋了從規格制定、架構、暫存器傳輸級 (RTL)、驗證到實體佈局 (Physical layout) 的完整設計流程。
- **CMOS**: 則是一種「電晶體製造技術 (Transistor technology)」。它結合了 NMOS 與 PMOS，是目前實現現代數位 IC 最主流的底層技術。
- **核心觀念總結**: VLSI 是我們正在「設計」的龐大系統，而 CMOS 是用來「製造」這個系統所使用的底層技術。現代大多數的 VLSI 晶片 (如 CPU、GPU、SoC 等) 都是基於 CMOS 技術打造的。
## 為什麼 CMOS 能成為主流技術？(Why CMOS Became Dominant)
- CMOS 能夠成為主宰市場的技術，是因為它在密度、功耗、速度與可製造性 (Manufacturability) 之間取得了強大的平衡：
- **低靜態功耗 (Low static power)**: 在穩定狀態下 (沒有切換動作時)，只會產生極小的直流電流。
- **高密度 (High density)**: 極小的晶片面積內可以容納非常多個電晶體。
- **良好的雜訊邊際 (Good noise margin)**: 能夠更可靠、清晰地分辨邏輯 0 與邏輯 1 的訊號狀態。
- **具備微縮性 (Scalable)**:這種技術架構能夠適應微縮化，跨越許多世代的製程技術持續發展。
- **高效能 (High performance)**: 透過精心的設計，能夠達到極快的開關切換速度。
- **製程成熟 (Mature process)**: 擁有龐大的產業生態系 (Ecosystem) 與豐富的設計經驗 (Design know-how)。
## 不同的硬體平台概覽
- **微控制器 (Microcontroller, MCU)**：適用於低成本、低功耗的嵌入式控制 (例如 STM32, Arduino)。
- **中央處理器 (CPU/MPU)**: 用於通用的軟體處理，具備高效能並能運行複雜的作業系統 (例如 Intel, ARM)。
- **FPGA**: 具備可重組的硬體架構，適合用於客製化硬體與原型開發
- **ASIC**: 專為單一應用打造的客製化晶片
## 什麼是 ASIC？(What Is an ASIC?)
- **定義：** ASIC 的全名為特殊應用積體電路 (Application-Specific Integrated Circuit)，是專為特定的產品、演算法或應用所客製化設計的晶片
- **常見範例**: AI 加速器、影片編解碼晶片、智慧型手機數據機 (Modem)、網路交換器晶片等。
- **優點**: 具備最高效能、最低功耗與極小的面積，且在大規模量產 (High-volume production) 時單位成本較低。
- **限制**: 初期設計成本 (Design cost) 非常高，而且一旦進入製造階段 (Fabrication) 後，硬體功能就完全固定，無法輕易更改
## 什麼是 FPGA？(What Is an FPGA?)
- **定義**: FPGA 的全名為現場可程式化邏輯閘陣列 (Field-Programmable Gate Array)。這是一種包含可程式化邏輯與繞線 (Programmable logic and routing) 的晶片。
- **特點**: 它內部由許多可配置邏輯區塊 (Configurable Logic Blocks, CLB) 組成，在製造完成並部署後，仍可以重新程式化 (Reprogrammable) 來改變其硬體功能。
- **用途與缺點**: 非常適合用於原型設計 (Prototyping) 與教育用途，也可以用來加速特定的運算工作。但缺點是，相比於 ASIC，它通常會消耗更多的功耗與佔用更大的晶片面積。
## ASIC 與 FPGA 的關鍵比較 (ASIC vs FPGA)
- 這是一個非常實用的對比，可以用一句話總結：FPGA 適合靈活開發與原型驗證，ASIC 則是最終最佳化的矽晶片解決方案。
- **製造後更改**: FPGA 可以重新配置；ASIC 則是固定不變的
- **初期設計成本**: FPGA 較低；ASIC 較高。
- **大量生產的單位成本**: FPGA 較高；ASIC 較低
- **效能與能源效率**: FPGA 表現不錯，但 ASIC 能達到極高 (Very high) 的水準。
## 什麼是系統單晶片？(What Is a SoC?)
- **概念**: SoC 將許多不同的次系統 (Subsystems) 整合進單一顆晶片中，形成一個完整的系統。
- **組成模組**: 一顆 SoC 通常會包含 CPU、圖形處理器 (GPU)、數位訊號處理器 (DSP)、AI 加速器、記憶體控制器 (Memory Ctrl.)、外部通訊介面 (I/O, 如 PCIe, USB)、安全加密模組 (Security) 與電源管理 (Power Mgmt.) 等各種功能區塊。
- **重要觀念**: SoC 本身通常也就是一種 ASIC（因為它是為了某個特定產品，如某款手機所專門設計的客製化整合晶片）。
## 為什麼需要抽象化？(Why Do We Need Abstraction?)
- 現代晶片太過複雜，無法單靠人工逐一處理每個電晶體。
- 抽象化可以幫助團隊分工，讓工程師能分別專注於架構、RTL、驗證或實體設計等不同領域。
- 抽象化也有助於電子設計自動化 (Electronic Design Automation, 簡稱 EDA) 工具的運作，讓軟體能將高階的硬體描述自動轉換成低階的具體實作。
## VLSI 的各個抽象化層級 (VLSI Abstraction Levels)
- 系統與架構層級 (System and Architecture Levels)
    - **系統層級 (System level)**:主要回答「晶片要做什麼 (What)」，專注於定義整體需要的功能、效能、成本與功耗目標 (例如：打造一顆低功耗的影像處理晶片)。
    -  **架構層級 (Architecture level)**: 主要回答「系統如何組織 (How)」，負責規劃主要的功能區塊 (如 CPU、加速器、記憶體、匯流排等)，並評估不同組織方式的權衡 (Trade-offs)。
- 暫存器傳輸級 (Register Transfer Level, 簡稱 RTL)
    - 這個層級會使用硬體描述語言 (Hardware Description Languages, HDLs，如 Verilog、SystemVerilog 或 VHDL) 來描述硬體的行為。
    - 主要描述暫存器 (Registers) 中儲存的狀態，以及透過組合邏輯 (Combinational logic) 計算後產生的資料移動。
    - **重要觀念**: RTL 程式碼並不是軟體，而是一種硬體描述，最終會被合成出真實的邏輯閘硬體。
- 邏輯閘層級與標準元件 (Gate Level and Standard Cells)
    - RTL 程式碼會被轉換成實際的邏輯閘 (Logic gates，如 AND, OR, NOT) 與正反器 (Flip-flops)。
    - 這些邏輯閘會對應到標準元件庫 (Standard-cell library)，這是一個包含預先設計好邏輯元件的資料庫，每個元件都帶有特定的功能、時序 (Timing)、功耗、面積與實體佈局視圖。
- 電晶體層級 (Transistor Level)
    - 邏輯閘是由 MOS 電晶體所組成的 (例如一個 CMOS 反相器包含一個 PMOS 與一個 NMOS)。
    - 這個層級的具體實作，決定了電路的延遲 (Delay)、功耗與雜訊邊際 (Noise margins) 等關鍵物理特性。
- 實體佈局層級 (Physical / Layout Level)
    - 在這個最終階段，所有的電子元件都會轉化為矽晶片上的幾何形狀 (Geometric shapes)，包含金屬層 (Metal)、多晶矽 (Poly)、擴散區 (Diffusion) 等。
    - 佈局視圖是晶圓代工廠 (Foundry) 用來製造晶片的光罩 (Masks) 的基礎。
    - 在送交製造前，必須進行實體驗證 (Physical verification)：
        - DRC (Design Rule Check，設計規則檢查)：確認佈局是否符合代工廠製造的幾何規則要求 (如最小間距)。
        - LVS (Layout Versus Schematic，佈局與電路圖比對)：確認畫出來的物理佈局是否與預期的邏輯電路 (Netlist) 完全相符。
## 前端設計 (Front-End Design)
前端設計的主要目標是證明邏輯功能正確無誤。
- **涵蓋步驟**: 規格制定 (Specification)、架構設計 (Architecture)、RTL 設計、功能模擬與驗證 (Functional Simulation and Verification)、邏輯合成 (Logic Synthesis)。
- **產出物 (Handoff)**: 驗證過邏輯閘級網表 (Verified netlist)。
## 後端設計 (Back-End Design)
後端設計的主要目標是將邏輯轉換為可製造的實體晶片佈局。
- **涵蓋步驟**: 平面規劃 (Floorplanning)、擺放 (Placement)、時脈樹合成 (Clock Tree Synthesis)、繞線 (Routing)、時序收斂 (Timing closure)、實體驗證 (Physical verification)。
- **產出物 (Handoff)**: GDSII 格式的實體佈局檔案
## 完整的 8 大設計步驟

**1. 規格制定與架構 (Specification and Architecture)**
- **規格 (Specification)**: 定義晶片要做什麼 (What)，包含時脈頻率、面積與功耗預算、輸入與輸出介面等需求。
- **架構 (Architecture)**: 決定系統如何組織 (How)，包含需要哪些區塊、記憶體位置、區塊間如何通訊。

**2. RTL 設計 (RTL Design)**
- 將架構的決定轉換成**可合成的硬體描述 (Synthesizable hardware description)**。
-  使用 Verilog 或 SystemVerilog 等語言來撰寫。

**3. 功能模擬與驗證 (Functional Simulation and Verification)**
- **目的**: 確認 RTL 程式碼的行為是否正確
- **測試平台 (Testbench)**: 負責提供輸入訊號 (Patterns)、時脈與重置訊號，並檢查輸出結果是否符合預期。

**4. 邏輯合成 (Logic Synthesis)**
- 將 RTL 程式碼轉換成對應標準元件庫 (Standard-cell library) 的邏輯閘 (Gates)。
- **產出報告**: 包含面積報告 (Area report)、時序報告 (Timing report) 與功耗估算 (Power estimate)。

**5.  靜態時序分析 (Static Timing Analysis, STA)**
- **目的**: 檢查資料訊號是否能在時脈規定的截止時間前到達目的地。
- **關鍵概念**: 發射與擷取正反器 (Launch/Capture FF)、關鍵路徑 (Critical path)、建立時間 (Setup time) 與保持時間 (Hold time)。

**6. 實體設計 (Physical Design)**
- 將邏輯網表轉換為實體晶片佈局。
- **流程**: 平面規劃 (Floorplan) ➔ 擺放 (Placement) ➔ 時脈樹 (Clock Tree) ➔ 繞線 (Routing)。
- 必須滿足時序、面積、功耗、繞線擁擠度與製造規則的要求。

**7. 實體驗證與簽核 (Physical Verification and Signoff)**

晶片在送交製造前必須通過的最終檢查：
- **DRC (Design Rule Check, 設計規則檢查)**:確認實體佈局是否符合代工廠的製造幾何規則 (如最小間距)。 
- **LVS (Layout Versus Schematic, 佈局與電路圖比對)**: 確認物理佈局是否與原本設計的邏輯網表完全一致。
- **萃取 (Extraction)**: 萃取出佈局中的寄生電阻與電容 ($R_{par}, C_{par}$)，以進行最精確的時序與功耗分析。

**8. 下線製造到成品 (Tape-Out to Finished Chip)**
- **Tape-out (下線)**: 將最終通過驗證的實體佈局資料庫 (GDSII 格式) 送交晶圓代工廠。
- **後續流程**: 將 GDSII 轉為光罩 (Masks) ➔ 晶圓廠製造 (Wafer Fab) ➔ 切割與封裝 (Packaging) ➔ 測試 (Testing) ➔ 最終產出可用的 IC 成品。
## 半導體生態系與專業分工 (Semiconductor Ecosystem)
- **分工合作的產業模式**: 現代晶片的設計與製造通常由不同的組織分別負責，形成一個緊密相連的生態系。整個流程包含：晶片構想 (Chip Idea) $\rightarrow$ 無晶圓廠設計 (Fabless Design) $\rightarrow$ EDA 工具與矽智財 (IP) $\rightarrow$ 晶圓代工廠 (Foundry) $\rightarrow$ 封裝測試 (Packaging / Test) $\rightarrow$ 最終客戶產品 (Customer Product)。 
- **生態系中的四大關鍵角色 (Key Roles)：**
    - **無晶圓廠公司 (Fabless company)**: 負責定義產品、架構與執行晶片設計，但公司本身不擁有晶圓製造廠房。
    - **晶圓代工廠 (Foundry)**: 負責使用特定的製程技術 (Process technology) 與設計規則來實際製造晶圓 (Wafers)
    - **矽智財供應商 (IP provider)**: 提供可重複使用的設計區塊 (Reusable design blocks)，例如 CPU 核心、PCIe、USB 與記憶體控制器等，讓設計公司不需從零開始研發。
## 兩大重要設計資源：PDK 與標準元件庫
要進行真正的 ASIC 設計，不可或缺的兩個底層資源：
- **製程設計套件 (Process Design Kit, 簡稱 PDK)**: 由晶圓代工廠提供給設計方的資料包，裡面包含了技術檔案、元件模型 (SPICE Models)、圖層定義資訊 (Layer Definitions) 以及製造必須遵守的設計規則 (Design Rules，如 DRC/LVS 規則)。
