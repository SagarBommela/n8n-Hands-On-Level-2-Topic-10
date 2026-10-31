# Topic 10: Operational Data Management with Google Sheets

## 1. Overview

This project demonstrates an operational inventory and order tracking workflow using **n8n and a Mock Google Sheets API**.

The workflow processes customer orders, checks available inventory, updates stock quantities, records successful orders, and generates low-stock procurement alerts.

It also handles orders when sufficient stock is not available.

## 2. Objective

The main objective is to automate inventory and order management using n8n.

The workflow performs the following operations:

- Reads inventory records from the mock Google Sheets server.
- Validates stock availability for each order.
- Calculates the remaining stock quantity.
- Updates inventory after successful orders.
- Appends fulfilled orders to the orders ledger.
- Identifies low-stock items.
- Generates procurement reorder alerts.
- Rejects orders when stock is insufficient.
- Generates a final execution summary.

## 3. Technologies Used

- n8n – Workflow automation.
- JavaScript – Data processing and inventory calculations.
- HTTP Request – API communication.
- Webhook – Mock Google Sheets API endpoints.
- Postman – API testing.

## 4. Workflow Architecture

The project contains two workflows.

### Workflow 1: Mock Google Sheets Server

This workflow simulates Google Sheets operations without requiring Google OAuth credentials.

It provides the following API endpoints:

| Method | Endpoint | Purpose |
|---|---|---|
| GET | /mock/sheets/inventory | Read inventory records |
| PUT | /mock/sheets/inventory | Update stock quantity |
| POST | /mock/sheets/orders | Append fulfilled orders |
| GET | /mock/sheets/orders | Read orders ledger |
| POST | /mock/sheets/reset | Reset inventory and ledger |

### Workflow 2: Main Inventory Processing

The main workflow processes customer orders and manages inventory.

Main nodes:

1. Manual_Trigger
2. Code_SimulateOrders
3. Loop_Over_Orders
4. HTTP_GetInventoryRows
5. Code_ReconcileStock
6. IF_HasSufficientStock
7. Log_StockoutRejection
8. HTTP_UpdateInventoryRow
9. HTTP_AppendOrderLedger
10. IF_IsLowStockTrigger
11. Code_BuildReorderAlert
12. Code_FulfilledResult
13. Code_AuditSummary

## 5. Sample Order Scenarios

The workflow processes three sample orders.

| Order ID | SKU | Quantity | Expected Result |
|---|---|---:|---|
| ORD-7001 | SKU-KB-01 | 2 | Successfully fulfilled |
| ORD-7002 | SKU-MO-02 | 2 | Fulfilled with low-stock alert |
| ORD-7003 | SKU-DS-03 | 5 | Rejected due to insufficient stock |

## 6. Inventory Processing Logic

### Scenario 1: Normal Order

- SKU: SKU-KB-01
- Initial Stock: 25
- Ordered Quantity: 2
- Remaining Stock: 23

The order is fulfilled, and inventory is updated.

### Scenario 2: Low-Stock Order

- SKU: SKU-MO-02
- Initial Stock: 6
- Ordered Quantity: 2
- Remaining Stock: 4
- Reorder Point: 5

The order is fulfilled, and a procurement reorder alert is generated because the remaining stock is below the reorder point.

### Scenario 3: Out-of-Stock Order

- SKU: SKU-DS-03
- Initial Stock: 1
- Requested Quantity: 5

The order is rejected because sufficient stock is unavailable. Inventory is not deducted, and the order is not added to the ledger.

## 7. Testing

The following tests were performed:

- Verified inventory retrieval using the GET endpoint.
- Verified stock updates using the PUT endpoint.
- Verified order insertion using the POST endpoint.
- Tested normal order processing.
- Tested low-stock reorder alert generation.
- Tested insufficient stock rejection.
- Verified the final inventory quantities.
- Verified fulfilled orders in the orders ledger.
- Verified the final execution summary.

GIT Url:

https://github.com/SagarBommela/n8n-Hands-On-Level-2-Topic-10

Loom video:

https://www.loom.com/share/1f843f7576614f6e99edb19e87dd34b1







