
# Speed Issue on Updating PDF Status

## Business Requirement

SigoSigns requires an efficient mechanism to update the status of PDF files within the system when they are moved across various folders. The key goal is to minimize delays in updating the `PDFStatus` and `PDFFilePath` while ensuring that the correct status is reflected across different file movement scenarios. Slow performance in the update process can lead to operational inefficiencies, delays in processing orders, and the potential for inconsistencies in the status of PDF files. A fast and reliable update mechanism is critical to ensuring that designers and operators can move files without disrupting workflow and that the database accurately reflects the file status at all times.

## UpdatePDFStatusOnFolder Module

**UpdatePDFStatusOnFolder** is a module responsible for updating the `PDFStatus` and `PDFFilePath` of files when they are manually moved from one folder to another. These movements may be performed by designers, such as:

-   Moving files from the **Shipby date folder** to the **Fixed folder**, updating the `PDFStatus` from `PDFCreated` to `ToPrint`.
-   Moving files to **Problems folder** or **Printed folder**, which also necessitates updating the relevant statuses.
-   Manually renaming **size folders** by the designer by concatenating their name's initials in the folder name to indicate who is working on a specific set of files.

To update these values efficiently, the module originally scanned the entire **Exported PDF** directory, where files are generated. 
**For each order**, the file was checked against its existing filepath. If the file was missing, the system searched the directory recursively based on the filename to locate its new filepath and update the database. If the file had been moved to special folders like **Fixed, Problems, or Printed**, the relevant status was updated accordingly.

### Performance Bottlenecks and Optimization

The recursive search for each order file within the large **Exported PDF** directory was extremely slow, causing the **UpdatePDFStatus cron job** to run for extended periods continuously.

To address this, a **cache mechanism** was introduced to simplify operations. A dictionary cache was implemented using `FileName` as the key and `FilePath` as the value:

``allFiles[file.Name] = file.FullName``

Now, instead of recursively iterating through the massive directory, the operation simply performs a lookup in the cache, significantly improving performance.
