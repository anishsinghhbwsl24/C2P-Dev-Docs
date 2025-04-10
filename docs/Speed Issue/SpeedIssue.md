# Speed Issue on Updating PDF Status

## UpdatePDFStatusOnFolder Module

**UpdatePDFStatusOnFolder** is a module responsible for updating the `PDFStatus` and `PDFFilePath` of files when they are manually moved from one folder to another. These movements may be performed by designers, such as:

-   Moving files from the **Shipby date folder** to the **Fixed folder**, updating the `PDFStatus` from `PDFCreated` to `ToPrint`.
    
-   Manually renaming **size folders** by concatenating designer initials in the folder name to indicate which designer is working on a specific set of files.
    
-   Moving files to **Problems folder** or **Printed folder**, which also necessitates updating the relevant statuses.
    

To update these values efficiently, the module originally scanned the entire **Exported PDF** directory, where files are generated. For each order, the file was checked against its existing filepath. If the file was missing, the system searched the directory recursively based on the filename to locate its new filepath and update the database. If the file had been moved to special folders like **Fixed, Problems, or Printed**, the relevant status was updated accordingly.

### Performance Bottlenecks and Optimization

The recursive search for each order file within the large **Exported PDF** directory was extremely slow, causing the **UpdatePDFStatus cron job** to run for extended periods continuously.

To address this, a **cache mechanism** was introduced to simplify operations. A dictionary cache was implemented using `FileName` as the key and `FilePath` as the value:

```
allFiles[file.Name] = file.FullName;
```

Now, instead of recursively iterating through the massive directory, the operation simply performs a lookup in the cache, significantly improving performance.
