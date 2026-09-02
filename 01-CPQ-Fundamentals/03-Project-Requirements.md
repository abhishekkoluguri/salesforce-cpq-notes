# Project Requirements — TechNova Solutions CPQ Implementation

This document maps each business requirement (from
`02-Project-Use-Case.md`) to the specific CPQ feature that solves it,
the Salesforce configuration needed, and the test case that proves it
works. Rows are added progressively as we reach each topic — this is
not the full and final list.

Status legend: 🟡 Planned (not started) · 🔵 In Progress · ✅ Verified

| # | Business Requirement | CPQ Feature | Salesforce Configuration | Test Case | Status |
|---|---|---|---|---|---|
| 1 | Sales reps need a clean, structured catalog of TechNova's Hardware, Software, and Service products | **Products** (core Product2 records) | Create Product2 records for Business Laptop, Monitor, Server, Cloud Productivity Suite, Security Software, Analytics Platform, Implementation Service, Premium Support, Training Service. Add each to the Standard Price Book with a List Price. | Rep can search each product and see it available with a price on a new Quote. | 🟡 |
| 2 | A Business Laptop has configurable RAM, Storage, Warranty, and Support options that must be selected together as one sellable unit | **Product Bundles + Product Options + Features** | Mark Business Laptop as a bundle (`Configuration Type = Allowed/Required`). Create Feature groups: RAM, Storage, Warranty, Support. Add each option (8GB/16GB, 512GB/1TB, 1yr/3yr, Standard/Premium) as a Product Option. | Rep adds Business Laptop to a Quote, configuration screen opens, rep selects one option per feature, bundle saves correctly with child line items. | 🟡 |
| 3 | If a customer selects 3-Year Warranty, Premium Support should become available (but not forced) | **Product Rule — Selection Rule** | Create a Product Rule of type "Selection" scoped to the Business Laptop bundle, triggered when 3-Year Warranty is selected, targeting the Premium Support option. | Select 3-Year Warranty → Premium Support option becomes selectable/auto-selected per rule type chosen. Select 1-Year Warranty → rule does not fire. | 🟡 |
| 4 | A 3-year warranty cannot be combined with a product that doesn't support extended coverage | **Product Rule — Validation Rule** | Create a Product Rule of type "Validation" with an error condition tied to incompatible option combinations; define the error message shown to the rep. | Attempt the invalid combination → Quote configuration blocks save and shows the defined error message. | 🟡 |
| 5 | Pricing must be calculated automatically and consistently across all reps, for both one-time and recurring (subscription) products | **Pricing Methods + Price Books** | Confirm Standard Price Book (done). Set pricing method per product (List, Cost markup, or Contracted, as applicable). Define subscription pricing fields (subscription term, pricing per unit/term) on subscription-enabled products (Premium Support, Cloud Productivity Suite, Security Software). | Add products to a Quote → Net Price and subscription pricing calculate automatically without manual entry. | 🟡 |
| 6 | Orders of more than 20 laptops should automatically receive a volume discount | **Discount Schedules** | Create a Discount Schedule with tiers (e.g. 21–49 units = X%, 50+ units = Y%). Attach the schedule to the Business Laptop product. | Add 50 laptops to a Quote → discount tier applies automatically to the line item without manual override. | 🟡 |
| 7 | Discounts applied above a defined threshold must require manager approval before the quote can be finalized | **Approvals** (deferred — documented for reference now, implemented later) | Not yet configured — will define approval condition (e.g. discount % > threshold) and approval process once Discounting is complete and tested. | Not yet defined. | 🟡 |
| 8 | The final quote sent to the customer must look professional and include all selected products, pricing, and terms | **Quote Templates** (deferred) | Not yet configured — comes after Quote Configuration basics are working. | Not yet defined. | 🟡 |
| 9 | A signed quote for a 3-year contract must generate a trackable Contract with Subscriptions that can later be renewed | **Contracts & Renewals** (deferred) | Not yet configured — last major topic in the learning path. | Not yet defined. | 🟡 |

## Notes
- Rows 1–6 are our **immediate next hands-on work**, in this exact order,
  since each depends on the one before it (can't configure bundles
  before products exist; can't test discount tiers before pricing works).
- Rows 7–9 are intentionally left underspecified for now — filling them
  in prematurely would mean guessing at configuration we haven't learned
  or tested yet, which breaks the "don't invent details" rule for this
  project.
- This table will be updated in place (not replaced) as each row moves
  from 🟡 → 🔵 → ✅, with real Actual Result / Issue notes added in the
  corresponding topic's `02-Use-Case-and-Implementation.md` file.
