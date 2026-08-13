# BuyMore — KPI Framework

> Business-first KPI framework for an independent Data Engineering & AI portfolio project

---

# 1. Purpose

The purpose of this KPI framework is to translate the BuyMore business model and value chain into measurable business outcomes.

The framework connects:

Business Objective  
↓  
Business Question  
↓  
KPI  
↓  
Formula  
↓  
Data Required  
↓  
Business Interpretation  
↓  
Decision

The KPIs are designed to support analysis across:

- Growth
- Revenue
- Profitability
- Inventory
- Warehouse Operations
- Fulfillment
- Logistics
- Customer Returns
- RTO
- Finance
- Settlement Reconciliation
- Data Quality

---

# 2. KPI Design Principles

## Principle 1 — Every KPI must answer a business question

A KPI should not exist simply because the data is available.

Example:

RTO % is useful because it helps identify delivery and revenue-loss problems.

---

## Principle 2 — KPI definitions must be explicit

Every KPI should have:

- Definition
- Formula
- Grain
- Dimensions
- Data source
- Interpretation
- Decision supported

---

## Principle 3 — Financial KPIs must reconcile

Revenue and contribution KPIs should be traceable back to transactional data.

---

## Principle 4 — Operational KPIs should identify bottlenecks

The objective is not only to measure performance.

The objective is to identify:

> Where is the operational problem occurring?

---

## Principle 5 — KPIs should support action

A useful KPI should help someone make a decision.

---

# 3. KPI Hierarchy

The KPI framework is organized into major business areas:

- Growth
- Profitability
- Inventory
- Warehouse Operations
- Fulfillment
- Logistics
- Customer
- Returns
- RTO
- Finance
- Data Quality

The executive layer should consolidate the most important metrics from these areas.

---

# 4. Executive KPI Layer

The executive dashboard should focus on a small set of high-value metrics.

| Business Area | KPI | Purpose |
|---|---|---|
| Growth | GMV | Measure merchandise value |
| Growth | Net Revenue | Measure realized sales value |
| Growth | Orders | Measure transaction volume |
| Growth | AOV | Measure average order value |
| Profitability | Contribution | Measure economic value after major costs |
| Profitability | Contribution Margin % | Measure profitability quality |
| Inventory | Stockout % | Measure inventory availability risk |
| Inventory | Inventory Turnover | Measure inventory efficiency |
| Operations | Fulfillment SLA % | Measure warehouse execution |
| Logistics | Delivery SLA % | Measure logistics performance |
| Logistics | RTO % | Measure failed delivery risk |
| Customer | Return Rate % | Measure post-delivery return behavior |
| Finance | Settlement Gap | Measure financial reconciliation risk |
| Finance | Reconciliation % | Measure financial control |

The executive layer should also show:

- Current value
- Previous period
- Trend
- Target
- Variance
- Business interpretation

---

# 5. Growth KPIs

## 5.1 GMV

### Definition

Gross Merchandise Value represents the gross value of merchandise sold through the commerce operation before deductions such as discounts, refunds and operational costs.

### Formula

GMV = Sum of Gross Item Value

### Grain

Order Item

### Dimensions

- Date
- Brand
- Product
- SKU
- Category
- Channel
- Marketplace

### Business Question

> How much merchandise value is being generated?

### Decision Supported

- Growth planning
- Brand performance
- Channel strategy
- Category strategy

---

# 6. Net Sales

### Definition

Net Sales represent merchandise value after applicable discounts and transaction adjustments.

### Formula

Net Sales = Gross Sales - Discounts + Applicable Tax Adjustments

The exact accounting definition should be aligned with the organization's finance policy.

### Grain

Order Item

### Business Question

> How much sales value remains after commercial discounts?

---

# 7. Revenue

Revenue should represent the value recognized according to the business's accounting treatment.

For this portfolio project, revenue is treated as an analytical metric derived from eligible transactions.

### Formula

Revenue = Sum of Net Order Value

### Important Note

Revenue recognition can differ from GMV.

Therefore:

