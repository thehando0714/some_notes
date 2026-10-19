## 由上而下分析 (Top-Down Parsing)
- 由樹根 (root) 開始建立剖析樹，並以前序 (preorder, depth-first) 的方式建立樹的節點。
- 分析器的目標是為輸入字串找出對應的最左推導 (leftmost derivation)。
- 主要分為兩種方法：遞迴下降分析 (Recursive-descent) 與預測型分析 (Predictive parsing)
## 遞迴下降分析 (Recursive-Descent Parsing)
- **核心概念**：嘗試所有可能性（窮舉搜尋），以找出能成功解析輸入字串的剖析樹。
- **缺點**：
    - 過程中可能需要進行回溯 (backtrack)，導致解析速度緩慢。
    -   若語法中包含左遞迴 (left-recursive grammar)，會導致分析器陷入無窮迴圈。
- **回溯機制**：為了嘗試不同的推導規則 (production)，分析器在失敗時，必須將輸入指標 (input pointer) 重設回當初嘗試該規則前的初始位置，才能繼續嘗試下一條規則。
## 預測型分析 (Predictive Parsing)
- 屬於遞迴下降分析的一種特例，其最大特點是不需要回溯。
- **前瞻機制 (Lookahead)**：透過預先查看下一個輸入符號 (next input symbol)，精準預測並決定要套用哪一條推導規則。
- 運作上需仰賴 FIRST() 與 FOLLOW() 兩個集合的運算，並結合剖析表 (Parsing Table) 將「非終結符號 + 該輸入符號」直接對應到唯一適用的推導規則，這也是 LL(1) 語法的基礎。
## FIRST() 集合的定義與計算(十分複雜要看講義)
- **定義**：FIRST(α) 是指從語法符號字串 $\alpha$ 所推導出的字串中，所有可能出現的「起始終結符號 (terminals)」所組成的集合。
- **決策用途**：若面對規則 $A \rightarrow \alpha \vert{} \beta$，當下一個輸入符號 $a$ 存在於 FIRST(α) 中，分析器就會選擇套用 $A \rightarrow \alpha$。
## FOLLOW() 集合的定義與計算
- **定義**：對於非終結符號 $A$，FOLLOW(A) 是指在某個句型中，緊接在 $A$ 右邊出現的終結符號 (terminals) 所組成的集合（即 $S \Rightarrow^* \alpha A a \beta$ 中的 $a$）
- 若 $A$ 有可能出現在某個句型的最右邊，則輸入結束標記 $ 會被加入 FOLLOW(A) 中
## 剖析表 (Parsing Table) 的建構規則
- 針對語法中的每一條推導規則 $A \rightarrow \alpha$，依照以下步驟將規則填入二維表格 $M[A, a]$ 中（其中 $A$ 為非終結符號，$a$ 為輸入符號）：
    1. 針對 FIRST(α) 中的每一個終結符號 $a$，將規則 $A \rightarrow \alpha$ 填入 $M[A, a]$。
    2.   若 $\varepsilon$ 存在於 FIRST(α)，則針對 FOLLOW(A) 中的每一個終結符號 $b$，將規則 $A \rightarrow \alpha$ 填入 $M[A, b]$。 
    3.  若 $\varepsilon$ 存在於 FIRST(α) 且 $ 存在於 FOLLOW(A)，則將規則 $A \rightarrow \alpha$ 填入 $M[A, \$]$。
- 將表格中所有未定義（沒有填入規則）的欄位，全部標記為錯誤 (error)。
- **核心精神**：預測型分析 (Predictive parsing) 實際上就是「遞迴下降分析 + 剖析表」。如果建構出的剖析表中，每一個格子最多只有一條推導規則，分析過程中就絕對不會發生回溯 (no backtracks)。
## FIRST() 與 FOLLOW() 的決策機制
- 當分析器遇到有多個選擇的產生式（例如 $A \rightarrow \alpha_1 \vert{} \alpha_2 \vert{} \dots \vert{} \alpha_k$），且下一個讀取到的輸入符號為 $a$ 時：
    -   若 $a$ 只存在於唯一一個 $FIRST(\alpha_i)$ 中，就毫不猶豫地選擇推導 $\alpha_i$。
    -   若 $a$ 同時存在於兩個以上的 $FIRST$ 集合中，代表發生了衝突，該語法就不是 LL(1) 語法。
    -   若 $a$ 不在任何一個 $FIRST$ 集合中，但其中某個 $\alpha_i$ 可以推導出空字串 $\varepsilon$，且 $a$ 剛好落在 $FOLLOW(A)$ 裡面，這時候就會選擇該條推導出 $\varepsilon$ 的式子。 
##   LL(1) 語法的定義與特性
- 命名意義：
    -   第一個 L：由左至右 (Left to right) 掃描輸入字串。
    - 第二個 L：尋找最左推導 (Leftmost derivation)。
    - 1：每次只需往前偷看 1 個輸入符號 (lookahead 1 symbol)。
- 嚴格限制：只要語法帶有「模稜兩可 (ambiguous)」或「左遞迴 (left-recursive)」的特性，它絕對不可能是 LL(1)。
- 判斷條件：一個語法若是 LL(1)，對於任何擁有分歧的產生式 $A \rightarrow \alpha \vert{} \beta$，必須滿足以下嚴格的互斥條件：
    1. $FIRST(\alpha)$ 與 $FIRST(\beta)$ 絕對不能有交集（不能有相同的開頭）。 
    2.   $\alpha$ 和 $\beta$ 最多只能有一個可以推導出空字串 $\varepsilon$。 
    3.   如果 $\beta$ 可以推導出 $\varepsilon$（代表 $\beta$ 可能會消失），那麼 $FIRST(\alpha)$ 與 $FOLLOW(A)$ 絕對不能有交集。
 