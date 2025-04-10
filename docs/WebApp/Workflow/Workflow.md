## **PDF Fixing Workflow**

The PDF generation process sometimes results in **misaligned signs**, requiring manual correction. The WebApp streamlines the workflow as follows:

### **1. Issue Detection**

-   PDFs with **alignment issues** are placed in a **specific directory for review**.
    

### **2. PDF Assignment & Fixing Process**

-   PDFs are categorized as **unassigned** or **assigned** to designers for correction.
    
-   Assigned PDFs appear based on the following filters:
    
    -   **shipBy** → Files with earlier **ship-by dates** are assigned first.
        
    -   **isSkipped** → Unskipped files are assigned first (**not used in the current WebApp version**).
        
    -   **orderType** → **Premium files** are assigned first.
        
    -   **updatedAt** → Files follow a **FIFO (First-In-First-Out)** order.
        
-   **Previously denied PDFs never appear again** in the WebApp.
    
-   Designers use **PhotoPea**, an online photo-editing tool, to **correct alignment issues**.
    
-   Once fixed, PDFs are moved to the **Fixed** folder, and their **status changes to "Ready to Print"**.

## **Deny Reasons**

-   When designers choose to **deny** a file, they are required to **provide a valid reason** for the denial.
    

## **Unassigned / My Items Preview**

-   The WebApp displays **unassigned files** and shows the **count** of these files.
    
-   **My Items** displays the files assigned to the **currently logged-in user**.
    
-   Users can also view the **list of approved items**.
    