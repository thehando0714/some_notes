## 語法分析器的角色與任務 (Role & Tasks of Parser)
- 語法分析器 (Parser) 負責接收詞法分析器 (Lexical Analyzer) 所產生的 token 字串。
- 主要任務是驗證該 token 字串是否符合來源程式的語法規則。
- 若語法合法，則會產生相對應的剖析樹 (Parse tree) 作為中間表示法。 
## 語法分析器的分類 (Two Types of Parsers)
- **由上而下分析 (Top-down)**：從樹根 (root) 往下建立剖析樹直到樹葉 (leaves)。
- **由下而上分析 (Bottom-up)**：從樹葉 (leaves) 往上建立剖析樹直到樹根 (root)。
## 上下文無關語法 (Context-Free Grammar, CFG)
- 語法可精確定義為四元組 $G = (T, N, P, S)$。
- **T (Terminals, 終結符號)**：構成字串的基本符號或 token (如 id, +, (, ))，慣例上以小寫英文字母或可列印字元表示。
- **N (Nonterminals, 非終結符號)**：表示字串集合的語法變數，慣例上以大寫英文字母開頭表示
- **P (Productions, 產生式)**：定義推導規則，形式為 $A \rightarrow \alpha_1, \alpha_2, \dots, \alpha_m$，其中 A 為 head，$\alpha$ 為 body。
- **S (Start symbol, 起始符號)**：開始進行推導的非終結符號，除非特別說明，通常是第一個產生式的 head。
## 推導 (Derivations)
- 推導符號 $\Rightarrow$ 代表「一步推導」。
-   推導符號 $\Rightarrow^+$ 代表「一步或多步推導」。
-   推導符號 $\Rightarrow^*$ 代表「零步或多步推導」。
-   句型 (Sentential form)：從起始符號推導出的字串，可同時包含終結符號與非終結符號。
-   句子 (Sentence)：完全不包含非終結符號的句型，而語法所產生的「語言」即為其所有句子的集合。
-   最左推導 (Leftmost Derivation)：推導時每一步都優先展開最左邊的非終結符號。
-   最右推導 (Rightmost Derivation)：推導時每一步都優先展開最右邊的非終結符號。  
##  剖析樹 (Parse Trees)
- 剖析樹是語法推導過程的圖形化表示法。  
- 對於同一個合法的句子，其最左推導與最右推導最終會產生出相同結構的剖析樹。  
## 模稜兩可的語法 (Ambiguous Grammar)
- **定義**：如果一個句子可以產生超過一棵剖析樹（即存在超過一種最左推導，或超過一種最右推導），該語法就是模稜兩可的。
- **造成的問題**：語法分析器無法唯一決定要選擇哪一棵剖析樹，導致句子的語意（例如數學運算的優先順序）無法被唯一確定。
- **消除方法**：通常需要改寫語法，這沒有通用的演算法，必須依賴期望的語意來決定。
- **解決優先權 (Precedence)**：為每個優先權層級使用一個專屬的非終結符號，並從較低優先權的運算開始設計規則。
- **解決結合律 (Associativity)**：若同優先權的運算子連續出現（如 id+id+id），需透過遞迴規則的方向來解決。
## 上下文無關語法 (CFG) vs 正規表示式 (RE)
- **能力比較**：CFG 的描述能力比 RE 更強大。任何能用 RE 描述的結構都能用 CFG 描述，但反之不成立（正規語言只是上下文無關語言的子集）。
- **經典反例**：語言 $L = \{a^n b^n \vert{} n \ge 1\}$ 可以用 CFG 描述，但無法使用 RE 描述。因為如果用有限狀態機 (DFA) 來辨識，狀態數量是有限的，無法記憶任意長度 $n$ 來確保 $a$ 和 $b$ 的數量一致，必定會產生矛盾。
- NFA 轉換為 CFG 的規則：
    - 針對 NFA 中的每一個狀態 $i$，建立一個非終結符號 $A_i$。
    -   若狀態 $i$ 接收輸入 $a$ 後會轉移至狀態 $j$，則加入產生式 $A_i \rightarrow a A_j$。
    -   若狀態 $i$ 是接受狀態 (Accepting state)，則加入產生式 $A_i \rightarrow \varepsilon$。
    -   NFA 的起始狀態即對應 CFG 的起始符號。 
