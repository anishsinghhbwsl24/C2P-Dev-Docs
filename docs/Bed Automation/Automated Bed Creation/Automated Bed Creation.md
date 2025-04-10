# Automated Bed Creation: Mixed Sizes

## Why Did We Need It?

For the Mixed Sizes bed type, as the name suggests, the sizes of the signs that go on the bed vary significantly—ranging from very small signs to very large ones, all placed together on the same bed.

For other bed types, such as Regular or Labels bed types, the signs on a bed are of the same size, allowing them to be placed in a regular grid-like fashion. However, this is not the case for the Mixed Sizes bed type. Due to irregular packing, space utilization was poor, leading to excessive material wastage. Since the bed material is expensive, every square inch of wasted space resulted in financial loss and environmental damage.

The previous algorithm used for creating a Mixed Sizes bed followed a greedy approach:

-   Beds were sorted in descending order based on sign dimensions.
    
-   The largest signs were placed from the bottom-left corner, stacking vertically with progressively smaller signs.
    
-   Once vertical space was exhausted, signs were placed horizontally.
    

This method led to high space wastage.

To improve space utilization, the problem was reframed as placing smaller rectangular signs onto a larger rectangular bed, which is a variant of the **Bin Packing Problem** (an NP-hard problem). Given the constraints, an approximate solution with fast performance was deemed sufficient. Various techniques and algorithms were researched, and the **3D Container Packing library** was chosen. This library implements the **EBAFIT algorithm**, which provides efficient packing solutions.

##  What Algorithmic Options Are Available?

### Available Options:

1.  **CSS Sprites**
    
2.  **Bin Packing**
    
3.  **EBAFIT**
    

### Considerations:

-   Signs can be rotated by **90°** to optimize space utilization.
    

## Task 3: What Algorithm Did We Use?

### Selected Algorithm: **EBAFIT (3D Bin Packing Algorithm)**

**Reason for Selection:**

-   The **3D Container Packing** library is available in C#.
    
-   Other libraries are available in Python, but using them would require cross-language integration, which we wanted to avoid.
    

### Input Parameters:

-   **Bed dimensions**
    
-   **Dimensions for each sign**
    
-   **Quantity of each sign**
    

### Output:

-   The algorithm places signs optimally on the bed.
    
-   For each placed sign, it provides:
    
    -   **(x, y, z) coordinates**
        
    -   **Length along the x-axis**
        
    -   **Length along the y-axis**
        
    -   **Length along the z-axis**
        

### Handling Unplaced Signs:

-   There is a possibility that not all signs can be placed on a bed.
    
-   In such cases, the algorithm returns the unplaced signs, and the process is repeated for another bed.
    

### Automated Bed Generation Threshold:

-   A **bed area utilization threshold** of **80%** was set for automated bed generation via cron jobs.
    
-   A bed is only generated if space utilization is **greater than 80%**.
    

## Assignment:

-   Identify the argument to pass such that the **x and y coordinates** are returned in the 3D packing algorithm while ignoring the **z-axis**.
    
-   Use the following repository to set up and configure the problem:
    
    -   [3D Container Packing Repository](https://github.com/davidmchapman/3DContainerPacking/tree/master)
        
-   The repository provides visualization tools to help analyze the packing solution.
