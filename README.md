# Momentum-Volitility Factor


因子策略，利用動能因子篩選出S&P 500的前10股票做交易，每一季換一次倉，數據處理有用離散傅立葉轉換(對於選股的當下，往回溯10年的股價做傅立葉轉換)，消除市場噪音，選出高潛力，低波動的股票，最後獲得比帶盤低的風險但是報酬是數倍。<br>
訓練期 : 2014-01-01 到 2021-12-31，測試期 : 2022-01-01 到 2024-12-31<br>

核心觀念 : 潛力 + 低波動率<br>

潛力 : <br>
M1 = Price ratio( 昨天 v.s  6   天前 )<br>
M2 = Price ratio( 昨天 v.s  15 天前 )<br>
M3 = Price ratio( 昨天 v.s  30 天前 )<br>
P = zscore(M1*M2*M3)<br>
直觀意涵 : M1*M2*M3低的話，代表股價還保有潛力<br>

低波動率 : <br>

S = zscore ( std ( 近六個月的股價) )<br>
直觀意涵 : 在過去六個月有較小的標準差，代表低波動率<br>

我們選擇P+M前10小的股票來做交易，<br>

最佳化 : <br>
一旦單一股票下跌超過5%，那支股票就止損<br>

![image](https://github.com/user-attachments/assets/53da4577-1136-4560-8832-64f95dfe5693)



未來改進 : ﻿用布林通道提前篩選出進出場點位，利用VIX指數，調整帶寬，市場恐慌時就讓帶寬變小，避免市場震盪影響，市場行情好的話就把帶寬變長，讓股票漲上去。<br><br>


Factor Strategy<br>
This strategy utilizes a momentum factor to select the top 10 S&P 500 stocks for trading, with a quarterly rebalancing approach. Discrete Fourier Transform (DFT) is applied to remove market noise, allowing the identification of high-potential, low-volatility stocks. As a result, the strategy achieves significantly higher returns compared to the benchmark while maintaining lower risk.<br>

Training & Testing Periods:<br>
Training period: 2014-01-01 to 2021-12-31<br>
Testing period: 2022-01-01 to 2024-12-31<br>
Core Concept: Potential + Low Volatility<br>

Potential:<br>

M1 = Price ratio( yesterday v.s  6   days ago )<br>
M2 = Price ratio( yesterday v.s  15 days ago )<br>
M3 = Price ratio( yesterday v.s  30 days ago )<br>
P = zscore(M1*M2*M3)<br>


Intuition : small M1*M2*M3 means that the stock remains potential<br>


S = zscore ( std ( prices of past 6 months ) )<br>

Intuition behind the factor S: <br>
Low standard variation means that in the past 6 months,<br>
the prices of stocks have lower fluctuation <br>

We select the top 10 stocks with the smallest P + M as stocks to trade from S&P 500 component stocks<br>



At the first day of each trading turns, Fast Fourier Transform is applied to<br>
stock prices over past 10 years in order to remove market noises (over-reacting).<br>


Future Improvements:<br>
Bollinger Bands will be used to pre-identify entry and exit points.<br>
VIX index will be incorporated to dynamically adjust bandwidth:<br>
During market panic, the bandwidth is reduced to minimize the impact of volatility.<br>
In strong market conditions, the bandwidth is widened to allow stocks to capture upward momentum.<br>