## 撰寫語法時的三大常見問題 (Writing a Grammar)
- 為了讓語法分析器能順利運作，經常需要將語法改寫為等價但沒問題的形式。主要需要消除以下三個問題：
    1. 模稜兩可 (Ambiguity)
    2.   左遞迴 (Left recursion)
    3.   需要進行左提取 (Left factoring)
## 結合律與遞迴規則 (Associativity & Recursive Rules)
- 為解決連續相同優先權運算子（如連續加法）的結合律問題，語法需透過遞迴方向來控制。
- 左遞迴 (Left recursion)：形式為 $A \Rightarrow A\alpha$，適用於左結合（Left associativity）的運算。
- 右遞迴 (Right recursion)：形式為 $A \Rightarrow \alpha A$，適用於右結合（Right associativity）的運算。
## 懸置的 else 問題 (Dangling else)
- 這是一種經典的模稜兩可語法問題：當程式出現巢狀的 if-then-else 結構時，else 會自動配對到距離它最近、且尚未擁有 else 的 if 子句，導致剖析樹不唯一。
- 消除方法：透過改寫語法，將陳述式明確分為已配對 (Matched, M) 與開放/未配對 (Open, O) 兩種。
- **核心概念**:強制規定介於 then 與 else 之間的陳述式，必須是「已完全配對」的陳述式，藉此消除語意分歧。
## 消除左遞迴 (Elimination of Left Recursion)
- **造成的問題**：由上而下的語法分析器 (Top-down parser) 無法處理帶有左遞迴的語法，解析時會陷入無窮迴圈。
- **消除立即左遞迴 (Immediate left recursion)：**
    - 將原本的產生式 $A \rightarrow A\alpha \vert{} \beta$ （其中 $\beta$ 不以 A 開頭）。 
    -  改寫並引入新的非終結符號 $A'$：$A \rightarrow \beta A'$ 以及 $A' \rightarrow \alpha A' \vert{} \epsilon$。
- **通用演算法**：對於不含循環的語法，演算法會透過雙層迴圈，有系統地將前面的非終結符號展開代入後面的產生式中，接著再逐一消除每個非終結符號的立即左遞迴。  
## 左提取 (Left Factoring)
- **造成的問題**：當一個非終結符號擁有多個具有共同字首 (Common prefix) 的產生式時（例如 $S \rightarrow ( S ) \vert{} ( )$），預測型由上而下分析器會無法在第一時間決定該選擇哪一條推導路徑。
- **解決方法 (延遲決策)**：將共同的字首提取出來，把分歧點往後延。   
    - 原本的產生式 $A \rightarrow \alpha\beta_1 \vert{} \alpha\beta_2$。
    -   改寫為：$A \rightarrow \alpha A'$ 以及 $A' \rightarrow \beta_1 \vert{} \beta_2$。 
- **演算法**：針對每個非終結符號，找出其產生式右側最長的共同字首 $\alpha$ 並進行提取，不斷重複此過程，直到沒有任何兩個產生式擁有共同字首為止。 
## 非上下文無關語言 (Non-Context-Free Language Constructs)
- CFG 雖然強大，但仍有其表達極限，部分語言結構無法用 CFG 描述。
- 簡報列出的經典反例包括：字串複製 $L = \{wcw \vert{} w \text{ is in } (a\vert{}b)^*\}$，以及多變數的數量一致性 $L = \{a^n b^m c^n d^m \vert{} n \ge 1, m \ge 1\}$。
## 語法分析器的主要任務 (Main task of a parser)：
- 接收 token 字串。
-   驗證這些 token 字串是否能由來源程式的語法規則所產生。
-   如果合法，則產生對應的剖析樹 (Parse tree)。
## 上下文無關語法 (Context-free grammar, CFG)：
- 涵蓋了推導 (Derivations) 的過程。
-   涵蓋了剖析樹 (Parse trees) 的結構與概念。   
## 消除常見的語法問題 (Elimination of the common grammar problems)：
- 消除模稜兩可 (Ambiguity)，以確保程式語意的唯一性。
-   消除左遞迴 (Left recursion)，使由上而下的分析器不會陷入無窮迴圈。
-   進行左提取 (Left factoring)，解決產生式具有共同字首時造成的預測困難。  