# BuyMore — Data Model

> Business-driven analytical data model for an independent Data Engineering & AI portfolio project

---

# 1. Purpose

The purpose of this document is to translate the BuyMore business processes and KPI framework into a structured analytical data model.

The design follows:

Business Process
↓
Business Question
↓
KPI
↓
Data Requirement
↓
Fact / Dimension
↓
Data Model
↓
Analytical Layer

The model is designed to support analysis across:

- Orders
- Products
- Brands
- Customers
- Inventory
- Warehouses
- Fulfillment
- Shipments
- Logistics
- Returns
- RTO
- Settlements
- Costs
- Business KPIs

---

# 2. Data Modeling Principles

## Principle 1 — Business-first modeling

Tables are created because a business process or KPI requires them.

---

## Principle 2 — Define grain before designing the table

Every fact table must have a clearly defined grain.

For example:

> One row per order item.

This prevents double counting.

---

## Principle 3 — Separate facts from descriptive entities

Transactional measurements belong in fact tables.

Descriptive business entities belong in dimension tables.

---

## Principle 4 — Preserve analytical history

Important attributes should support historical analysis where required.

---

## Principle 5 — Design for business questions

The model should allow analysts to answer:

- What happened?
- Where did it happen?
- When did it happen?
- Which brand / SKU / warehouse was involved?
- Why might it have happened?

---

# 3. Overall Data Architecture

The proposed analytical architecture follows a layered approach:

Source Data
↓
Raw Layer
↓
Bronze Layer
↓
Silver Layer
↓
Gold Layer
↓
Semantic / KPI Layer
↓
BI Dashboard
↓
AI / ML

---

# 4. Source Business Domains

The source data is organized into major business domains.

| Domain | Primary Entities |
|---|---|
| Commercial | Brand, Product, Order |
| Customer | Customer, Payment |
| Inventory | Inventory Snapshot, Inventory Movement |
| Warehouse | Warehouse, Warehouse Activity |
| Fulfillment | Order, Fulfillment |
| Logistics | Shipment, Shipment Event, Courier |
| Returns | Return, Return Reason |
| Finance | Settlement, Settlement Line, Cost |
| Geography | Location |
| Time | Date |

---

# 5. Star Schema Overview

The Gold analytical layer follows a star-schema approach.

Central business facts are connected to reusable dimensions.

The high-level structure is:

Dimensions
↓
Fact Tables
↓
Business KPIs

Major dimensions:

- Date
- Brand
- Product
- Customer
- Channel
- Marketplace
- Warehouse
- Courier
- Location
- Payment Method
- Return Reason
- Cost Type

Major facts:

- Order
- Order Item
- Inventory Snapshot
- Inventory Movement
- Shipment
- Shipment Event
- Return
- Settlement
- Cost
- Warehouse Activity

---

# 6. Dimension Tables

## 6.1 dim_date

### Purpose

Provide a reusable calendar dimension for time-based analysis.

### Grain

One row per calendar date.

### Key

date_key

### Important Attributes

- date_key
- full_date
- day
- day_name
- week
- month
- month_name
- quarter
- year
- financial_year
- financial_quarter
- is_weekend

### Used By

Almost every fact table.

---

# 7. dim_brand

### Purpose

Represent brands using the platform.

### Grain

One row per brand.

### Key

brand_key

### Attributes

- brand_key
- brand_id
- brand_name
- category_focus
- onboarding_date
- status

### Business Questions

- Which brands generate the most GMV?
- Which brands are most profitable?
- Which brands have high returns?

---

# 8. dim_product

### Purpose

Represent products and SKUs.

### Grain

One row per SKU.

### Key

product_key

### Attributes

- product_key
- product_id
- sku_id
- product_name
- brand_key
- category
- subcategory
- unit_price
- unit_cost
- weight
- launch_date
- status

### Relationships

brand_key → dim_brand

### Business Questions

- Which SKUs drive sales?
- Which SKUs have high returns?
- Which SKUs are slow-moving?

---

# 9. dim_customer

### Purpose

Represent customers.

### Grain

One row per customer.

### Key

customer_key

### Attributes

- customer_key
- customer_id
- customer_segment
- signup_date
- city
- state
- pincode
- acquisition_channel

### Business Questions

- Who are the most valuable customers?
- What is repeat purchase behavior?
- Which regions have high order volumes?

---

# 10. dim_channel

### Purpose

Represent commerce channels.

### Grain

One row per channel.

### Key

channel_key

