## bonuded-buffer problem (有限緩衝區問題)
- **共用資料結構**:包含N個緩衝區，並使用3個號誌來控管
    - semaphore mutex=1:提供存取緩衝區時的互斥(mutual exclusion)。
    - semaphore empty=N:紀錄目前有幾個空的緩衝區空間。
    - semaphore full=0:紀錄目前有幾個填滿的緩衝區空間。
- **運作機制**:
    - **生產者(producer)**:生產項目後，須先執行wait(empty)確保有空位，再執行wait(mutex)進入臨界區將項目加入，完成後執行signal(mutex)與signal(full)。
    - **消費者(consumer)**:須先執行wait(full)卻保有項目可取，再執行wait(mutex)進入臨界區取出項目，完成後執行signal(mutex)與signal(empty)
## Readers-Writers problem(讀者寫者問題)
探討多個並行行程（Concurrent processes）共享資料庫時的存取問題 。讀者只會讀取，寫者則會讀取與更新資料 。如果寫者與其他行程同時存取，就會造成資料混亂 。
- 兩種常見變形:
    1. **讀者優先**:除非寫者已取得使用共享物件的權限，否則不該讓讀者等待。
    2. **寫者優先**:一旦寫者準備好，應盡快執行寫入;若有寫者在等待存取物件，則不允許新的讀者開始讀取
- **第一類問題解法**:使用semaphore rw_mutex=1(同步讀寫)，semaphore mutex=1(保護更新計數器的read_count時的互斥)以及整數read_count=0。
- **實務應用**:這些概念在現代系統中被推廣為{讀寫鎖(read writer locks)}，允許多個行程同時以讀取模式獲取鎖，但寫入模式只能由單一行程獨佔。
## Dining-Philosophers Problem（哲學家就餐問題）
由 Edsger Dijkstra 於 1965 年提出的經典問題，用來探討資源分配與死結（Deadlock）問題
- **問題情境**:哲學家們圍在圓桌旁，只做思考和吃飯兩件事 。吃飯時必須同時取得左手邊與右手邊的兩根筷子，吃完後再將兩根筷子放下
- **號誌解法**:使用陣列semaphore chopstick[5] (全初始為1)代表五根筷子。哲學家i會執行wait(chopstick[i])，再執行wait(chopstick[(i+1)%5]) 取筷子 。
- **死結問題(deadlock)**:雖然上述解法保證相鄰的哲學家不會同時進食，但如果五個哲學家同時拿起左手的筷子，就會發生死結。
- **避免死結的解決方案**
    1. 最多只允許四位哲學家同時坐在桌旁。
    2. 規定哲學家必須在兩個筷子都可用時才能拿起筷子。
    3. 使用不對稱解法:奇數號哲學家先拿左手再拿右手邊的筷子，偶數鎬哲學家則是先拿右手邊再拿左手邊的筷子