> GMV ≠ Revenue

### Business Question

> How much commercial value is actually recognized?

---

# 8. Orders

### Definition

Number of unique orders created during the reporting period.

### Formula

Orders = Count Distinct Order ID

### Grain

Order

### Dimensions

- Date
- Brand
- Channel
- Marketplace
- Customer
- Geography

### Business Question

> How many transactions are being generated?

---

# 9. Average Order Value

### Definition

Average monetary value per eligible order.

### Formula

AOV = Net Order Value / Number of Eligible Orders

### Business Question

> How much value does the average order generate?

---

# 10. Order Growth %

### Formula

Order Growth % =

(Current Period Orders - Previous Period Orders)
/
Previous Period Orders
× 100

### Business Question

> Is transaction volume growing or declining?

---

# 11. GMV Growth %

### Formula

GMV Growth % =

(Current Period GMV - Previous Period GMV)
/
Previous Period GMV
× 100

### Business Question

> Is merchandise value growing?

---

# 12. Profitability KPIs

Revenue alone does not determine business quality.

A brand can generate high GMV while producing weak contribution because of:

- COGS
- Discounts
- Marketplace fees
- Fulfillment costs
- Shipping costs
- Returns
- RTO
- Other operational costs

Therefore the project introduces contribution-based metrics.

---

# 13. COGS

### Definition

Cost of Goods Sold represents the product cost associated with sold units.

### Formula

COGS = Sum of Unit Cost × Quantity Sold

### Grain

Order Item

### Business Question

> What is the product cost associated with sales?

---

# 14. Fulfillment Cost

### Definition

Operational cost associated with processing an order through warehouse fulfillment.

Potential components include:

- Picking
- Packing
- Handling
- Processing

### Formula

Fulfillment Cost = Sum of Fulfillment Costs

### Business Question

> How much does it cost to process orders?

---

# 15. Shipping Cost

### Definition

Cost associated with delivering a shipment.

### Formula

Shipping Cost = Sum of Shipment Shipping Cost

### Business Question

> How much are logistics operations costing?

---

# 16. Marketplace / Channel Fees

### Definition

Fees or deductions associated with the commerce channel.

### Formula

Marketplace Fees = Sum of Applicable Channel Fees

### Business Question

> How much commercial value is consumed by channel fees?

---

# 17. Contribution

### Definition

Contribution measures the economic value remaining after major variable costs.

### Analytical Formula

Contribution =

Net Order Value
- COGS
- Marketplace Fees
- Fulfillment Cost
- Shipping Cost
- Return / RTO Cost
- Other Variable Costs

### Business Question

> How much economic value remains after serving the order?

### Decision Supported

- Brand profitability
- Product profitability
- Channel profitability
- Pricing decisions
- Cost optimization

---

# 18. Contribution Margin %

### Formula

Contribution Margin % =

Contribution
/
Net Order Value
× 100

### Business Question

> What percentage of order value remains as contribution?

---

# 19. Cost per Order

### Formula

Cost per Order =

Total Variable Operating Cost
/
Eligible Orders

### Business Question

> What is the average variable cost of serving an order?

---

# 20. High-GMV / Low-Margin Detection

This is a derived business analysis rather than a single KPI.

A brand can be classified as:

- High GMV / High Margin
- High GMV / Low Margin
- Low GMV / High Margin
- Low GMV / Low Margin

This creates a useful management matrix:

| | Low Contribution Margin | High Contribution Margin |
|---|---|---|
| High GMV | Margin Risk | Growth Star |
| Low GMV | Weak Brand | Opportunity |

### Business Question

> Are we growing profitably?

---

# 21. Inventory KPIs

Inventory is a critical working-capital and customer-service metric.

---

# 22. On-Hand Inventory

### Definition

Quantity physically available in warehouse stock before operational reservations and blocks.

### Formula

On-Hand Inventory = Sum of On-Hand Quantity

### Dimensions

- Date
- Warehouse
- Brand
- Product
- SKU

### Business Question

> How much physical inventory exists?