### Attributes

- channel_key
- channel_id
- channel_name
- channel_type
- status

### Business Questions

- Which channels generate the most GMV?
- Which channels have the highest return rate?
- Which channels have settlement issues?

---

# 11. dim_marketplace

### Purpose

Represent marketplace or commerce platforms.

### Grain

One row per marketplace.

### Key

marketplace_key

### Attributes

- marketplace_key
- marketplace_id
- marketplace_name
- marketplace_type
- settlement_cycle
- status

### Business Questions

- Which marketplace generates the highest sales?
- Which marketplace has the largest settlement gap?

---

# 12. dim_warehouse

### Purpose

Represent warehouses used for inventory and fulfillment.

### Grain

One row per warehouse.

### Key

warehouse_key

### Attributes

- warehouse_key
- warehouse_id
- warehouse_name
- warehouse_type
- city
- state
- capacity_orders_per_day
- opening_date
- status

### Business Questions

- Which warehouses process the most orders?
- Which warehouses are approaching capacity?
- Which warehouses have poor SLA performance?

---

# 13. dim_courier

### Purpose

Represent logistics providers.

### Grain

One row per courier.

### Key

courier_key

### Attributes

- courier_key
- courier_id
- courier_name
- service_type
- status

### Business Questions

- Which courier has the best delivery SLA?
- Which courier has high RTO?
- Which courier has high delivery TAT?

---

# 14. dim_location

### Purpose

Provide reusable geographic information.

### Grain

One row per geographic location.

### Key

location_key

### Attributes

- location_key
- country
- state
- city
- pincode
- zone
- region

### Business Questions

- Which regions have high RTO?
- Where is demand concentrated?
- Where should inventory be positioned?

---

# 15. dim_payment_method

### Purpose

Represent payment methods used in transactions.

### Grain

One row per payment method.

### Key

payment_method_key

### Attributes

- payment_method_key
- payment_method
- payment_category

Example categories:

- Prepaid
- COD
- Other

### Business Questions

- Does payment method influence RTO?
- Does payment method influence returns?

---

# 16. dim_return_reason

### Purpose

Standardize return reasons.

### Grain

One row per return reason.

### Key

return_reason_key

### Attributes

- return_reason_key
- return_reason_code
- return_reason
- return_category

### Business Questions

- Why are customers returning products?
- Which product categories have quality-related returns?

---

# 17. dim_cost_type

### Purpose

Classify operational costs.

### Grain

One row per cost type.

### Attributes

- cost_type_key
- cost_type
- cost_category
- variable_fixed_flag

Potential categories:

- COGS
- Fulfillment
- Shipping
- Return
- RTO
- Marketplace Fee
- Packaging
- Other

---

# 18. Fact Tables

The fact tables represent measurable business events.

---

# 19. fact_order

### Purpose

Represent the order-level business transaction.

### Grain

One row per order.

### Primary Key

order_key

### Important Columns

- order_key
- order_id
- date_key
- brand_key
- customer_key
- channel_key
- marketplace_key
- warehouse_key
- location_key
- payment_method_key
- order_timestamp
- order_status
- gross_order_value
- discount_amount
- net_order_value
- tax_amount
- cancellation_flag

### Measures

- Gross Order Value
- Discount
- Net Order Value
- Tax

### Business Questions

- How many orders were created?
- What is total order value?
- Which brands generate the most orders?

---

# 20. fact_order_item

### Purpose

Represent individual products within orders.

### Grain

One row per order item.

### Primary Key

order_item_key

### Foreign Keys

- order_key
- product_key
- brand_key
- channel_key
- date_key

### Important Columns

- order_item_key
- order_key
- product_key
- quantity
- unit_price
- gross_item_value
- discount_amount
- net_item_value
- unit_cost
- cogs

### Measures

- Quantity
- Gross Item Value
- Discount
- Net Item Value
- COGS

### Business Questions

- Which SKUs generate the most sales?
- Which products have the highest contribution?
- Which categories are growing?

---

# 21. fact_inventory_snapshot

### Purpose

Represent inventory position at a specific point in time.

### Grain

One row per SKU + Warehouse + Date.

### Primary Key

inventory_snapshot_key

### Foreign Keys

- date_key
- product_key
- brand_key
- warehouse_key

### Important Columns

- inventory_snapshot_key
- date_key
- product_key
- brand_key
- warehouse_key
- on_hand_qty
- reserved_qty
- blocked_qty
- available_qty
- unit_cost
- inventory_value

