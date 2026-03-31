# Fuzzy-Store-Funnel-and-Product-Launching-analysis
An end-to-end data analysis project focused on optimizing the conversion funnel and evaluating product launch performance for "Fuzzy Store." This repository contains tools to identify customer drop-off points and measure the success of marketing campaigns through data-driven insights.
# Project Background
Fuzzy Factory is a direct-to-consumer e-commerce company specializing in premium stuffed animals and gift-oriented bear products. The company has been operational since early 2012 and operates entirely through its online storefront, making website performance and conversion optimization central to its revenue model.

As the in-house Data Analyst, the primary mandate is to support marketing, product, and executive leadership in making data-backed decisions across four strategic areas: understanding growth trends, diagnosing funnel inefficiencies, evaluating product launches, and optimizing marketing channel spend.

Key business metrics tracked:

- Conversion Rate (CVR) — sessions to completed purchase
- Bounce rate by landing page variant
- Cart abandonment rate

Insights and recommendations are provided on the following stakeholder questions:

`Why does high traffic volume not translate into proportional order volume — where are customers dropping off?`

The Python codes used to inspect and clean the data for this analysis can be found here [link].

Targeted SQL queries regarding various business questions can be found here [link].

An interactive Tableau dashboard used to report and explore sales trends can be found here [link].
# Data Structure & Initial Checks
The companies main database structure as seen below consists of four tables: table1, table2, table3, table4, with a total row count of X records. A description of each table is as follows:

`orders`: Stores high-level information and summary data for all placed orders.

`order_items`: Contains granular details for each specific product within an order (e.g., quantity, price per unit).

`order_item_refunds`: Tracks customer refund transactions and associated return data.

`products`: A comprehensive catalog of all products available on the platform.

`website_sessions`: Records user visit data, including traffic source and entry touchpoints.

`session_pageviews`: Logs specific pages viewed by users during each individual session.

|<img width="1288" height="510" alt="image" src="https://github.com/user-attachments/assets/e1336a4d-0858-4b64-8c05-51faae49be52" />|
|:-----------:|
|**Figure 1:** Entities Relationship Diagram|


# Executive Summary
Fuzzy Factory recorded over 400,000 website sessions across the analysis period, yet only 32,313 resulted in completed transactions — an overall conversion rate of 6.8%. This report investigates the root causes of the 93.2% drop-off, identifies the primary bottleneck in the conversion funnel, and documents the A/B testing journey that progressively improved landing page performance. The findings support a focused optimization effort on the Detail View → Add-to-cart stage, while confirming that the Home/Landing page bottleneck has been largely resolved through iterative experimentation.

[Visualization, including a graph of overall trends or snapshot of a dashboard]
# Insights Deep Dive
## Question 1: Why does high traffic volume not translate into proportional order volume — where are customers dropping off?

Table 1: Total Session through funnel

|year|total_sessions|step_1_home|step_2_products|step_3_product_detail|step_4_cart|step_5_shipping|step_6_billing|step_7_ordered|
|-------|:-------:|:-------:|:-------:|:-------:|:-------:|:-------:|:-------:|:-------:|
|2012|	62470 |	62470  |29468	 |21252 |9235 |	6306 |	5166 |	2586 |
|2013|	112781|	112781 |62491	 |47878	|21521|	14647|	11877|	7447 |
|2014|	233423|	233422 |130660 |108182|48794|	33058|	26580|	16860|
|2015|	64198 |	64198	 | 38612 |32902	|15403|	10473|	8435 |	5420 |

|<img width="1011" height="333" alt="Ảnh chụp màn hình 2026-03-29 230840" src="https://github.com/user-attachments/assets/15abc764-181f-422b-a3b2-fff8486d9917" />|
|:---------:|
|**Figure 2:** Conversion Rate and Drop-off by Stages|



Based on Table 1 and Figure 2, between March 2012 and March 2015, the Fuzzy Factory e-commerce platform recorded a total of 472,871 sessions. Out of these, only 32,313 sessions successfully converted into orders, resulting in an overall Conversion Rate (CVR) of 6.8%. Analysis of the conversion funnel reveals three critical bottlenecks:
- **Point 1: Home -> Product:** More than 200,000 sessions exit the site immediately after landing, without viewing any specific product.
- **Point 2: Product Detail View -> Add-to-cart:** Approximately 115,000 sessions—nearly 54,8% of users who viewed a product—dropped off before adding an item to their cart.
- **Point 3: Add-to-cart -> Success Purchase:** Out of 63,640   sessions that reached the "Add-to-cart" stage, 38,547 sessions failed to complete the transaction, resulting in only 32,313 successful orders.



Để có thể hiểu rõ hơn về các bottleneck, tôi sẽ drill-down vào từng stage để phân tích:

**Bottleneck 1:** Home → Product
To better understand these bottlenecks and explain why high traffic volume does not translate into proportional orders, a detailed drill-down into the first stage is required:

Bottleneck 1: Home → Product

1. By landing page

Main insight 1: Superior Performance of /lander-5 for New Desktop Users. Among all landing pages, /lander-5 achieved the highest efficiency with a 63.13% CTR for new desktop users. This indicates that once the platform moved away from experimental versions, this specific layout successfully captured and retained user interest better than any other iteration.

Main insight 2: The Significant Failure of /lander-4. When comparing similar segments (New/Desktop), /lander-4 underperformed severely with a CTR of only 48.31%, compared to the baseline /home (57.96%) and the high-performing /lander-5 (63.13%). This 10-15% performance gap confirms that the /lander-4 design failed to engage its target audience during its brief run.

