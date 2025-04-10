## **Overview of WebApp**

The WebApp is designed to **automate the process of fixing PDF alignment issues** in **Sigo Signs**. It allows designers to efficiently **review, approve, or deny PDFs**, ensuring that only properly aligned signs proceed to printing. The system also **automates the movement of files** between different folders based on their status, eliminating manual file handling and improving workflow efficiency.

## **Requirements**

-   The WebApp eliminates the need for **manual file movement** by **automating directory changes**.
    
-   Designers only need to **approve or deny files**, making the process significantly faster.
    
-   Ensures that **only correctly aligned PDFs proceed to printing**, reducing **errors and material wastage**.
    

## **File Path Changes Based on Action**

### **Action Definitions**

-   **Before Fixing:** The file is initially placed in the **Exported PDF** directory but is moved to the **Staging** folder for further processing.
    
-   **Approved:** Once approved, the file is moved to the **Fixed** folder inside the **Exported PDF** directory, ensuring correct categorization.
    
-   **Denied:** If denied, the file remains in its original directory under **Exported PDF**, ensuring easy reference and tracking.

The WebApp manages the approval process and automatically updates file paths based on the action taken:

| Action         | Current Path                                                  | New Path After WebApp Update                                       |
|---------------|--------------------------------------------------------------|-------------------------------------------------------------------|
| **Before Fixing** | `\Exported PDF\3-21-2025\DIBOND\111-7536207-7777833-DIBOND.pdf` | `\Staging\3-21-2025\DIBOND\111-7536207-7777833-DIBOND.pdf`       |
| **Approved**   |      -                                                            | `\Exported PDF\3-21-2025\Fixed\DIBOND\111-7536207-7777833-DIBOND.pdf` |
| **Denied**     |      -                                                            | `\Exported PDF\3-21-2025\DIBOND\111-7536207-7777833-DIBOND.pdf`  |

        

This structured approach ensures proper file organization and seamless automation of the approval process.