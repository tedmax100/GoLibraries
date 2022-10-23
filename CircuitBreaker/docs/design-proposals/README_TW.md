# Circuit Breaker

## Context and Problem
在一個稍微複雜點的系統架構中, 一個服務通常都會有許多的外部依賴項目, 且每個依賴項目都有可能會發生Failure(瘋狂失敗, 短時間內沒有響應, 一直超時, 也可能是網路問題就是).
這部份能參考```微服務瞎談(5) CAP理論```[^1]

最前面的調用方們, 可能當下還感受不到某個依賴項目沒在響應了. 而一直持續的發出請求.
![](system_depdencies.png)  
會導致更嚴重的```CataStrophic casading failure```災難性的級聯故障[^2]
讓系統內更多節點因這一個依賴項目沒響應, 而導致整條鏈路上的多個節點都陷入故障危機.

因此要讓整體變得更加可靠的話, 讓外部依賴變得完全可靠是不可能的.
我們能透過包裝對依賴項目的調用來設計, 並持續監控其故障率.
一旦故障率達到某個門閥值, 就跳閘, 讓調用在```最短時間內響應```故障或錯誤回去.
這設計理念能稱為```fail fast```[^3]

## Solution
Michael Nygard在Release It!該書中[^4], 提到了Circuit Breaker Pattern(斷路器模式)  
![](ReleaseIt.jpg)  
用來防止調用方重複地去嘗試執行極有可能失敗的遠端操作. 讓調用方停止去等待它並立刻處理失敗的依賴服務不可用的事實.
通過防止單個服務的故障在整個系統中發生級聯故障, Circuit breaker pattern有助於快速恢復整個系統.
Circuit breaker pattern還能自己檢測故障是否已經排除, 如果故障已經被解決, 則會允許調用方可以調用該操作.

## FSM
![](curcuit_breaker_FSM.png)



## References
[^1]: [微服務瞎談(5) CAP理論](https://ithelp.ithome.com.tw/articles/10235541)  
[^2]: [Cascading failure](https://en.wikipedia.org/wiki/Cascading_failure)  
[^3]: [Fail Fast](https://en.wikipedia.org/wiki/Fail-fast)  
[^4]: [Release It!](https://pragprog.com/titles/mnee2/release-it-second-edition/)