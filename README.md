# Maven-Fuzzy-Factory-Funnel-Traffic-Analysis
An end-to-end data analysis project focused on optimizing the conversion funnel performance for "Maven Fuzzy Factory." This repository contains tools to identify root-cause of customer drop-off points and propose recommendation through data-driven insights.
# Project Background
Fuzzy Factory is a direct-to-consumer e-commerce company specializing in premium stuffed animals and gift-oriented bear products. The company has been operational since early 2012 and operates entirely through its online storefront, making website performance and conversion optimization central to its revenue model.

As the in-house Data Analyst, the primary mandate is to support marketing, product, and executive leadership in making data-backed decisions across four strategic areas: understanding growth trends, diagnosing funnel inefficiencies, evaluating product launches, and optimizing marketing channel spend.

Key business metrics tracked:

- Conversion Rate (CVR) — sessions to completed purchase
- Click-through rate (CTR)
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
Between 2012 and 2015, the platform generated over 472,000 sessions with an overall conversion rate of 6.8%. While desktop acquisition is optimized—notably through the /lander-5 deployment—the funnel reveals the main bottlenecks: systemic mobile underperformance. To maximize efficiency, we recommend establishing /lander-5 as the desktop control baseline, and optimizing the mobile funnel to close the device performance gap,

# Overview

Table 1: Total Session through funnel

|Year|Total Sessions|Step 1-Home|Step 2-products|Step 3-Product Detail|Step 4-Cart|Step 5-Shipping|Step 6-Billing|Step 7-Ordered|
|-------|:-------:|:-------:|:-------:|:-------:|:-------:|:-------:|:-------:|:-------:|
|2012|	62470 |	62470  |29468	 |21252 |9235 |	6306 |	5166 |	2586 |
|2013|	112781|	112781 |62491	 |47878	|21521|	14647|	11877|	7447 |
|2014|	233423|	233422 |130660 |108182|48794|	33058|	26580|	16860|
|2015|	64198 |	64198	 | 38612 |32902	|15403|	10473|	8435 |	5420 |

Based on Table 1 and Figure 2, between March 2012 and March 2015, the Fuzzy Factory e-commerce platform recorded a total of 472,871 sessions. Out of these, only 32,313 sessions successfully converted into orders, resulting in an overall Conversion Rate (CVR) of 6.8%. Analysis of the conversion funnel reveals three critical bottlenecks:
- **Point 1: Home -> Product:** More than 200,000 sessions exit the site immediately after landing, without viewing any specific product.
- **Point 2: Product Detail View -> Add-to-cart:** Approximately 115,000 sessions—nearly 54,8% of users who viewed a product—dropped off before adding an item to their cart.
- **Point 3: Add-to-cart -> Success Purchase:** Out of 63,640   sessions that reached the "Add-to-cart" stage, 38,547 sessions failed to complete the transaction, resulting in only 32,313 successful orders.

|<img width="1011" height="333" alt="Ảnh chụp màn hình 2026-03-29 230840" src="https://github.com/user-attachments/assets/15abc764-181f-422b-a3b2-fff8486d9917" />|
|:---------:|
|**Figure 2:** Conversion Rate and Drop-off by Stages|

To better understand these bottlenecks and explain why high traffic volume does not translate into proportional orders, a detailed drill-down into the first stage is required:

# Insight Deep Dive

### **Stage 1:** Top-Funnel Diagnostics (Home/Landing → Product)

***Key takeaway:*** The 200,000+ session drop-off at the top of the funnel is primarily a filtering of low-intent traffic. Continuous A/B testing and split-routing have optimized this stage close to its ceiling, with the exception of a gap on mobile devices.

- **Main finding 1:** The hypothesis that the landing page design is flawed is rejected for desktop users. Historical data traces the A/B testing progression for new desktop traffic. Between mid-2012 and mid-2014, traffic allocated to early variants (`/lander-1`, `/lander-2`, and `/lander-4`) resulted in a 45%–55% CTR, underperforming the `/home` page's 60%–66% baseline and reducing overall monthly averages. In August 2014, the deployment of `/lander-5` achieved a 62.1% CTR, matching the `/home` baseline. Reallocating traffic volume to `/lander-5` in late 2014 stabilized the overall desktop acquisition CTR above 60% by early 2015.

|<img width="1389" height="690" alt="image" src="https://github.com/user-attachments/assets/a62dbe2f-73b6-497e-ad37-64494291eced" />|
|:---------:|
|**Figure 3:** Desktop Acquisition CTR of New Customer on Desktop|

