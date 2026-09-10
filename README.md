# Inventory Management System (MySQL)

An enterprise-style Inventory Management System developed using MySQL for managing inventory lifecycle and supply chain operations. The system enables efficient handling of products, suppliers, warehouses, procurement, sales transactions, and stock movement while leveraging relational database design, automation through triggers and stored procedures, and data-driven reporting for operational insights.

---

## Project Overview

### Introduction

A SQL-based Inventory Management System developed using **MySQL** to efficiently manage and monitor inventory operations across products, suppliers, warehouses, and orders. The project demonstrates real-world database management concepts including inventory tracking, stock control, supplier management, purchase and sales processing, warehouse operations, automated stock updates, and business reporting.

### Project Description

Developed a scalable inventory management database using MySQL with 15+ relational tables, managing products, suppliers, customers, warehouses, purchases, sales, and inventory transactions for operational and business analysis. Automated core inventory operations using SQL triggers and stored procedures for stock updates, reorder monitoring, purchase processing, and inventory movement tracking.

---

## Business Domain

Retail, Wholesale, Warehouse, and Supply Chain Inventory Operations.

## Objectives

- Track inventory levels
- Manage suppliers
- Manage customers
- Record purchases
- Record sales
- Maintain warehouse stock
- Monitor inventory movement
- Support business reporting

## Business Problems Solved

- Overstocking
- Understocking
- Product traceability
- Supplier performance monitoring
- Customer order management
- Revenue analysis
- Inventory visibility across warehouses

## Users

- Administrators
- Inventory Managers
- Warehouse Staff
- Sales Executives
- Procurement Team

---

# Project Scope

## Included Modules

- Product Management
- Supplier Management
- Customer Management
- Purchase Orders
- Sales Orders
- Inventory Transactions
- Payment Management
- Reporting & Analytics

## Excluded Modules

- Accounting Ledger
- GST Filing
- Payroll
- Logistics Tracking
- Mobile Applications

---

# Functional Modules

## User Management
Maintain system users and roles.

## Supplier Management
Manage supplier master information.

## Product Catalog
Manage products, categories, and inventory items.

## Warehouse Management
Manage warehouse locations and capacities.

## Purchase Management
Track purchases from suppliers.

## Sales Management
Track customer sales orders and transactions.

## Inventory Control
Monitor incoming and outgoing stock movement.

## Payment Management
Track customer payments.

## Analytics Module
Generate inventory, revenue, and operational reports.

---

# Database Normalization

## First Normal Form (1NF)

- No repeating groups
- Atomic column values

## Second Normal Form (2NF)

- Full dependency on primary keys
- No partial dependencies

## Third Normal Form (3NF)

- No transitive dependencies
- Independent master entities

---

# Database Schema

## Roles

| Column | Description |
|----------|----------|
| RoleID (PK) | Role Identifier |
| RoleName | Role Name |
| Description | Role Description |

---

## Users

| Column | Description |
|----------|----------|
| UserID (PK) | User Identifier |
| RoleID (FK) | Reference to Roles |
| UserName | User Name |
| Email | User Email |
| Phone | Contact Number |
| CreatedDate | User Creation Date |

---

## Suppliers

| Column | Description |
|----------|----------|
| SupplierID (PK) | Supplier Identifier |
| SupplierName | Supplier Name |
| ContactPerson | Contact Person |
| Phone | Contact Number |
| Email | Supplier Email |
| City | Supplier City |
| State | Supplier State |
| Status | Active / Inactive |

---

## Categories

| Column | Description |
|----------|----------|
| CategoryID (PK) | Category Identifier |
| CategoryName | Category Name |
| Description | Category Description |

---

## SubCategories

| Column | Description |
|----------|----------|
| SubCategoryID (PK) | SubCategory Identifier |
| CategoryID (FK) | Reference to Categories |
| SubCategoryName | SubCategory Name |

---

## Products

| Column | Description |
|----------|----------|
| ProductID (PK) | Product Identifier |
| SubCategoryID (FK) | Reference to SubCategories |
| ProductName | Product Name |
| SKU | Stock Keeping Unit |
| UnitPrice | Product Price |
| ReorderLevel | Reorder Threshold |
| Status | Product Status |

---

## Warehouses