Main insight 3: Post-Pilot Recovery of /lander-3. After a period of high-volume but low-quality traffic during the Pilot phase, /lander-3 saw its CTR recover to 41.65% in March 2014. This suggests that the landing page itself was functional, but its metrics were previously suppressed by the mismatch between the campaign audience and the page content.

2. By campaign

Main insight 1: Quality Dilution via the /lander-3 Pilot Campaign. Between January and February 2014, the Pilot campaign attracted a surge of new customers to /lander-3. However, the quality of this traffic was significantly lower, causing CTR to plummet from 53.46% (Dec 2013) to a low of 35.04% (Feb 2014). The high "leakage" at Point 1 during this period is directly attributed to this influx of low-intent sessions.

Main insight 2: Inefficiency of the Desktop-Targeted Campaign on /lander-2. The campaign launched for /lander-2 in late 2014 proved highly ineffective. It resulted in a simultaneous loss of traffic volume and a crash in traffic quality, with CTR dropping from 53.13% in October to a critical low of 29.75% in December 2014 (a -31.9% MoM decline).

Main insight 3: Stability through Brand and Direct Traffic at /home. Unlike the experimental landers, traffic directed to /home (primarily Brand and Direct) remained high-quality and consistent. This segment acted as a stabilizer for the funnel, even while experimental non-brand campaigns were causing significant drop-offs elsewhere.

3. By device type

Main insight 1: Mobile as the Primary Leakage Point for New Traffic. Mobile sessions consistently show the highest drop-off rates. For new users, /home mobile CTR was only 41.92% compared to 57.96% on desktop. This inherent device friction is a major reason why high total traffic (driven by mobile expansion) does not yield proportional orders.

Main insight 2: High Intent of Repeat Customers on Desktop. The strongest performance in the entire funnel was seen among repeat customers on desktop at /home, with a 70.12% CTR. This confirms that the "Home -> Product" transition is nearly seamless for loyal users, whereas "cold" traffic from new campaigns is where the majority of the 200,000+ exits occur.

Main insight 3: Optimization Gap for Mobile-Targeted Landers. While /lander-5 maximized desktop performance, the lack of an equivalent mobile-optimized version for these new campaigns forced mobile traffic into lower-performing funnels (like the pilot on /lander-3), further exacerbating the drop-off at Point 1.
**Bottleneck 2 — Detail View → Add-to-Cart (~55% drop-off):**

This is the most significant active bottleneck. Average time on the product detail page is approximately 2 minutes — indicating user engagement rather than UI friction. The high exit rate therefore points to product-side barriers: insufficient product description quality, non-compelling imagery, or a pricing mismatch relative to willingness-to-pay. This is the highest-priority optimization target.

<img width="1186" height="690" alt="1a110e4e-6547-49cf-adc4-aa826a199ffe" src="https://github.com/user-attachments/assets/a5708691-a296-4635-bdbb-b6c9f30a2d1a" />

**Figure 3:** Product Detail to Cart Conversion Rate by Product

**Bottleneck 3 — Billing Drop-off (37.9%):**

Elevated, but within the accepted e-commerce benchmark range of ~60–80% ([source](https://baymard.com/lists/cart-abandonment-rate)). Average time at this stage (~3.25 minutes) suggests checkout form complexity as a contributing factor. Given benchmark alignment, this is a lower priority relative to Bottleneck 2.


# Recommendations:
Based on the insights and findings above, we would recommend the [stakeholder team] to consider the following:
Specific observation that is related to a recommended action. Recommendation or general guidance based on this observation.
Specific observation that is related to a recommended action. Recommendation or general guidance based on this observation.
Specific observation that is related to a recommended action. Recommendation or general guidance based on this observation.
Specific observation that is related to a recommended action. Recommendation or general guidance based on this observation.
Specific observation that is related to a recommended action. Recommendation or general guidance based on this observation.
# Assumptions and Caveats:

Throughout the analysis, multiple assumptions were made to manage challenges with the data. These assumptions and caveats are noted below:

**1. Partial months excluded from YoY trend analysis:**
The dataset begins on March 19, 2012 and ends on March 19, 2015. Both March periods contain only 13–19 days of data. Including these months in YoY comparisons would overstate 2013 growth by approximately 2x due to unequal day counts in the baseline. All trend analysis uses April 2012 as the start point for YoY calculations. For March 2015 performance, a Month-to-Date (MTD) comparison using the same 19-day window from 2014 is used instead of full-month extrapolation.

**2. Null UTM campaign handling:**

For records in website_sessions where utm_campaign is missing (null), traffic is categorized using the following logic:

- ***Direct Traffic:*** Sessions where both utm_source and http_referer are null — users accessing via direct URL or bookmarks.
- ***Organic Search:*** Sessions where utm_source is null but http_referer contains search engine strings — unpaid search discovery.

**3. Bounce rate benchmarks sourced from Shopify industry data:**

The e-commerce bounce rate benchmark range of 36–45% referenced in Category 2 is based on published Shopify industry averages for retail and gifting categories. This benchmark should be periodically refreshed as market conditions evolve.

**4. March 2015 YoY decline is a data artifact, not a business signal:**

The apparent -3.7% YoY session decline in March 2015 is caused by the dataset ending on March 19 — creating an incomplete month compared to a full March 2014. This should not be reported as a performance decline without the MTD context provided in Category 1.
