# System Overview: C2P (Convert to Print) Order Management for Sigo Signs  
  
## Overview  
  
C2P (Convert to Print) is the order management system for Sigo Signs, handling orders from multiple sources, including Amazon and Magento-based websites. The system integrates with Teapplix, which serves as the central repository for all orders and their attributes.  
  
Orders are processed at both Item Level and Order Level, ensuring smooth tracking from creation to shipping.  
  
## Order Sources  
  
**Marketplaces:**  
  
Amazon  
SigoSigns Website ([sigosigns.com](http://sigosigns.com))  
  
**Order Management Platform:**  
  
**Teapplix** – The central source for all orders, containing attributes such as order details, item specifications, and customer information.  
  
## Order Processing Workflow  
  
**Step 1: Fetching Orders from Teapplix**  
  
**Module:** `GetOrdersTeapplix`  
**Function:** A cron job fetches orders from Teapplix and inserts them into the `OrderURLDownloads` table.  
  
**Database Information:**  
**SQL Database:** `SigoSingsDev`  
* **Tables where orders are stored:** `OrderURLDownload`  
  
  
**Initial Status:**  
* **Stock Orders:** `PDFStatus`: `ToPrint` (Ready for printing)  
* **Custom Orders:** `PDFStatus`: `JSONDownloaded` (Customization needed)  
**Populated Fields:**  
* `JSONFilePath` (for custom orders)  
* Other relevant order details  
  
**Step 2: PDF Generation**  
  
**Module:** `PDFGenerator`  
**Function:** Generates PDFs for custom orders.  
**Status Update:**  
* `PDFStatus`: `PDFCreated` (PDF is generated and stored)  
**Supporting Files (Art Files):**  
* Background files  
* Cut lines  
* Cut holes  
* Borders  
**Storage:**  
* Art files are stored in Dropbox  
* PDFs are saved with metadata such as ASIN, SKU, and SignSize  
  
**Step 3: Updating PDF Paths and Status**  
  
**Modules:**  
* `UpdatePDFFilePathsInDB`  
* `UpdatePDFStatusOnFolder`  
**Function:** After designers fix and move PDFs to a fixed folder, these modules update the status.  
**Final Status Before Printing:**  
* `PDFStatus`: `ToPrint`  
  
**Step 4: Printing & Order Fulfillment (C&P - Convert & Print)**  
  
Creation of beds from bed layout.  
Thermal Processing  
Printing, cutting, and engraving as required.  
Shipping  
Orders are routed for shipment after production is complete.  
  
## Order-Level Status Flow  
  
| Status Code | Description |  
| ------------------- | ----------------------------------------------- |  
| JSON Downloaded | (for custom orders) |  
| PDF Created | (custom orders only) |  
| To Print | (stock orders & processed custom orders) |  
| Sign on Bed | (processing stage) |  
| Routed / Printed | |  
| Shipped | |  
  
This workflow ensures an organized process from order retrieval to final shipping, maintaining efficiency in stock and custom order processing.


Customers can upload their own images to create a sign. However, these uploaded images may have:

-   **Poor quality or low resolution**, leading to **blurry or pixelated prints**.
    
-   **Smaller intrinsic dimensions** compared to the required print size.
    
-   A **specific DPI requirement** for printing, necessitating a higher-resolution image.
    

To ensure high-quality prints, the business requires **upscaling** of uploaded customer images before printing.