---

# 23. Available Inventory

### Formula

Available Inventory =

On-Hand Quantity
- Reserved Quantity
- Blocked Quantity

### Business Question

> How much inventory can actually be allocated?

---

# 24. Inventory Value

### Formula

Inventory Value =

Available Quantity × Unit Cost

### Business Question

> How much capital is tied up in inventory?

---

# 25. Stockout Rate %

### Definition

Percentage of SKU-location observations where available inventory is zero.

### Formula

Stockout % =

Stockout SKU-Location Observations
/
Total SKU-Location Observations
× 100

### Business Question

> Where are we unable to fulfill demand because stock is unavailable?

---

# 26. Days of Inventory

### Definition

Estimated number of days current inventory can support future demand.

### Formula

Days of Inventory =

Available Inventory
/
Average Daily Demand

### Business Question

> How long can current inventory support expected demand?

---

# 27. Inventory Turnover

### Formula

Inventory Turnover =

COGS
/
Average Inventory Value

### Business Question

> How efficiently is inventory being converted into sales?

---

# 28. Slow-Moving Inventory

A SKU can be classified as slow-moving when demand remains below a defined threshold for a sustained period.

Potential indicators:

- Low sales velocity
- High inventory days
- Low recent demand
- High inventory value

### Business Question

> Which inventory is tying up working capital without sufficient demand?

---

# 29. Inventory Risk Score

A future derived score can combine:

- Stockout risk
- Demand volatility
- Inventory days
- Sales velocity
- Return rate

### Business Question

> Which SKUs require immediate inventory attention?

---

# 30. Warehouse KPIs

Warehouse performance directly affects fulfillment.

---

# 31. Orders Processed

### Formula

Orders Processed =

Count of orders successfully fulfilled

### Business Question

> How much workload is each warehouse handling?

---

# 32. Warehouse Productivity

A possible analytical measure is:

Warehouse Productivity =

Orders Processed
/
Labor Hours

The exact operational definition should depend on available labor data.

### Business Question

> How efficiently is warehouse capacity being utilized?

---

# 33. Fulfillment SLA %

### Definition

Percentage of orders fulfilled within the required operational SLA.

### Formula

Fulfillment SLA % =

Orders Fulfilled Within SLA
/
Eligible Fulfillment Orders
× 100

### Business Question

> Are warehouses processing orders on time?

---

# 34. Order Processing Time

### Formula

Processing Time =

Fulfillment Completion Timestamp
-
Order Timestamp

### Business Question

> How long does it take to process an order?

---

# 35. Order Ageing

Orders can be grouped into ageing buckets:

- 0–24 hours
- 24–48 hours
- 48–72 hours
- 72+ hours

### Business Question

> How much operational backlog exists?

---

# 36. Warehouse Capacity Utilization

### Formula

Capacity Utilization =

Orders Processed
/
Warehouse Capacity
× 100

### Business Question

> Which warehouses are approaching capacity?

---

# 37. Logistics KPIs

---

# 38. Delivery TAT

### Definition

Time from shipment dispatch to successful delivery.

### Formula

Delivery TAT =

Delivery Timestamp
-
Shipment Timestamp

### Business Question

> How long does it take to deliver an order?

---

# 39. Delivery SLA %

### Formula

Delivery SLA % =

Shipments Delivered Within SLA
/
Eligible Delivered Shipments
× 100

### Business Question

> Are customers receiving orders within the expected timeframe?

---

# 40. On-Time Delivery %

### Formula

On-Time Delivery % =

On-Time Deliveries
/
Total Delivered Shipments
× 100

This KPI can be similar to Delivery SLA depending on the business definition.

---

# 41. NDR Rate %

### Definition

Percentage of shipments experiencing a non-delivery report/event.

### Formula

NDR % =

Shipments With NDR
/
Total Shipments
× 100

### Business Question

> How frequently are delivery attempts failing?

---

# 42. RTO Rate %

### Definition

Percentage of shipments returned to origin after unsuccessful delivery.

### Formula

RTO % =