- **Main finding 2:** Audience intent dictates the conversion ceiling, validating the split-routing architecture. Data shows that Repeat and Brand-search cohorts outperform New Nonbrand segments by a 10% to 15% margin across all timeframes and devices. The routing architecture aligns with this user behavior: `/lander-x` pages process nonbrand traffic, while the `/home` page is reserved for Direct, Brand, and Returning users. Operating as a navigation hub, the `/home` page maintains a 68%–75% conversion rate. The remaining top-funnel drop-offs represent the expected baseline of acquiring first-time buyers.

|<img width="1389" height="690" alt="image" src="https://github.com/user-attachments/assets/9a03bf39-15a3-4209-b03d-d52589222a15" />|
|:---------:|
|**Figure 4:** Top-Funnel CTR by Customer Segment and Landing Page Variant|

- **Main finding 3:** Mobile-specific routing improved mobile CTR, though a 10%–12% performance gap remains compared to desktop. Prior to mid-2013, mobile nonbrand traffic maintained a 28%–33% click-through rate (CTR) on the `/home` and `/lander-1` pages. The introduction of `/lander-3`, a dedicated mobile landing page, increased and stabilized the mobile CTR at 52%–54% through early 2015. Despite this increase, mobile performance continues to trail the desktop `/lander-5` benchmark by approximately 10%–12%, identifying mobile viewport optimization as the primary remaining action item at this stage.

|<img width="1033" height="518" alt="image" src="https://github.com/user-attachments/assets/305f02de-312d-4c8e-a678-8de09d92e5d5" />|
|:----------------:|
|**Figure 5:** Click-through rate Trend by device|

**Conclusion:**
>The top-funnel is functioning exactly as an optimized filter should. The remaining drop-offs are largely the natural friction of acquiring first-time buyers. The only actionable structural leak left at this stage is the ~10% performance gap on mobile devices, which requires a final round of mobile viewport optimization.

## **Stage 2:** Mid-Funnel Diagnostics (Detail View → Add-to-Cart)

***Key takeaway:*** The ~55% mid-funnel drop-off is a compound issue, driven by the conversion ceiling of the primary product (`Mr. Fuzzy`) and consistent friction on mobile devices across all product pages.

|<img width="1186" height="690" alt="image" src="https://github.com/user-attachments/assets/e005ec95-6531-4caf-a1f6-b30636b18736" />|
|:----------------:|
|**Figure 6:** Product Detail to Add-to-Cart Conversion Rate by Product|

- **Main finding 1:** The primary product, `/the-original-mr-fuzzy`, drives volume but represents the largest absolute drop-off. It accounts for 77.5% of product views but results in over 92,000 lost "Add-to-Cart" sessions due to its 43.04% CVR baseline. Newer products (`Love Bear` at 55.6% and `Mini Bear` at 65.1%) operate at higher conversion rates, but their overall impact is limited by lower traffic allocation.

- **Main finding 2:** The drop-off rate is higher on mobile devices across all products. For `/the-original-mr-fuzzy`, mobile PDP-to-ATC conversion lags desktop by 3.8 percentage points (40.1% vs. 43.9%). This consistent underperformance across the portfolio indicates a mobile-specific UX issue.

Table 2: Product Portfolio Conversion Performance (Aggregate 2012 - 2015)
| Product Landing Page | Total Detail Views | Sessions Added to Cart | View-to-Cart CVR | View-to-Cart CVR (Mobile Only) |
|:---|---:|---:|---:|---:|
| `/the-original-mr-fuzzy` | 162,525 | 69,957 | 43.04% | 40.13% |
| `/the-forever-love-bear` | 26,033 | 14,485 | 55.64% | 50.20% |
| `/the-birthday-sugar-panda` | 19,046 | 8,811 | 46.26% | 41.50% |
| `/the-hudson-river-mini-bear` | 2,610 | 1,700 | 65.13% | 60.30% |

- **Main finding 3** Assuming a uniform PDP layout template, the higher conversion rates of alternative SKUs indicate product-market fit rather than page design differences. The current user flow does not systematically direct traffic bouncing from the primary product to these alternatives.

**Conclusion:**
> Mitigating the 55% mid-funnel drop-off requires two actions. Operationally, a mobile PDP audit is needed to address CTA visibility. Strategically, implementing a cross-sell architecture (e.g., "Frequently Bought Together") on the primary product page will redirect bouncing users to the higher-converting secondary products.