### Measures

- On-Hand Quantity
- Reserved Quantity
- Blocked Quantity
- Available Quantity
- Inventory Value

### Business Questions

- Where are stockouts occurring?
- Which warehouses hold the most inventory?
- Which SKUs have excess inventory?

---

# 22. fact_inventory_movement

### Purpose

Track changes in inventory.

### Grain

One row per inventory movement event.

### Primary Key

inventory_movement_key

### Foreign Keys

- date_key
- product_key
- warehouse_key

### Important Columns

- inventory_movement_key
- movement_id
- movement_timestamp
- movement_type
- quantity
- reference_type
- reference_id

### Movement Types

- Purchase
- Sale
- Return
- Transfer In
- Transfer Out
- Adjustment
- Damage
- Write-off

### Business Questions

- Why did inventory change?
- How much inventory entered or left the warehouse?

---

# 23. fact_shipment

### Purpose

Represent shipment-level logistics activity.

### Grain

One row per shipment.

### Primary Key

shipment_key

### Foreign Keys

- order_key
- warehouse_key
- courier_key
- location_key
- date_key

### Important Columns

- shipment_key
- shipment_id
- order_key
- warehouse_key
- courier_key
- origin_location_key
- destination_location_key
- shipment_timestamp
- delivered_timestamp
- shipment_status
- promised_delivery_date
- shipping_cost
- delivery_tat
- delivery_sla_flag
- rto_flag

### Measures

- Shipping Cost
- Delivery TAT
- SLA Flag
- RTO Flag

### Business Questions

- Which courier performs best?
- Which regions have delivery delays?
- Where is RTO increasing?

---

# 24. fact_shipment_event

### Purpose

Capture the detailed lifecycle of a shipment.

### Grain

One row per shipment event.

### Primary Key

shipment_event_key

### Foreign Keys

- shipment_key
- date_key
- location_key

### Important Columns

- shipment_event_key
- shipment_key
- event_timestamp
- event_type
- event_location_key
- event_status
- failure_reason

### Example Events

- Created
- Picked Up
- In Transit
- Out for Delivery
- Delivered
- NDR
- RTO Initiated
- RTO Delivered

### Business Questions

- Where did a shipment fail?
- How long did each stage take?
- Where are delivery bottlenecks occurring?

---

# 25. fact_return

### Purpose

Represent customer return transactions.

### Grain

One row per return transaction.

### Primary Key

return_key

### Foreign Keys

- order_key
- order_item_key
- product_key
- customer_key
- warehouse_key
- return_reason_key
- date_key

### Important Columns

- return_key
- return_id
- order_key
- order_item_key
- product_key
- return_timestamp
- return_status
- return_reason_key
- return_qty
- refund_amount
- return_cost
- restockable_flag

### Measures

- Return Quantity
- Refund Amount
- Return Cost

### Business Questions

- Which SKUs have high return rates?
- Why are customers returning products?
- How much value is being refunded?

---

# 26. fact_settlement

### Purpose

Represent financial settlement records.

### Grain

One row per settlement line.

### Primary Key

settlement_key

### Foreign Keys

- order_key
- brand_key
- marketplace_key
- date_key

### Important Columns

- settlement_key
- settlement_id
- order_key
- brand_key
- marketplace_key
- settlement_date
- gross_sales
- marketplace_fee
- shipping_deduction
- refund_deduction
- other_deduction
- expected_settlement
- actual_settlement
- settlement_gap
- reconciliation_status

### Measures

- Gross Sales
- Fees
- Deductions
- Expected Settlement
- Actual Settlement
- Settlement Gap

### Business Questions

- Where are settlement gaps occurring?
- Which channels have reconciliation issues?
- How much value remains unresolved?

---

# 27. fact_cost

### Purpose

Represent operational and financial cost events.

### Grain

One row per cost event.

### Primary Key

cost_key

### Foreign Keys

- order_key
- product_key
- brand_key
- warehouse_key
- cost_type_key
- date_key

### Important Columns

- cost_key
- cost_event_id
- order_key
- product_key
- brand_key
- warehouse_key
- cost_type_key
- cost_date
- cost_amount

### Business Questions

- What are the major cost drivers?
- Which brands have high fulfillment costs?
- Which orders have high operational cost?

---

# 28. fact_warehouse_activity

### Purpose

Represent warehouse operational activity.

### Grain

One row per warehouse activity record.

### Primary Key

warehouse_activity_key

### Foreign Keys