RTO Shipments
/
Total Shipped Orders
× 100

### Dimensions

- Geography
- Courier
- Brand
- SKU
- Channel
- Payment Method

### Business Question

> Where are failed deliveries occurring?

---

# 43. RTO Cost

### Formula

RTO Cost =

Forward Shipping Cost
+
Reverse Shipping Cost
+
RTO Handling Cost
+
Other RTO Costs

### Business Question

> How much financial impact is caused by failed deliveries?

---

# 44. Return KPIs

---

# 45. Return Rate %

### Formula

Return Rate % =

Returned Orders
/
Delivered Orders
× 100

### Business Question

> What percentage of successful deliveries result in returns?

---

# 46. Refund Value

### Definition

Total monetary value refunded for customer returns and applicable cancellations.

### Formula

Refund Value = Sum of Refund Amount

### Business Question

> How much sales value is being reversed?

---

# 47. Return Cost

### Definition

Cost associated with processing returns.

### Formula

Return Cost = Sum of Return Processing Costs

### Business Question

> What is the operational cost of returns?

---

# 48. Return Reason Distribution

Returns should be analyzed by reason:

- Damaged
- Wrong item
- Quality issue
- Customer preference
- Size / fit
- Late delivery
- Not as expected

### Business Question

> Why are customers returning products?

---

# 49. Restockable Return %

### Formula

Restockable Return % =

Restockable Returned Units
/
Total Returned Units
× 100

### Business Question

> How much returned inventory can be recovered?

---

# 50. Customer KPIs

---

# 51. New Customers

### Formula

New Customers =

Count of customers whose first eligible order occurs during the period.

### Business Question

> How effectively are we acquiring customers?

---

# 52. Repeat Customer Rate

### Formula

Repeat Customer Rate =

Customers With More Than One Eligible Order
/
Active Customers
× 100

### Business Question

> How much customer activity comes from repeat buyers?

---

# 53. Orders per Customer

### Formula

Orders per Customer =

Eligible Orders
/
Active Customers

### Business Question

> How frequently are customers ordering?

---

# 54. Customer Revenue

### Formula

Customer Revenue =

Sum of Net Order Value by Customer

### Business Question

> Which customers contribute the most commercial value?

---

# 55. Financial Reconciliation KPIs

---

# 56. Expected Settlement

### Definition

Expected financial amount after known deductions.

### Formula

Expected Settlement =

Gross Sales
- Marketplace Fees
- Shipping Deductions
- Refund Deductions
- Other Deductions

### Business Question

> How much should the business receive?

---

# 57. Actual Settlement

### Definition

Actual amount received or recorded as settled.

### Formula

Actual Settlement =

Sum of Actual Settlement Amount

### Business Question

> How much was actually settled?

---

# 58. Settlement Gap

### Formula

Settlement Gap =

Expected Settlement
-
Actual Settlement

### Interpretation

Positive gap:

Potential under-settlement.

Negative gap:

Potential over-settlement or timing/accounting difference.

### Business Question

> Is there a difference between expected and actual settlement?

---

# 59. Settlement Gap %

### Formula

Settlement Gap % =

Absolute Settlement Gap
/
Expected Settlement
× 100

### Business Question

> How material is the reconciliation difference?

---

# 60. Reconciliation %

### Formula

Reconciliation % =

Reconciled Settlement Lines
/
Total Settlement Lines
× 100

### Business Question

> What percentage of settlement records are successfully reconciled?

---

# 61. Outstanding Reconciliation Value

### Formula

Outstanding Reconciliation Value =

Sum of Absolute Unreconciled Settlement Gaps

### Business Question

> How much financial value remains unresolved?

---

# 62. Data Quality KPIs

Data quality is itself a business capability.

---

# 63. Completeness %

### Formula

Completeness % =

Non-Null Required Values
/
Total Required Values
× 100

### Business Question

> Is required business data available?

---

# 64. Referential Integrity %

### Formula

Referential Integrity % =

Valid Foreign Key Records
/
Total Foreign Key Records