P2P Process



The Procure-to-Pay (P2P) process is a critical end-to-end business cycle within an organization that covers all activities from the initial identification of a need for goods or services, through procurement, receipt, and ultimately, payment to the supplier. Its primary goal is to ensure efficient, compliant, and cost-effective acquisition of necessary resources.



I typically break down the P2P process into these key stages:



Requisitioning (Need Identification):



This is where the process begins. An business user identifies a need for a good or service.



In a modern system like SAP Ariba Downstream, this is often done through Guided Buying. Users can easily search catalogs (hosted or PunchOut), select items, and fill out requisitions with details like quantity, delivery date, and cost center. This streamlines the process and ensures compliance with preferred suppliers and contracts. For non-catalog items, "ad-hoc" requisitions are created.



**Requisition Approval:**



Once a requisition is created, it enters an approval workflow. This ensures that the purchase is authorized, within budget, and compliant with company policies.



Ariba provides highly configurable workflows based on factors like spend amount, commodity, cost center, or project. This ensures proper governance and prevents unauthorized spending.



**Purchase Order (PO) Creation \& Dispatch:**



After approval, the requisition is converted into a Purchase Order. The PO is a formal document outlining the terms of the purchase (items, quantities, prices, delivery dates, payment terms).



The PO is then sent to the selected supplier.



In Ariba, POs are typically sent electronically via the Ariba Network, enabling immediate and traceable communication with suppliers. Suppliers can acknowledge receipt, provide order confirmations, and even submit Advance Ship Notices (ASNs) through the network.



**Goods Receipt (GR) / Service Entry Sheet (SES):**



This stage confirms that the ordered goods have been physically received, or services have been rendered.



For goods, a Goods Receipt is created, typically by the receiving department or the requester. It validates the quantity and condition of the delivered items against the PO.



For services, a Service Entry Sheet (SES) is created to confirm the completion of work or specific milestones.



Ariba facilitates this through user-friendly interfaces, often integrated with the backend ERP. A correct GR/SES is crucial for triggering the next step, especially for 3-way matching.



**Invoice Management:**



The supplier submits an invoice for the delivered goods or services.



Ariba Invoice Management is key here. Invoices are received electronically (via the Ariba Network, email, or OCR scanning).



The system then performs 2-way or 3-way matching.



2-way match: Invoice vs. Purchase Order (checking price and quantity).



3-way match: Invoice vs. Purchase Order vs. Goods Receipt/Service Entry Sheet (checking price, PO quantity, and received quantity).



If the invoice matches within pre-defined tolerances, it can be processed "touchlessly" for payment. If there are discrepancies, the invoice goes into an exception workflow, often involving collaborative dispute resolution with the supplier on the Ariba Network.



**Invoice Approval \& Payment:**



Once an invoice is matched and exceptions are resolved, it typically undergoes a final approval, especially for non-PO invoices or complex scenarios.



After approval, the invoice data is sent to the backend ERP system (e.g., SAP S/4HANA or ECC).



The ERP then processes the payment according to the agreed-upon terms, and the payment advice is often sent back to the supplier via the Ariba Network.



Key Benefits of an Optimized P2P Process (especially with Ariba):



Increased Efficiency \& Automation: Reduces manual effort and accelerates cycle times.



Cost Savings: Enforces contract compliance, identifies savings opportunities, and reduces maverick spend.



Improved Spend Visibility: Provides detailed insights into where money is being spent.



Enhanced Compliance \& Governance: Enforces procurement policies and approval rules.



Better Supplier Relationships: Streamlines collaboration and enables faster, more accurate payments.