- warehouse_key
- date_key
- order_key

### Important Columns

- warehouse_activity_key
- warehouse_key
- order_key
- activity_timestamp
- activity_type
- processing_minutes
- labor_hours
- quantity_processed
- sla_flag

### Activity Types

- Picking
- Packing
- Quality Check
- Dispatch
- Receiving
- Putaway
- Return Processing

### Business Questions

- Which warehouses are under pressure?
- What is warehouse productivity?
- Where are fulfillment delays occurring?

---

# 29. Fact Table Summary

| Fact Table | Grain | Primary Business Process |
|---|---|---|
| fact_order | One row per order | Commerce |
| fact_order_item | One row per order item | Sales |
| fact_inventory_snapshot | SKU + Warehouse + Date | Inventory |
| fact_inventory_movement | One row per movement | Inventory |
| fact_shipment | One row per shipment | Logistics |
| fact_shipment_event | One row per shipment event | Logistics |
| fact_return | One row per return | Returns |
| fact_settlement | One row per settlement line | Finance |
| fact_cost | One row per cost event | Finance / Operations |
| fact_warehouse_activity | One row per activity | Warehouse |

---

# 30. Dimension Table Summary

| Dimension | Grain | Purpose |
|---|---|---|
| dim_date | One row per date | Time analysis |
| dim_brand | One row per brand | Brand analysis |
| dim_product | One row per SKU | Product analysis |
| dim_customer | One row per customer | Customer analysis |
| dim_channel | One row per channel | Channel analysis |
| dim_marketplace | One row per marketplace | Marketplace analysis |
| dim_warehouse | One row per warehouse | Warehouse analysis |
| dim_courier | One row per courier | Logistics analysis |
| dim_location | One row per location | Geography analysis |
| dim_payment_method | One row per payment method | Payment analysis |
| dim_return_reason | One row per return reason | Return analysis |
| dim_cost_type | One row per cost type | Cost analysis |

---

# 31. Key Relationships

The main analytical relationships are:

Brand
↓
Product
↓
Order Item
↓
Order

Customer
↓
Order

Channel
↓
Order

Marketplace
↓
Order
↓
Settlement

Warehouse
↓
Inventory
↓
Order
↓
Shipment

Order
↓
Shipment
↓
Shipment Event

Order
↓
Return

Order
↓
Cost

This creates an interconnected analytical model.

---

# 32. Simplified Entity Relationship View

The conceptual relationship can be represented as:

dim_brand
    ↓
dim_product
    ↓
fact_order_item
    ↓
fact_order
    ├── dim_customer
    ├── dim_channel
    ├── dim_marketplace
    ├── dim_warehouse
    ├── dim_location
    └── dim_payment_method

fact_order
    ↓
fact_shipment
    ↓
fact_shipment_event
    ├── dim_courier
    └── dim_location

fact_order
    ↓
fact_return
    └── dim_return_reason

fact_order
    ↓
fact_settlement

fact_order
    ↓
fact_cost
    └── dim_cost_type

dim_product
    ↓
fact_inventory_snapshot
    └── dim_warehouse

dim_product
    ↓
fact_inventory_movement
    └── dim_warehouse

dim_warehouse
    ↓
fact_warehouse_activity

---

# 33. Order-Centric Data Flow

The order is the central commercial transaction.

The analytical relationship is:

Order
↓
Order Items
↓
Products
↓
Brand

Order
↓
Fulfillment
↓
Shipment
↓
Shipment Events

Order
↓
Return

Order
↓
Settlement

Order
↓
Costs

This allows one transaction to be analyzed across:

Sales
+
Inventory
+
Operations
+
Logistics
+
Returns
+
Finance

---

# 34. KPI-to-Data Mapping

| KPI | Required Facts | Required Dimensions |
|---|---|---|
| GMV | fact_order_item | Date, Brand, Product, Channel |
| Orders | fact_order | Date, Brand, Channel |
| AOV | fact_order | Date, Brand, Channel |
| Contribution | Order + Cost + Settlement | Brand, Product, Channel |
| Stockout % | fact_inventory_snapshot | Product, Warehouse, Date |
| Inventory Turnover | Inventory + Order Item | Product, Warehouse, Date |
| Fulfillment SLA | fact_order / warehouse_activity | Warehouse, Date |
| Delivery SLA | fact_shipment | Courier, Location, Date |
| RTO % | fact_shipment | Courier, Brand, Location |
| Return Rate | fact_return + fact_order | Product, Brand, Date |
| Settlement Gap | fact_settlement | Brand, Marketplace, Date |
| Reconciliation % | fact_settlement | Marketplace, Brand, Date |

