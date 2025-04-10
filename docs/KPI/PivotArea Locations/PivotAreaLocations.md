## Definitions: PivotGrid Area Locations

https://docs.devexpress.com/WindowsForms/images/xtrapivotgrid_area_locations4659.png


* **Row Headers:**
    * **Bed type:** Categorization of beds (e.g., Regular, Mixed Sizes, Labels, Decals).
    * **Bed Size:** Determined by `groupsize` if the bed was created based on it; otherwise, it reflects the `Signsize`.
    * **Bed name:** The unique identifier for a specific bed.
    * **Status:** The sequence of stages a bed progresses through.
        * **Jig beds:** Ready -> Printing -> Printed -> Routing -> Routed
        * **Non-jig beds:** Ready -> Printing -> Printed -> Cutting -> Cutting Done -> Routing -> Routed
        * **Engraving beds:** Ready -> Engraving -> Engraving Done -> Routing -> Routed
    * **User:** The individual responsible for a specific action on a bed at a particular status.

* **Data Headers:**
    * **Bed count:** The number of beds created (PDFs generated). This metric is associated with the `Ready` status. If data is not yet bifurcated at the status level, it represents the bed count for the chosen group.
    * **Printed count:** The number of beds that have been printed. Linked to the `Printed` and `Engraving Done` statuses.
    * **Cut count:** The number of beds that have been cut. Linked to the `Cutting Done` status. For beds not requiring cutting, this value is 0.
    * **Sign count:** The total number of individual signs on a bed. Linked to the `Printed` status.
    * **SQ inches:** The total surface area of all signs on a bed in square inches. Linked to the `Ready` status.
    * **Shipped count:** The number of unique orders (not individual items or signs) associated with the shipped beds displayed. Linked to the `Routed` status.

* **Metrics:**
    * **Signs:** A measure of the total number of signs.
    * **Beds:** A measure of the total number of beds.
    * **Square inches:** A measure of the total area of signs.
    * **Idle time:** For a specific user, the total time difference between when they finished printing one bed (`Printed` status) and started printing the next (`Printing` status). Calculated as the sum of `(Printing[i+1] - Printed[i])` when sorted by time for a user's `Printing` and `Printed` events. Other statuses are not considered.
    * **Print time:** The total duration a user spent printing. Calculated as the sum of `(Printed[i] - Printing[i])` for all a user's printing events.
    * **Cut time:** The total duration a user spent cutting. Calculated as the sum of `(CuttingDone[i] - Cutting[i])` for all a user's cutting events.
    * **Shipped:** The count of distinct orders that were part of the beds currently displayed in the PivotGrid UI and have been shipped.

## Important Considerations

* **User-Level Metrics (Idle Time, Print Time, Cut Time):** These metrics are calculated at the user level. The dashboard displays the aggregated values for all users currently visible in the PivotGrid UI. To view the metrics for a specific user, apply a user filter. The underlying `Printing` and `Printed` events used for calculation are based on the selected users, not necessarily the beds displayed.
* **Shipped Count Discrepancy:** The `Shipped count` displayed in the PivotGrid UI (as a data header) might be higher than the `Shipped` metric. This can occur because a single order can be present on multiple beds. The UI will count each instance of the shipped order on different beds, leading to overcounting when aggregated. The `Shipped` metric resolves this by counting only the distinct orders associated with the displayed shipped beds.