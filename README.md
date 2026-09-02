# Semiconductor & Chip Design Companies; Financial Analysis

Comparing Nvidia against its top semiconductor/chip-design competitors (AMD, Intel, TSMC, Qualcomm, Broadcom, ASML) using quarterly financial statements and stock price data, to see how Nvidia's financial performance and market valuation stack up against the sector after its record-breaking August 2026 earnings report.

## Motivation

On August 26, 2026, Nvidia published a quarterly report that sent the whole US stock market into a "green day," with Nvidia itself up 10% on actual revenue and earnings beating expectations. Since I'd been working with `plotly.express` and pandas data-cleaning techniques, I used this as an opportunity to build a real comparison: how does Nvidia actually perform financially against its top 7 competitors, and does its stock price reflect that financial position, revenue, market share, market cap, or something else?

**Note:** Data pulled via `yfinance` was current through end of June 2026, so it does **not** include Nvidia's most recent report.

## Repo Structure

```
├── Code/     # Jupyter notebook with data pull, cleaning, and chart generation
├── Data/     # Empty in repo; script downloads fresh data via yfinance on each run
├── Graph/    # Exported chart images (PNG)
└── README.md
```

> Data isn't committed to the repo since the notebook pulls it live from `yfinance` each time it's run; this keeps the analysis reproducible with current data rather than a stale snapshot.

## Tools Used

- `pandas`; data cleaning, merging (`merge_asof`), currency conversion, groupby aggregation
- `yfinance`; quarterly income statements + historical price data
- `plotly.express`; bar, pie, scatter (bubble), and box charts
- `matplotlib`; price trend line chart

## Data & Cleaning

- Companies: Nvidia, AMD, Intel, TSMC, Qualcomm, Broadcom, ASML
- Pulled last 5 quarterly income statements + 2 years of monthly price history per company
- Cleaned: dropped NaNs, removed unnecessary columns, standardized date types
- Merged quarterly financials with price data using `merge_asof` (backward direction) to align each statement with the most recent available price
- **Currency normalization:** TSMC reports in TWD and ASML in EUR; both converted to USD before cross-company comparison

## Charts

**1. Total Revenue by Company**
![Total Revenue Bar Chart](Graph/total_revenue_bar.png)

**2. Market Share by Revenue**
![Market Share Pie Chart](Graph/market_share_pie.png)

**3. Quarterly Revenue by Company**
![Quarterly Revenue Bar Chart](Graph/quarterly_revenue_bar.png)

**4. P/E vs Revenue Growth, Sized by Market Cap**
![P/E vs Revenue Growth Bubble Chart](Graph/pe_vs_growth_bubble.png)

**5. Price Distribution (log scale)**
![Price Distribution Box Chart](Graph/price_distribution_box.png)

**6. Price Trend Over Time**
![Price Line Chart](Graph/price_line_chart.png)

## Analysis

In the first total revenue chart, Nvidia's total revenue is higher than 1.5x the highest total revenue of the remaining companies, which indicates how much the company has succeeded in manufacturing and selling chips and related technology products, including chips and selling AI systems.

If we move to the market share pie chart, we can see the percentage of each company's total revenue to the total revenues of all companies, where Nvidia holds 38% of market share alone, and the second position belongs to TSMC, which holds 22% of total market share.

Let's move on to the third chart, which shows the revenue of named companies in quarterly periods as announced by the companies. As expected, Nvidia still has the highest quarterly revenues among all companies. Something that catches your attention at first look is the growth of Nvidia's revenue in each quarter; for example, between the first and second quarter, we have a rise of approx. 5% in revenue, despite an approx. 20% increase between the next quarters. However, other companies' revenues are increasing mostly around 10%, and also decreasing in some quarters. This still indicates the success rate of Nvidia in generating strong revenue in each quarter, which makes it well known as well.

