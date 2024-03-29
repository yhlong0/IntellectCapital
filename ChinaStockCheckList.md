# Instruction For China Stock Market

1. Go to https://www.tradingview.com/stock-screener/, filter by below:
   - CN Market
   - Sector filter out financial stocks, utilities stocks
   - ROA > 25%, full year
   - PE > 5
3. NetworkTab -> Scan -> Response -> data array
4. Replace winner.js -> data
5. node winner.js
6. Review Financial Statements.
    - Go to the (url)[https://www.tradingview.com/symbols/SSE-688707/]
    - Search symbols -> click **see overview**, not launch chart
    - https://www.tradingview.com/symbols/SZSE-000408/financials-income-statement/
8. Overview -> Growth and profitability ->
   - Ensure a consistent upward trend in income. Recent quarterly income is not declining.
   - Look for stable or increasing profit margins.
   - Debt decrease, free cash flow and cash increase
9. Statements -> Cash flow -> yearly,
   - Verify that yearly operating cash is increasing and not declining recently.
   - Ensure the sum of investing and financing cash flows is less than operating cash flow.
   - Financing should predominantly be used for dividends or stock repurchases.
10. Balance sheet
   - Confirm a consistent increase in equity.
   - Current assets should be greater than current liabilities.
11. Assess the market capitalization, average income, and equity amount. Estimate the time required to recuperate your investment.
12. Quarterly, add 4-5 stocks to your portfolio, aiming for a total of 15-25 stocks. Remove or replace stocks that underperform for 2-3 consecutive quarters.
13. When adjusting your portfolio, redistribute additional funds such that each stock's value equals the total portfolio value divided by the number of stocks.

```
8/10/2023

000408: ZANGGE MINING CO L
002460: 赣锋锂业
300628: YEALINK NETWORK TE
300861: YANGLING METRON NE, 电镀金刚石线的研发、生产及销售
301004: ZHEJIANG CAYI VACU
603688: JIANGSU PACIFIC QUARTZ CO.,LTD.

11/08/2023
600188, cap 126B, income 20B, equity 114B, 1 year,
000822, cap 6B, income 0.7B, equity 4.7B, 2 years
000933, cap 34B, income 7B, equity 22B, 2 years
600096, cap 30B, income 4.5B, equity 19B, 3 years,
600873, cap 27B, income 3-4B, equity 14B, 3.7 years

02/18/2024
301371, cap 120B, equity 56B, income 7B, 9 years 
688717, cap 122B, equity 23B, income 11B, 9 years
001358, cap 24B, equity 7B, income 1.5B, 11 years
688581, cap 46B, equity 21B, income 1.5B, 16 years
```