---

# 35. Grain Validation

Before implementing the model, every fact table must pass grain validation.

Examples:

fact_order:

One row = One Order

fact_order_item:

One row = One Product Line within an Order

fact_inventory_snapshot:

One row = One SKU + One Warehouse + One Date

fact_shipment:

One row = One Shipment

fact_shipment_event:

One row = One Shipment Event

fact_return:

One row = One Return Transaction

fact_settlement:

One row = One Settlement Line

fact_cost:

One row = One Cost Event

fact_warehouse_activity:

One row = One Warehouse Activity Record

---

# 36. Avoiding Double Counting

One of the most important data modeling risks is incorrect joins between facts.

For example:

One Order
↓
Multiple Order Items
↓
Multiple Shipment Events

If these are joined directly without aggregation, the order value can be duplicated.

Therefore analytical queries should respect fact grain.

Recommended approach:

Aggregate each fact to the required business grain
↓
Join aggregated results
↓
Calculate KPI

This is especially important for:

- Revenue
- GMV
- Contribution
- Shipping Cost
- Return Cost
- Settlement Gap

---

# 37. Surrogate Keys

The Gold dimensional model should use surrogate keys where appropriate.

Examples:

- brand_key
- product_key
- customer_key
- warehouse_key
- courier_key
- location_key

Business identifiers such as:

- brand_id
- product_id
- customer_id
- warehouse_id

can remain as natural/business keys.

This separates analytical relationships from source-system identifiers.

---

# 38. Slowly Changing Dimensions

Some dimensions may require historical tracking.

Potential examples:

- Brand
- Product
- Customer
- Warehouse

For example, if a product changes category, historical reporting may need to preserve the category that was valid when the transaction occurred.

The project can use a simplified Slowly Changing Dimension Type 2 approach where historical tracking is useful.

Typical fields:

- effective_from
- effective_to
- is_current

---

# 39. Data Layers

The model will eventually be implemented through three major processing layers.

## Bronze

Purpose:

- Preserve source structure
- Minimal transformation
- Add ingestion metadata
- Preserve raw records

---

## Silver

Purpose:

- Clean data
- Standardize types
- Resolve duplicates
- Validate relationships
- Apply business rules
- Create reusable entities

---

## Gold

Purpose:

- Analytical facts
- Analytical dimensions
- KPI-ready datasets
- Business-friendly structures

---

# 40. Data Quality Rules

The data model should enforce:

### Primary Key Rules

Every primary key must be unique.

### Foreign Key Rules

Foreign keys must resolve to valid dimension / parent records.

### Null Rules

Mandatory fields should not be null.

### Date Rules

Business timestamps should be logically consistent.

Example:

Shipment Timestamp
≤
Delivery Timestamp

### Quantity Rules

Inventory and order quantities should follow valid business constraints.

### Financial Rules

Expected settlement and actual settlement should be mathematically reproducible.

---

# 41. Business Rules

Important business rules include:

1. Every order must have at least one order item.
2. Every order item must reference a valid product.
3. Every product must belong to a valid brand.
4. Every shipment must reference an order.
5. A shipment can have multiple shipment events.
6. A return must reference an eligible order or order item.
7. A settlement line must reference a valid financial transaction.
8. Inventory must be associated with a product and warehouse.
9. Inventory movement must reference a valid product and warehouse.
10. Cost events must reference an appropriate cost category.
11. Delivery timestamp cannot occur before shipment timestamp.
12. Return timestamp should not precede order creation.
13. Settlement calculations must follow defined financial rules.

---

# 42. Analytical Data Flow

The final data flow will be:

Source Data
↓
Raw
↓
Bronze
↓
Data Quality
↓
Silver
↓
Business Transformations
↓
Gold Facts + Dimensions
↓
KPI Layer
↓
Power BI
↓
AI / ML

---

# 43. Data Model and Future AI

The data model is also designed to support future machine learning.

Examples:

### Demand Forecasting

Inputs:

- Historical sales
- Product
- Brand
- Date
- Channel
- Seasonality
- Inventory

Target:

Future demand

---

### RTO Prediction

Inputs:

- Customer
- Location
- Payment Method
- Product
- Channel
- Courier
- Historical RTO

Target:

RTO probability

---

### Inventory Risk

Inputs:

