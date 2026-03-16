# amazon-profit-analysis
# Amazon Marketplace Profitability Analysis

This project builds a SQL-based profitability mart for Amazon marketplace sales, aggregated by:

- month
- country
- item_code (SKU)

The goal is to calculate product-level and country-level profitability by combining sales, VAT, fees, reimbursements, refunds, shipping, ads, and COGS.

## Main Output Table

`gold.mart_profit_country_item_month`

### Columns

- `month` → month of transaction / order aggregation
- `country` → shipping country / marketplace country
- `item_code` → SKU or item identifier
- `qty_sold` → total quantity sold
- `gross_revenue` → gross sales revenue
- `vat_amount` → VAT separated from revenue
- `net_revenue` → revenue after VAT / promotions logic
- `cogs_total` → total cost of goods sold
- `provision_total` → marketplace commission / fees
- `shipping_total` → shipping-related cost
- `ad_spend_total` → advertising cost
- `refund_total` → customer refunds / returns
- `reimbursement_total` → reimbursements from Amazon
- `profit` → final profit
- `margin` → profit / net_revenue

## Profit Formula

```sql
profit =
  net_revenue
  - cogs_total
  - provision_total
  - shipping_total
  - ad_spend_total
  - refund_total
  + reimbursement_total
