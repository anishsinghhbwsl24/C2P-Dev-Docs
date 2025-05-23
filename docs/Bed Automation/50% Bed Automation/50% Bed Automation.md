
# 50% Bed Automation

## Business Requirement

SigoSigns aims to minimize manual intervention in the bed creation process to improve efficiency and reduce the time spent by operators. The goal is to automate the selection of orders for bed generation, reducing manual effort and speeding up the bed creation process. 

### Current Bed Creation Methods

Currently, beds are created through two primary methods:

* **Manual Creation:** Users manually create beds via the C&P bed layout tab.
* **Automated Bed Creation (Cron):** A scheduled cron job automatically creates beds based on predefined rules.

To understand the scope of automation, an analysis was conducted to assess the manual effort involved in creating different bed types.

The relevant analysis report can be found here: [https://docs.google.com/spreadsheets/d/1LnzPuIFyl83TxOiSYi2GiPRzIILkR-Xj61RV3E8C9Yc/edit?usp=sharing](https://docs.google.com/spreadsheets/d/1LnzPuIFyl83TxOiSYi2GiPRzIILkR-Xj61RV3E8C9Yc/edit?usp=sharing)

The **Report** sheet provides a row-wise breakdown of bed types and a column-wise breakdown of users who created those beds. It includes the count of beds generated by each user and the average percentage of bed area covered by signs.

The **Full Report** sheet offers detailed data specific to each bed size.

The analysis considered **6,538 beds** created after the implementation of "Automated Bed Creation 2".

## Key Insights from Analysis

* **Autogenerated Beds:**
    * Overall, **8% (505 out of 6,538)** of all beds are currently autogenerated.
    * For bed sizes included in autogeneration rules, **17% (338 out of 1,975)** are autogenerated.
* **Most Common Bed Types:**
    * **Regular (53%)** and **MixedSizes (36%)** constitute the majority of created beds.
    * **Labels** and **Decals** together account for less than 10% of beds.

## Automated Bed Creation Logic

The automated bed creation process relies on a set of rules defined in the `BedAutomationRules` table. This table contains combinations of:

* `SignSize`
* `Background`
* `Custom`

Orders matching these specific combinations are eligible for automated bed creation.

**Old Process:**

The previous automation process iterated through each rule in the `BedAutomationRules` table. For each rule, it would:

1.  Fetch orders matching the specified `SignSize`, `Background`, and `Custom` values.
2.  Generate a bed based on these fetched orders.

**Crucially, beds were generated independently for each rule.**

**New Process (Modification):**

The updated process first processes **all** the rules in the `BedAutomationRules` table. It then retrieves all orders that match **any** of the defined rules.

The subsequent grouping of these selected orders for bed creation follows a specific sequence:

1.  **Grouping based on Custom:** All selected order items are first divided into **stock** and **custom** items. A single bed can only contain items of the same type (either all stock or all custom).
2.  **Grouping based on GroupSize:** Items within the stock or custom categories are then grouped based on their `GroupSize`. Items with the same `GroupSize` are considered for inclusion in the same bed.
3.  **Grouping based on SignSize:** If no `GroupSize` is specified, the remaining items are grouped based on their `SignSize`.
4.  **Grouping based on Background:**
    * If a rule has no specific `Background` defined, all background colors within the current group are combined into a single set.
    * If specific backgrounds (e.g., Red and Black) are defined in the rules, the groups will be further divided based on matching backgrounds. Only items with the specified background (or all backgrounds if none is specified in the rule) will be considered for bed creation together.

**Important Note:** Automation rules only control the **selection and triggering** of bed creation. They do not dictate the final arrangement of signs on a bed. The existing bed creation process determines how the selected items are ultimately laid out on the bed. The automation essentially emulates manually selecting order items for bed creation based on the defined rules.

## Handling Orders After 3 PM

To optimize for next-day shipping, the system considers the next day's orders when fetching orders after 3 PM.

**Initial Implementation:**

Initially, only orders with the exact next day's date were considered.

**Current Implementation (Improved):**

Due to weekends and holidays where the immediate next day might not be a shipping day, the `shipby` date restriction has been modified. The system now considers orders with the **next earliest shipby date** when fetching orders after 3 PM. This ensures that orders are prepared for the soonest possible shipping date.
