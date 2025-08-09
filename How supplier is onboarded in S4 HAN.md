**How supplier is onboarded in S4 HANA in detail**



Supplier onboarding in SAP S/4HANA is a structured process to ensure that a supplier is correctly created, maintained.



**Key Steps in BP Creation:**

T-Code: BP



Select Role: FLVN00 (Supplier - FI view)

Optionally add FLVN01 (Supplier - Purchasing)



Enter:



General Data (Name, Address, Language)



Company Code Data (Reconciliation Account, Payment Terms, Bank details)



Purchasing Org Data (Purchasing Group, Order Currency, Incoterms, Partner Functions)



Each BP is linked to one or more Company Codes and Purchasing Orgs.



Assign Accounting Information:



Reconciliation account



Payment terms



Tax indicators (Withholding Tax, VAT ID)



Assign Purchasing Information:



Order currency



Incoterms



GR-Based IV flag (for 3-way match)



Supplier Subrange (if applicable)



**Supplier Onboarding via Ariba SLP** 



📌 If using SAP Ariba Supplier Lifecycle \& Performance (SLP):

Supplier submits registration via Ariba Network.



Procurement team evaluates and approves supplier.



Approved supplier data is pushed to S/4HANA via SAP Cloud Integration Gateway (CIG) or SAP Master Data Integration (MDI).



In S/4HANA:



Data lands in Staging Area (if using MDG)



Approved Business Partner is created or updated



Role assignments like FLVN00, FLVN01 are made automatically



If you plan to send POs, RFQs, or Contracts to the supplier:



Ensure communication methods are maintained:



Email



EDI ID / cXML



Test by creating:



Purchase Requisition



Purchase Order



Goods Receipt



Invoice Verification

**How supplier data is pushed from S4 to ariba**



**Purpose of Supplier Data Sync**

Make sure supplier master data in S/4HANA is replicated in:



Ariba Buying



Ariba Contracts



Ariba Network (optional)



Enable accurate transactions like PO, invoice, confirmation, etc.



**What Data Is Pushed?**

Category	Examples

General Data	Supplier name, address, ANID

Purchasing Data	Purchasing Org, payment terms, incoterms

Company Code Data	Reconciliation account, payment methods

Contact Info	Email, phone, contact person

Classification	Commodity codes, supplier type





Integration Components

Component	Role

SAP S/4HANA	Source system of truth for supplier data

SAP CIG (Cloud Integration Gateway)	Middleware to map/convert ERP data to Ariba

Ariba Realm	Target for downstream consumption



**Supplier Sync Process: Step-by-Step**

✅ Step 1: Extract Supplier Data in S/4HANA

Use standard SAP programs:



ARBCIG\_MASTER\_DATA\_EXPORT



ARBCIG\_SUPPLIER\_EXPORT



This exports supplier master data into a CIG-compatible format (XML/cXML).



This program can be scheduled as a batch job (e.g., daily sync).



**tep 2: Mapping and Transformation via CIG**

Supplier data is passed through CIG.



CIG applies:



Field mappings (e.g., Vendor ID → Supplier ID)



Business rules (e.g., supplier partitioning, address handling)



Data is transformed into cXML format Ariba understands.



**✅ Step 3: Push to Ariba Buying / Contracts**

Data is transmitted to Ariba Realm (Buying/Contracts) using cXML over HTTPS.



The supplier gets created or updated in Ariba Supplier Database.



If the supplier is partitioned, it is available only to the associated business units



**Step 4: Validation in Ariba**

Ariba validates the data (e.g., mandatory fields, duplicates).



If successful, supplier is visible in:



Ariba Buying (Manage Suppliers)



Ariba Contracts (if relevant)



If failed, error messages are visible in CIG Monitor or Ariba Integration Logs.





credit memo



A credit memo:



* is a credit or refund from the supplier back to you
* may or may not be associated to a purchase order
* is at the line item level and never entered as a total amount only
* is entered the same way you enter an invoice; except the amount is negative
* is performed so that the invoice accumulation can be adjusted

invoice

contract request



Goods receipt



Goods Receipt (GR) in SAP Ariba is a crucial step in the procure-to-pay (P2P) process. A Goods Receipt is an electronic confirmation in Ariba that items or services corresponding to a purchase order have been delivered and accepted by the buying organization. It serves as proof of delivery and is often a prerequisite for invoice processing.



**Types of Goods Receipts**

Ariba supports various ways to record goods receipts, catering to different business needs:



**Manual Receipt (By Quantity/By Amount):**



