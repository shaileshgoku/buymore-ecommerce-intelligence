# BuyMore — E-Commerce Intelligence Platform

> **Business-first Data Engineering & AI portfolio project**

## 📌 Project Overview

BuyMore is an e-commerce technology and operations company that provides end-to-end services across marketplace management, warehousing, order processing, fulfillment, analytics and financial reconciliation.

This project explores how an e-commerce operations business can transform fragmented operational data into a reliable analytical platform for business decision-making.

The project follows a **business-first approach**:

Business Understanding  
↓  
Business Model  
↓  
KPI Framework  
↓  
Data Model  
↓  
Synthetic Data  
↓  
Data Engineering  
↓  
Data Quality  
↓  
BI & Business Insights  
↓  
AI Use Cases

---

## 🎯 Business Problem

An end-to-end e-commerce operation generates data across multiple business processes:

- Orders
- Products & SKUs
- Brands
- Inventory
- Warehouses
- Fulfillment
- Shipments
- Couriers
- Returns
- RTO
- Marketplaces
- Settlements
- Operational costs

When these datasets exist independently, leadership may struggle to answer questions such as:

- Which brands are driving growth?
- Which brands are generating profitable growth?
- Where are stockouts occurring?
- Which SKUs are becoming slow-moving?
- Which warehouses are under operational pressure?
- Which couriers are causing delivery SLA failures?
- Where is RTO increasing?
- Are marketplace settlements being reconciled correctly?
- Where is margin leakage occurring?

This project designs a data platform to answer these questions.

---

# 🧠 Business-First Approach

This project intentionally starts with business understanding instead of immediately writing code.

### Step 1 — Understand the Business

Understand:

- Business model
- Value chain
- Customers
- Revenue streams
- Operational processes
- Business risks
- Decision-making requirements

### Step 2 — Define KPIs

Translate business objectives into measurable KPIs.

Examples:

- GMV
- Revenue
- Contribution Margin
- AOV
- Stockout Rate
- Inventory Turnover
- Fulfillment SLA
- Delivery SLA
- RTO %
- Return Rate
- Settlement Gap
- Reconciliation %

### Step 3 — Design the Data Model

Translate KPIs into:

- Fact tables
- Dimension tables
- Grain
- Relationships
- Business rules

### Step 4 — Engineer the Data

Build:

Raw Data → Bronze → Silver → Gold

using Python, PySpark and SQL.

### Step 5 — Build Business Intelligence

Create executive and operational dashboards to identify:

- Growth
- Profitability
- Inventory problems
- Operational bottlenecks
- Logistics issues
- Financial leakage

### Step 6 — Add AI

Use the analytical foundation to explore AI use cases such as:

- Demand forecasting
- Inventory optimization
- RTO prediction
- Settlement anomaly detection
- SKU risk scoring
- Operational alerts

---

# 🏗️ Architecture

                    BUSINESS SYSTEMS
                           │
        ┌──────────────────┼──────────────────┐
        │                  │                  │
    Commerce            Warehouse          Logistics
        │                  │                  │
        └──────────────────┼──────────────────┘
                           ↓
                    RAW SOURCE DATA
                           ↓
                       BRONZE
                           ↓
                    DATA QUALITY
                           ↓
                       SILVER
                           ↓
                    STAR SCHEMA
                           ↓
                         GOLD
                           ↓
                    KPI / SQL LAYER
                           ↓
                    BI DASHBOARD
                           ↓
                    AI / ML LAYER

---

# 📊 Core Business Processes

Brand
  ↓
Product / SKU
  ↓
Inventory
  ↓
Order
  ↓
Fulfillment
  ↓
Shipment
  ↓
Delivery
  ↓
Return / RTO
  ↓
Settlement
  ↓
Reconciliation
  ↓
Business Intelligence

---

# 🗃️ Data Model

The analytical model is based on a star-schema approach.

## Fact Tables

- `fact_order`
- `fact_order_item`
- `fact_inventory_snapshot`
- `fact_inventory_movement`
- `fact_shipment`
- `fact_shipment_event`
- `fact_return`
- `fact_settlement`
- `fact_cost`
- `fact_warehouse_activity`

## Dimension Tables

- `dim_date`
- `dim_brand`
- `dim_product`
- `dim_customer`
- `dim_marketplace`
- `dim_channel`
- `dim_warehouse`
- `dim_courier`
- `dim_location`
- `dim_return_reason`
- `dim_payment_method`
- `dim_cost_type`

---

# 📈 KPI Framework

| Business Area | Key KPIs |
|---|---|
| Growth | GMV, Revenue, Orders, AOV, Active Brands |
| Profitability | Contribution, Margin %, Cost / Order |
| Inventory | Stockout %, DOH, Inventory Turnover |
| Operations | Fulfillment SLA, Order Ageing, Warehouse Productivity |
| Logistics | Delivery SLA, Delivery TAT, RTO % |
| Customer | Return Rate, Refund Rate, Complaint Rate |
| Finance | Settlement Gap, Reconciliation %, Outstanding Amount |

---

# 🧪 Synthetic Dataset

This project uses **synthetic data** created specifically for research and portfolio purposes.

The prototype dataset contains approximately:

