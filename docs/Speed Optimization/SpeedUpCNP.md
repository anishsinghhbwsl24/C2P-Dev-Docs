
# Speedup Convert and Print

## Business Requirement

The primary goal was to **make the CNP application faster** by addressing performance issues. Users complained regarding **long startup time** and **slow tab switching** in the CNP app. Since this is a very broad scope with respect to the project, an initial analysis was done to identify the specific areas where improvement should be done first.

## Analysis and scope of development:

The key findings and the specific improvements were:

1.  **Duplicate Loading Issue in** `Main.cs`:
    -   The `Main.cs` file, which manages the Windows-like ribbon UI, was responsible for loading tabs.
    -   Due to its implementation, the **BedLayout tab was loading twice**, leading to redundant database queries to fetch the BedLayout orders.
    -   This issue was resolved by fixing the instantiation logic.
        
2.  **Optimizing Default Filters for BedLayout Tab:**
    
    -   Previously, the BedLayout tab fetched all orders using the filters: `JSONDownloaded`, `PDFCreated`, and `ToPrint` of all ShipBy dates. There was no date filter present due to which all orders were fetched based on the statuses. Since a BedLayout user would only print today's or future orders, loading orders of past dates was unnecessary.
    -   Two new filters were added, a From ShipBy date filter and a To ShipBy date filter. This helped to load only relevant orders in the BedLayout tab.
        
3.  **Improved Error Filtering:**
    
    -   The existing **error message filter** caused a full reload of the BedLayout tab's data source as the orders were refetched from the database.
    -   This was optimized by applying the filter **directly on the grid** rather than reloading the entire dataset.
        
4.  **Enhancing Tab Switching Performance:**
    
    -   Every time a new tab was opened, an **instance of the tab was stored in a container array**.
    -   These instances were **never destroyed**, causing old instances to temporarily reappear when switching tabs, further degrading performance.
    -   The fix involved simplifying instance management, ensuring old instances were properly disposed of when switching tabs.