By Quantity: This is the most common type. Users manually enter the exact quantity of items received against each line item of a Purchase Order (PO). This is crucial for physical goods where precise counts are needed.



By Amount: For certain services or non-tangible items, receipt might be recorded by the monetary value of the service completed or goods delivered, rather than a specific quantity.



**Auto-Receiving**: A powerful feature to automate the GR process for specific scenarios, reducing manual effort and speeding up the P2P cycle. Auto-receiving can be configured based on various parameters:



On Order Date: The system automatically generates a receipt as soon as the PO moves to "Ordered" status. This is suitable for very low-value items or services where immediate receipt confirmation is acceptable.



On Due Date: A receipt is automatically generated when the delivery due date for the items arrives. This assumes that goods will be delivered on time and is useful for recurring or predictable deliveries.



**No Receipt Required (2-Way Match)**: For some low-risk or specific purchases, the system might be configured not to require a goods receipt at all. In such cases, the invoice reconciliation becomes a "2-way match" (PO vs. Invoice), rather than a "3-way match" (PO vs. GR vs. Invoice). This simplifies the process but carries a higher risk if not properly managed.



**Partial Receipts**: Ariba allows for partial goods receipts, meaning you can record the receipt of only a portion of the ordered quantity. This is common when deliveries happen in installments. The PO remains open for the outstanding quantity until fully received or closed.



**Returns and Rejections:**



Return: If goods need to be sent back to the supplier (e.g., due to damage, incorrect item), a "negative receipt" can be recorded in Ariba, effectively reversing the original receipt. This updates the received quantity and typically triggers a credit memo process.



**Over-receiving \& under receiving**



This may be necessary for certain commodities, such as printed materials, where it is common to expect a greater quantity than ordered to allow for defects.



It is less common to allow for under receiving because most organizations will not allow purchase orders to be considered fully received until all quantities have been received.



You can accomplish this by setting the tolerance value to 0.



Normally, the quantities and amounts on a receipt match the quantities and amounts of the PO. However, you might receive fewer items or for a lesser amount than was specified on the PO (under-receiving), or you might receive more items or for a greater amount than specified on the PO (over-receiving). Under- and over-receiving is allowed and controlled by tolerances configured by your administrator.





**SES**



For service purchase orders, service entry sheets are documents created to capture the information about the services that have been provided.

Service sheets can be created by the supplier and submitted over the Ariba network, or they can be created by a user on behalf of the supplier.

Once the service entry sheets have been created, they must be approved to acknowledge that the services have actually been rendered.



**How to create a SES** 



Open corresponding PO. Option called Create Service entry sheet. Fill in all details such as Service start data, end date.





**Invoice**



The invoice process in SAP Ariba is a critical component of the procure-to-pay (P2P) cycle.



Invoice Submission

Suppliers can submit invoices to their buyers through SAP Ariba in several ways:



PO Flip Invoice (Ariba Network): This is the most common and preferred method. Suppliers receive a Purchase Order (PO) on the Ariba Network. They can then "flip" the PO into an invoice directly within their Ariba Network account. This method ensures that the invoice is inherently linked to the PO and often pre-populates many fields, reducing errors.



Non-PO Invoice (Ariba Network): For purchases made without a formal PO (e.g., certain services, utilities, or emergency purchases), suppliers can create and submit a "non-PO invoice" directly on the Ariba Network. These often require more robust approval workflows on the buyer's side.



Contract Invoice (Ariba Network): If the purchase is against a contract, suppliers can create an invoice referencing that contract, detailing services or goods delivered as per the contract terms.





**Invoice Validation and Reconciliation (Invoice Reconciliation - IR)**

Once an invoice is received in Ariba, it undergoes an automated validation and reconciliation process. Ariba creates an Invoice Reconciliation (IR) document for each invoice. This IR document serves as the central hub for matching and resolving discrepancies.



Key Matching Types:



2-Way Match (PO vs. Invoice): This is the simplest form. Ariba checks if the invoice details (supplier, PO number, quantity, price, amount) match the corresponding Purchase Order. This is typically used for services or non-inventory items where a goods receipt isn't required.



3-Way Match (PO vs. Goods Receipt vs. Invoice): This is the most common and robust matching type, particularly for physical goods. Ariba verifies that:



The invoice details match the Purchase Order.



The invoice quantity/amount matches the recorded Goods Receipt(s).



The Goods Receipt(s) match the Purchase Order.

This ensures that goods were ordered, received, and then invoiced correctly