- Sales velocity
- Inventory
- Demand trend
- Return rate
- Lead time assumptions

Target:

Inventory risk score

---

### Settlement Anomaly Detection

Inputs:

- Expected settlement
- Actual settlement
- Fees
- Deductions
- Historical settlement behavior

Target:

Anomaly / normal

---

# 44. Recommended Gold Layer

The Gold layer should contain business-ready tables.

Suggested structure:

gold_fact_order
gold_fact_order_item
gold_fact_inventory_snapshot
gold_fact_inventory_movement
gold_fact_shipment
gold_fact_shipment_event
gold_fact_return
gold_fact_settlement
gold_fact_cost
gold_fact_warehouse_activity

and:

gold_dim_date
gold_dim_brand
gold_dim_product
gold_dim_customer
gold_dim_channel
gold_dim_marketplace
gold_dim_warehouse
gold_dim_courier
gold_dim_location
gold_dim_payment_method
gold_dim_return_reason
gold_dim_cost_type

The naming convention can be adjusted during implementation.

---

# 45. Data Model Implementation Strategy

Implementation should follow this sequence:

1. Create dimensions.
2. Validate dimension keys.
3. Create order facts.
4. Create inventory facts.
5. Create logistics facts.
6. Create return facts.
7. Create settlement facts.
8. Create cost facts.
9. Create warehouse activity facts.
10. Validate relationships.
11. Validate grain.
12. Validate KPI calculations.

---

# 46. Data Model to SQL Mapping

The model will later be implemented using SQL.

Examples:

fact_order
↓
orders table

fact_order_item
↓
order_items table

fact_inventory_snapshot
↓
inventory_snapshot table

fact_shipment
↓
shipments table

fact_return
↓
returns table

fact_settlement
↓
settlements table

fact_cost
↓
costs table

The exact physical naming convention can be finalized during the engineering stage.

---

# 47. Data Model to PySpark Mapping

PySpark will be responsible for:

- Reading source data
- Schema enforcement
- Cleaning
- Deduplication
- Validation
- Joining reference data
- Business transformations
- Writing Bronze
- Writing Silver
- Writing Gold

The objective is to demonstrate a realistic data engineering pipeline rather than simply loading CSV files into Spark.

---

# 48. Data Model to BI Mapping

Power BI will consume Gold-level analytical tables.

Potential dashboards:

### Executive Dashboard

- GMV
- Revenue
- Contribution
- Orders
- AOV
- RTO
- Return Rate
- Settlement Gap

### Inventory Dashboard

- Stockout
- Inventory Value
- Inventory Days
- Slow-Moving SKUs
- Warehouse Inventory

### Operations Dashboard

- Fulfillment SLA
- Order Ageing
- Warehouse Productivity
- Capacity Utilization

### Logistics Dashboard

- Delivery SLA
- Delivery TAT
- RTO
- NDR
- Courier Performance

### Finance Dashboard

- Expected Settlement
- Actual Settlement
- Settlement Gap
- Reconciliation %

---

# 49. Data Model Summary

The data model converts the business into an analytical structure.

Business Process
↓
Data Entity
↓
Fact / Dimension
↓
Business Grain
↓
Relationships
↓
KPI
↓
Dashboard
↓
Decision

The central design principle is:

> The data model exists to make business questions answerable.

---

# 50. Next Stage

The next stage is:

**Synthetic Data Design & Generation**

The data generation stage will define:

- Source datasets
- Record volumes
- Column definitions
- Data types
- Relationships
- Distribution rules
- Business scenarios
- Data quality scenarios
- Reproducibility
- Generation scripts

The synthetic dataset must be realistic enough to exercise the data engineering pipeline and produce meaningful business analysis.

---

# Research & Portfolio Disclaimer

This is an independent research and portfolio project based on publicly available information about BuyMore / Counfreedise Retail Services Ltd. and analytical assumptions where company-specific information is not publicly disclosed.

This project is **not affiliated with, endorsed by, or produced by BuyMore**.

The tables, entities, columns, relationships, grains, keys, business rules, architecture, data layers and technical implementation described in this document are proposed designs created for learning, research, simulation and portfolio purposes.

They should not be interpreted as BuyMore's actual internal database schema, data architecture, technology stack, proprietary processes, operational systems or confidential information.

Where company-specific information is unavailable, the design uses analytical assumptions to create a realistic e-commerce data engineering scenario.

No confidential, private, proprietary or non-public company information has been used.

This document is intended solely for **educational, research and portfolio demonstration purposes**.