| Entity | Prototype Volume |
|---|---:|
| Brands | 100 |
| Products / SKUs | 500 |
| Customers | 5,000 |
| Orders | 20,000 |
| Order Items | 28,604 |
| Shipments | ~19K |
| Inventory Records | Prototype subset |
| Returns / RTO | Scenario-driven |
| Settlement Lines | ~19K |
| Cost Events | Multiple per order |

The generator uses deterministic random seeds so that the dataset can be reproduced.

---

# 🔍 Business Scenarios

The synthetic dataset contains controlled scenarios so the analytical system has real problems to investigate.

### Scenario 1 — Stockout Crisis

Selected high-demand SKU + warehouse combinations experience inventory shortages.

### Scenario 2 — High RTO Region

Selected geographic areas have elevated RTO probability.

### Scenario 3 — Courier Degradation

Selected courier performance deteriorates, increasing delivery TAT and SLA failures.

### Scenario 4 — Settlement Leakage

Selected settlement records contain controlled reconciliation gaps.

### Scenario 5 — Slow-Moving Inventory

Selected SKUs experience declining demand and increasing inventory days.

### Scenario 6 — High-Return SKU

Selected products have unusually high return rates.

### Scenario 7 — Warehouse Capacity Pressure

Selected warehouses experience increased order volumes and fulfillment delays.

### Scenario 8 — High-GMV / Low-Margin Brand

A brand generates strong sales volume but weak contribution margin.

---

# 🛠️ Technology Stack

### Data Generation

- Python
- Pandas
- NumPy
- Faker

### Data Engineering

- PySpark
- Spark SQL
- SQL

### Data Architecture

- Medallion Architecture
- Star Schema
- Fact & Dimension Modeling

### Analytics

- Power BI
- SQL
- Python

### AI / ML

Planned:

- Scikit-learn
- XGBoost
- Forecasting
- Anomaly Detection
- Predictive Modeling

### Development

- Git
- GitHub
- Jupyter

---

# 📂 Repository Structure

buymore-ecommerce-intelligence/
│
├── README.md
├── .gitignore
│
├── docs/
│   ├── 01-business-understanding/
│   ├── 02-business-model/
│   ├── 03-kpi-framework/
│   ├── 04-data-model/
│   └── 05-data-generation/
│
├── data/
│   └── sample/
│
├── src/
│   ├── generators/
│   ├── validators/
│   └── transformations/
│       ├── bronze/
│       ├── silver/
│       └── gold/
│
├── config/
│
├── notebooks/
│
├── sql/
│   ├── staging/
│   ├── dimensions/
│   ├── facts/
│   └── kpis/
│
├── dashboards/
│
├── tests/
│
└── assets/

---

# 🚦 Project Status

| Stage | Status |
|---|---|
| Business Understanding | ✅ Complete |
| Business Model | ✅ Complete |
| KPI Framework | ✅ Complete |
| Data Model | ✅ Complete |
| Synthetic Data Design | ✅ Complete |
| Prototype Data Generation | ✅ Complete |
| Data Quality Validation | 🔄 Next |
| PySpark Pipeline | ⏳ Planned |
| Gold Data Model | ⏳ Planned |
| SQL KPI Layer | ⏳ Planned |
| Power BI Dashboard | ⏳ Planned |
| AI Use Cases | ⏳ Planned |

---

# 🔍 Data Quality

The prototype currently validates:

- Primary-key uniqueness
- Foreign-key integrity
- Order → Order Item relationships
- Order → Shipment relationships
- Shipment → Event relationships
- Order → Return relationships
- Order → Settlement relationships
- Order → Cost relationships
- Shipment temporal consistency
- Delivery temporal consistency

All prototype validation checks currently pass.

---

# 💡 Future AI Use Cases

Once the analytical foundation is complete, the project will explore:

### Demand Forecasting

Predict SKU-level future demand to improve inventory planning.

### RTO Prediction

Predict orders with high RTO probability before shipment.

### Inventory Risk Scoring

Identify SKUs at risk of:

- Stockout
- Overstock
- Slow movement
- Dead stock

### Settlement Anomaly Detection

Identify unusual marketplace settlement discrepancies.

### Warehouse Risk Prediction

Predict potential SLA breaches based on:

- Order volume
- Capacity
- Processing time
- Historical performance

---

# 📚 Documentation

Detailed project documentation is available under:

`docs/`

The documentation follows the project lifecycle:

1. Business Understanding
2. Business Model
3. KPI Framework
4. Data Model
5. Synthetic Data Design
6. Data Engineering
7. Business Insights

---

# ⚠️ Research & Portfolio Disclaimer

This is an independent research and portfolio project based on publicly available information about BuyMore / Counfreedise Retail Services Ltd. and analytical assumptions where company-specific information is not publicly disclosed.

This project is **not affiliated with, endorsed by, or produced by BuyMore**.

The synthetic datasets, schemas, KPI targets, costs, volumes, business scenarios, assumptions and technical architecture are created for learning, research, simulation and portfolio purposes.

They should not be interpreted as BuyMore's actual internal data, database architecture, operational metrics, financial information, technology stack, proprietary processes or confidential information.

No confidential, private, proprietary or non-public company information has been used.