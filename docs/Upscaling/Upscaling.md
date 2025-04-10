
**Upscaling Customer Images**


### **Business Requirement*

Customers can upload their own images to create a sign. However, these uploaded images may be of poor quality or low resolution, which can lead to poor print quality. Additionally, the image might need to be printed in a much larger size than its intrinsic dimensions or at a specific DPI (dots per inch), necessitating a higher-quality image.

To ensure that printed images maintain high quality, an upscaling mechanism is required to enhance the resolution of the uploaded customer images. This will ensure sharp, clear prints, especially for signs that will be viewed from a distance. Images that are pixelated or blurry due to being stretched beyond their original resolution could negatively affect the brand's image and customer satisfaction.

### **Criteria for image upscaling**

-   If dimensions of the uploaded image meets or exceeds the required print dimensions, then upscaling is not required. For example, if a 100 * 100 customer image is used at 100 * 100 (or 90 * 90) dimensions, then upscaling is not required.
-   If the dimensions of the print image are greater than the dimensions of the uploaded customer image, then upscaling is required. For example, a 100 * 100 image is used at 200 * 200 or greater dimensions, then upscaling is required.

Basically, upscaling is required if ``Dimension of Print > Dimension of Image``

This ensures that all printed images maintain sharpness and clarity, preventing pixelation when enlarged.

**Key Consideration:** When upscaling an image, the aspect ratio (length/width) must be maintained to prevent distortion.

### **How to Upscale?**

To automate the image upscaling process, we utilize Claid.AI’s image upscaling service.

#### ***Claid.AI for Image Upscaling***

Claid.AI provides machine-learning-based image enhancement, ensuring that upscaled images retain quality. The method currently in use is called **Smart Enhance**, which effectively increases resolution without significant loss of detail.

#### **Workflow of Claid.AI Integration**

1.  **API Request:**
    -   The customer-uploaded image is sent to Claid.AI’s servers via an API request.
    -   The request includes the dimensions of the print image, the image itself as well as 72 dpi.
2.  **Processing:**
    -   Claid.AI applies ML-based image enhancement techniques to upscale the image while preserving quality.
3.  **API Response:**
    -   Claid.AI returns a URL pointing to the upscaled image, which is then used for printing.

### **Conclusion**

By integrating Claid.AI’s upscaling capabilities, we ensure that all printed images maintain sharpness and clarity, meeting both business requirements and customer expectations. This process optimizes image quality for large-format printing, preventing pixelation and distortion in the final product.
