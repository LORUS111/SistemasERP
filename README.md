# SistemasERP
Este repositorio contiene la estructura lógica y los flujos de procesos basados en sistemas de gestión empresarial.

#Acerca del Proyecto
El objetivo de este proyecto es organizar y documentar las operaciones comerciales en departamentos claros, tales como:
* Ventas
* Compras
* Producción
* Servicio
* Inventario
* Finanzas e Informes

---

#Diagrama de Flujo de Procesos

Puedes ver la estructura de los procesos en el siguiente diagrama de flujo:

```mermaid
graph LR
    classDef crmSRM fill:#2E7D32,stroke:#fff,stroke-width:2px,color:#fff;
    classDef sales fill:#E65100,stroke:#fff,stroke-width:2px,color:#fff;
    classDef purchasing fill:#0277BD,stroke:#fff,stroke-width:2px,color:#fff;
    classDef production fill:#4A148C,stroke:#fff,stroke-width:2px,color:#fff;
    classDef service fill:#FBC02D,stroke:#fff,stroke-width:2px,color:#000;
    classDef inventory fill:#616161,stroke:#fff,stroke-width:2px,color:#fff;
    classDef finance fill:#D32F2F,stroke:#fff,stroke-width:2px,color:#fff;
    classDef reporting fill:#BA68C8,stroke:#fff,stroke-width:2px,color:#fff;

    %% Actores principales (CRM / SRM)
    Activities(("Activities")):::crmSRM
    Customer(("Customer")):::crmSRM
    Lead(("Lead")):::crmSRM
    Supplier(("Supplier")):::crmSRM
    BusinessPartnerMaster(("Business Partner Master")):::crmSRM

    %% Línea naranja (Sales)
    Customer --> Opportunity["Opportunity"]:::sales
    Opportunity --> Pricing["Pricing"]:::sales
    Pricing --> SalesQuotation["Sales Quotation"]:::sales
    SalesQuotation --> SalesOrder["Sales Order"]:::sales
    SalesOrder --> DeliveryNote["Delivery Note"]:::sales
    DeliveryNote --> ARInvoice["AR Invoice"]:::sales
    ARInvoice --> IncomingPayments["Incoming Payments"]:::sales

    %% Línea azul (Purchasing)
    Lead -.-> PurchaseRequest["Purchase Request"]:::purchasing
    PurchaseRequest --> PurchaseQuotation["Purchase Quotation"]:::purchasing
    PurchaseQuotation --> PurchaseOrder["Purchase Order"]:::purchasing
    PurchaseOrder --> GoodsReceiptPO["Goods Receipt PO"]:::purchasing
    GoodsReceiptPO --> APInvoice["AP Invoice"]:::purchasing
    APInvoice --> OutgoingPayments["Outgoing Payments"]:::purchasing

    %% Línea gris (Inventory)
    CustomerEquipmentCard(("Customer Equipment Card")):::inventory --> ItemMaster["Item Master"]:::inventory
    ItemMaster --> WarehouseManagement["Warehouse Management"]:::inventory
    WarehouseManagement --> SalesOrder
    ItemMaster --> PurchaseOrder
    DemandPlanning["Demand Planning"]:::inventory --> BackorderReporting["Backorder Reporting"]:::inventory

    %% Línea amarilla (Service)
    CustomerEquipmentCard -.-> ServiceCall["Service Call"]:::service
    ServiceCall --> ServiceContract["Service Contract"]:::service
    ServiceContract --> ServiceBilling["Service Billing"]:::service
    ServiceBilling -.-> FinancialPostings["Financial Postings"]:::finance

    %% Línea morada (Production)
    Supplier -.-> Sourcing["Sourcing"]:::production
    Sourcing --> ProductionOrder["Production Order"]:::production
    ProductionOrder --> IssueToProduction["Issue to Production"]:::production
    IssueToProduction --> ReceiptFromProduction["Receipt from Production"]:::production
    BillOfMaterials["Bill of Materials"]:::production --> MaterialRequirementsPlanning["Material Requirements Planning"]:::production
    MaterialRequirementsPlanning --> ProductionOrder

    %% Línea roja (Finance)
    ARInvoice --> AP_AR["AP / AR"]:::finance
    AP_AR --> CashManagement["Cash Management"]:::finance
    CashManagement --> Reconciliation["Reconciliation"]:::finance
    Reconciliation --> FinancialReporting["Financial Reporting"]:::finance
    ChartOfAccounts["Chart of Accounts"]:::finance --> GeneralLedgerAccounts["General Ledger Accounts"]:::finance
    GeneralLedgerAccounts --> GLAccountDetermination["G/L Account Determination"]:::finance
    GLAccountDetermination --> CostAccounting["Cost Accounting"]:::finance
    CostAccounting --> JournalEntries["Journal Entries"]:::finance

    %% Línea rosa (Reporting)
    InventoryAuditReport["Inventory Audit Report"]:::reporting --> AccountBalancesReport["Account Balances Report"]:::reporting
    AccountBalancesReport --> ProductReporting["Product Reporting"]:::reporting
