# Circuit Breaker

在一個稍微複雜點的系統架構中, 一個服務通常都會有許多的外部依賴項目, 且每個依賴項目都有可能會發生Failure(也可能是網路問題).
這部份能參考[```微服務瞎談(5) CAP理論```][^1]

最前面的調用方們, 可能當下還感受不到某個依賴項目沒在響應了. 而一直持續的發出請求.
![](system_depdencies.png)  
會導致更嚴重的[```CataStrophic casading failure```災難性的級聯故障][^2]


## References
[^1]: [微服務瞎談(5) CAP理論](https://ithelp.ithome.com.tw/articles/10235541)  
[^2]: [Cascading failure](https://en.wikipedia.org/wiki/Cascading_failure)