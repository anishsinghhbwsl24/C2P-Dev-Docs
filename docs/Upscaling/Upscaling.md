## **Analysis of Image Upscaling Requirement**

To determine whether an image needs upscaling, an initial analysis was conducted. The key factor in deciding this was:

-   **If the dimensions of the printed image are greater than the dimensions of the uploaded customer image, then the image requires upscaling.**
    
-   **If the uploaded image meets or exceeds the required print dimensions, then upscaling is not necessary.**
    

This ensures that all printed images maintain sharpness and clarity, preventing pixelation when enlarged.


## **Claid AI for Image Upscaling**

To automate the upscaling process, **Claid AI** is used. Claid AI offers machine learning-based upscaling algorithms, with **Smart Enhance** being the chosen method.

### **How Claid AI Works**

1.  **API Request**:
    
    -   The uploaded customer image is sent to **Claid AI’s servers** via an API request.
        
    -   The request includes the **required final dimensions** for the sign PDF.
        
2.  **Processing**:
    
    -   Claid AI applies **ML-based image enhancement** to upscale the image while preserving quality.
        
3.  **API Response**:
    
    -   The response contains a **URL to the upscaled image**, which can then be used for printing.
        

This integration ensures that all images are **optimized for print quality**, meeting business and customer expectations.