## **Bottleneck 3 — Check-out funnel (Shipping → Billing → Purchased):**

***Key takeaway:*** The checkout flow outperforms global e-commerce benchmarks, indicating that bottom-funnel is highly optimized. The primary drop-off occurs at the initial Cart stage rather than during shipping or payment steps.

- **Main finding 1:** Overall cart abandonment of 65.97% falls below the global e-commerce benchmark of 69–72% ([source](https://baymard.com/lists/cart-abandonment-rate)). However, device-level breakdown reveals that desktop (63.00%) is driving this result, while mobile (77.23%) sits above benchmark — indicating the aggregate figure masks a structural mobile problem.

Table 3: Total Session and Conversion Rate of each Stage in Check-out Funnel 
|device|total cart sessions|	total shipping sessions|	cart to shipping cvr (%)|	total billing sessions|	shipping to billing cvr (%)| total success purchase|	billing to purchased cvr (%)|	cart abandonment rate (%)|
|:-----:|:-----:|:-----:|:-----:|:-----:|:-----:|:-----:|:-----:|:-----:|
mobile |	19798|	11792|	59.56|	8336 |	70.69|	4508 |	54.08|	77.23|
desktop|	75155|	52692|	70.11|	43722|	82.98|	27805|	63.59|	63.00|

- Main finding 2: Shipping cost is not a driver of drop-off. Of sessions reaching /shipping, 80.73% proceed to /billing — indicating that delivery terms are not a deterrent at this stage.

- Main finding 3: Payment friction was resolved through A/B testing. /billing-2 lifted billing-to-purchase CVR from 44.79% to 63.36% on desktop and from 34.55% to 55.09% on mobile — a sustained improvement that has held since September 2012.
  
Table 4: Billing Landing Page Performance
|Device|Page URL| Period|Total Billing Session|Successful Purchase|Billing to Successful Purchase CVR (%)|
|:-----|:-----:|:-----:|:-----:|:-----:|:-----:|
|desktop|/billing  |	3206	|1478|	46.10|
|desktop|/billing-2|	40516|	26327|	64.98|
|mobile|	/billing  |	411	|142	|34.55|
|mobile|	/billing-2|	7925|	4366|	55.09|

**Conclusion:**

>The checkout funnel performs within benchmark at the aggregate level, but this masks a mobile abandonment rate of 77.23% — 14 percentage points above desktop. The gap runs across all three checkout steps and is not explained by shipping cost or payment design, both of which have been addressed. Mobile checkout UX is the one remaining active problem at this stage.

# Recommendations:
Based on the insights and findings above, we would recommend the [stakeholder team] to consider the following:
|Priority|Observation|Recommendation|
|:------:|-------|-------|
|P1|consistent underperformance of mobile traffic across the funnel. Data indicates a ~10% performance gap at the acquisition stage (`/lander-3` vs. desktop equivalents) and a 3.8% lag in Product Detail Page (PDP) conversion.|Prioritize mobile viewport optimization for landing pages and ensure above-the-fold visibility for the "Add-to-Cart" CTA on all mobile product pages to eliminate systemic device friction.|
|P2|`/lander-5` matches `/home` on CTR for new desktop customers (61–63% vs. 61–65%) but records the lowest refund rate among active landing pages (4.07% vs. 4.28–4.40%). This indicates that `/lander-5` attracts higher-quality buyers, not just more clicks|Use `/lander-5` as the control baseline for any future desktop landing page experiments. Prioritize traffic allocation to `/lander-5` over other variants when acquisition quality — not just volume — is the objective|

# Assumptions and Caveats:

Throughout the analysis, multiple assumptions were made to manage challenges with the data. These assumptions and caveats are noted below:

**1. Null UTM campaign handling:**

For records in website_sessions where utm_campaign is missing (null), traffic is categorized using the following logic:

- ***Direct Traffic:*** Sessions where both utm_source and http_referer are null — users accessing via direct URL or bookmarks.
- ***Organic Search:*** Sessions where utm_source is null but http_referer contains search engine strings — unpaid search discovery.

**2. March 2015 YoY decline is a data artifact, not a business signal:**

The apparent decline in March 2015 is caused by the dataset ending on March 19 — creating an incomplete month compared to a full March 2014. Therefore, this should not be reported as a performance decline.