Based on what we've seen until now, we can say the most successful company has been Nvidia, so we can expect a high stock price and higher P/E. To find out, let's move on to the next graph, the quarterly P/E vs Revenue Growth sized by Market Cap bubble chart. As mentioned before, the graph shows that the revenue growth of Nvidia is around 20 percent, and unlike other companies, its revenue growth has been more constant, with no sharp changes in recent quarters. Also, its bubble/market cap is the largest one, which indicates either higher price, higher market share, or both. An important point about Nvidia to mention here is that with a higher market cap, it should be much more difficult for the company to increase its revenue growth in percentage terms; Nvidia has the highest market cap and a higher, more constant revenue increase than others. But surprisingly, we see its P/E ratio is not the highest in the market, and is placed approximately in the middle range, between 100 and 200, which raises a question: is this because the stock is undervalued, or are stockholders waiting on/expecting some important news about the company?

Let's keep this in mind and move to the next chart, price distribution. Something to note about this chart is that the y-axis is log type, and box sizes don't reflect percent change in price. Based on this chart, Nvidia had price changes between 109 and 202, which is quite low for a company with high growth rate and high market cap. This may reinforce the previous question raised in the last graph; why doesn't the price fluctuate much, and why don't we see higher values? One answer to this can be Nvidia's high market cap compared to other companies, making it much more difficult for it to move in percentage terms.

Before moving to the last, price chart, and conclusion, let's sum up what we have so far: Nvidia has the highest total revenue, market share, and revenue growth. On the other hand, the price changes and P/E ratio are below what we expected. This leaves us with two questions to answer; is the price undervalued, or is there something wrong about the company that we can't simply read from the charts?

In the price line chart, we see that Nvidia's stock price is almost the same as other companies. The reason some companies have much higher prices or fluctuate more sharply can be because of their market cap and the concentration of shares held by a specific range of investors, which can move price more than for companies like Nvidia with a larger share count. However, the revenue and market share increase rates don't exactly translate into stock price.

### Conclusion

To answer our questions, maybe we have to go beyond just the charts and take a look at stakeholder expectations. Although we had strong revenue reports and growth, according to Stocktwits (Aug 13, 2026), NVIDIA's 5-year CDS spread has recently reached 79.8 basis points, more than double its late-May level and close to the 83.7 bp record set in July. This doesn't mean NVIDIA itself is over-leveraged; rather, the concern is that the AI boom is increasingly being financed through debt across the industry. If NVIDIA's customers fail to generate sufficient returns from their AI investments, demand for NVIDIA's GPUs could weaken, putting its future growth at risk.

So my answer is: despite this rising credit risk, the moderate P/E still suggests the stock may be undervalued relative to its fundamentals; though the credit risk is a real headwind that could limit how much further the price runs. To get a clearer answer, it's worth watching two things going forward: whether the CDS spread keeps climbing or stabilizes in the coming months, and whether Nvidia's next quarterly guidance shows any slowdown tied to its financing partners' actual returns on AI infrastructure. Both would tell us whether the market's caution is temporary or a sign of a real shift in Nvidia's growth story.

> *This analysis is for educational purposes only, reflects my personal opinion based on public data, and is not financial or investment advice.*

## Challenges & What I Learned

- Handling multi-currency financial statements (TSMC in TWD, ASML in EUR) and converting them to a common USD basis before comparison
- Aligning two different data frequencies (monthly price data vs. quarterly statements) using `merge_asof`
- Keeping consistent colors and category ordering across five different Plotly chart types plus a separate matplotlib chart
- Debugging a P/E ratio formula error (had it inverted initially) and a `groupby().value_counts()` step that wasn't doing what it looked like it was doing
- Formatting log-scale axes to show plain numbers instead of scientific notation / powers of ten

## What I'd Improve Next

- Re-run once the latest Nvidia earnings report is reflected in `yfinance` data
- Use historical exchange rates per quarter instead of a single static conversion rate for TWD/EUR
- Add error handling for tickers with missing or delayed financial data
- Extend the analysis with a rolling correlation between revenue growth and price movement