| Column | Description |
|----------|----------|
| WarehouseID (PK) | Warehouse Identifier |
| WarehouseName | Warehouse Name |
| City | Warehouse City |
| State | Warehouse State |
| Capacity | Warehouse Capacity |

---

## Customers

| Column | Description |
|----------|----------|
| CustomerID (PK) | Customer Identifier |
| CustomerName | Customer Name |
| Phone | Contact Number |
| Email | Customer Email |
| City | Customer City |
| CustomerType | Retail / Wholesale |

---

## PurchaseOrders

| Column | Description |
|----------|----------|
| PurchaseOrderID (PK) | Purchase Order Identifier |
| SupplierID (FK) | Reference to Suppliers |
| OrderDate | Purchase Date |
| OrderStatus | Order Status |
| TotalAmount | Total Purchase Amount |

---

## PurchaseOrderItems

| Column | Description |
|----------|----------|
| POItemID (PK) | Item Identifier |
| PurchaseOrderID (FK) | Purchase Order Reference |
| ProductID (FK) | Product Reference |
| Quantity | Ordered Quantity |
| UnitCost | Cost Per Unit |
| LineAmount | Total Item Amount |

---

## GoodsReceipts

| Column | Description |
|----------|----------|
| ReceiptID (PK) | Receipt Identifier |
| PurchaseOrderID (FK) | Purchase Order Reference |
| WarehouseID (FK) | Warehouse Reference |
| ReceiptDate | Goods Receipt Date |
| ReceivedBy | Receiving User |

---

## SalesOrders

| Column | Description |
|----------|----------|
| SalesOrderID (PK) | Sales Order Identifier |
| CustomerID (FK) | Customer Reference |
| OrderDate | Sales Date |
| OrderStatus | Order Status |
| TotalAmount | Total Sales Amount |

---

## SalesOrderItems

| Column | Description |
|----------|----------|
| SalesItemID (PK) | Sales Item Identifier |
| SalesOrderID (FK) | Sales Order Reference |
| ProductID (FK) | Product Reference |
| Quantity | Quantity Sold |
| UnitPrice | Selling Price |
| LineAmount | Total Item Amount |

---

## InventoryTransactions

| Column | Description |
|----------|----------|
| TransactionID (PK) | Transaction Identifier |
| ProductID (FK) | Product Reference |
| WarehouseID (FK) | Warehouse Reference |
| TransactionType | IN / OUT |
| Quantity | Transaction Quantity |
| TransactionDate | Transaction Date |

---

## Payments

| Column | Description |
|----------|----------|
| PaymentID (PK) | Payment Identifier |
| SalesOrderID (FK) | Sales Order Reference |
| Amount | Payment Amount |
| PaymentDate | Payment Date |
| PaymentMode | Cash / Card / UPI / Bank Transfer |

---

# Sample SQL Business Solutions

## Top 10 Customers by Revenue

### SQL Query

```sql
SELECT
    c.CustomerName,
    SUM(p.Amount) AS Revenue
FROM Customers c
JOIN SalesOrders so
    ON c.CustomerID = so.CustomerID
JOIN Payments p
    ON so.SalesOrderID = p.SalesOrderID
GROUP BY c.CustomerName
ORDER BY Revenue DESC
LIMIT 10;
```

### Business Use

Identify high-value customers and improve customer retention strategies.

---

## Products Never Sold

### SQL Query

```sql
SELECT ProductID, ProductName
FROM Products
WHERE ProductID NOT IN
(
    SELECT DISTINCT ProductID
    FROM SalesOrderItems
);
```

### Business Use

Identify dead inventory and optimize stock planning.

---

# Key Features

- Relational Database Design
- Third Normal Form (3NF)
- Inventory Tracking
- Warehouse Management
- Supplier & Customer Management
- Purchase & Sales Management
- Payment Tracking
- Inventory Analytics
- SQL Reporting
- Stored Procedures
- Triggers
- Views
- Business Intelligence Queries

---

# Technologies Used

- MySQL
- SQL
- ER Modeling
- Database Normalization
- Stored Procedures
- Triggers
- Views
- Joins
- Aggregate Queries

---

# Author

**Surekaa M**

Data Analyst | SQL Developer | Business Intelligence Enthusiast
