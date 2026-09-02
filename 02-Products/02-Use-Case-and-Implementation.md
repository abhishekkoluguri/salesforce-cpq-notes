# Products — Use Case & Implementation (TechNova)

## Business Requirement
(Maps to Requirement #1 in `03-Project-Requirements.md`)
Sales reps need a clean, structured catalog of TechNova's Hardware,
Software, and Service products before any quoting, bundling, or
pricing logic can be built.

## Why the Project Needs This
Without Product2 records in the org, there is nothing for a Quote
Line, Bundle, Rule, or Discount Schedule to attach to. This is the
literal first hands-on step of the entire project.

## Expected Behavior
Each product should be creatable, active, and priced in the Standard
Price Book, ready to be added to a Quote.

## Configuration Approach
Create Product2 records one at a time, each immediately followed by
a Standard Price Book entry — never leave a product without a price.

## Objects Involved
- `Product2`
- `PricebookEntry`
- `Pricebook2` (Standard Price Book)

## Record Created So Far

| Field | Value |
|---|---|
| Product Name | Business Laptop |
| Product Code | TN-HW-LAPTOP-001 |
| Product Family | Hardware |
| Active | Yes |
| Description | Business-grade laptop with configurable RAM, storage, warranty, and support options. |
| Standard Price Book Entry | $1200.00, Active |

## Testing Steps
1. App Launcher → Products → confirmed Business Laptop listed, Active.
2. Opened record → confirmed Standard Price Book entry shows $1200.00, Active.

## Expected Result
Business Laptop exists as an active, priced product, ready to be
converted into a bundle in the next step.

## Actual Result
✅ Matches expected result. Product created and priced successfully.

## Issues Encountered
None.

## Troubleshooting
N/A for this record.

## Lessons Learned
Creating the Product2 record alone is not enough — the Price Book
Entry step is what actually makes a product usable on a Quote. Good
habit: never save a product without immediately pricing it.

## Screenshots
- Business Laptop product detail page — captured
- Standard Price Book entry ($1200.00, Active) — captured

## Full Product Catalog Created

| Product Name | Product Code | Family | List Price | Active |
|---|---|---|---|---|
| Business Laptop | TN-HW-LAPTOP-001 | Hardware | $1200.00 | ✅ |
| Monitor | TN-HW-MONITOR-001 | Hardware | $250.00 | ✅ |
| Server | TN-HW-SERVER-001 | Hardware | $4500.00 | ✅ |
| Cloud Productivity Suite | TN-SW-CLOUDPROD-001 | Software | $15.00 | ✅ |
| Security Software | TN-SW-SECURITY-001 | Software | $10.00 | ✅ |
| Analytics Platform | TN-SW-ANALYTICS-001 | Software | $50.00 | ✅ |
| Implementation Service | TN-SVC-IMPL-001 | Services | $2000.00 | ✅ |
| Premium Support | TN-SVC-PREMSUPPORT-001 | Services | $200.00 | ✅ |
| Training Service | TN-SVC-TRAINING-001 | Services | $1000.00 | ✅ |

All 9 products created with matching Standard Price Book entries,
Active.

## Testing Steps (Full Catalog)
1. App Launcher → Products → confirmed all 9 products listed, Active.
2. Opened each → confirmed Standard Price Book entry present, Active,
   matching the prices above.

## Expected Result
Complete 9-product catalog for TechNova, all active and priced,
ready for bundling.

## Actual Result
✅ Matches expected result. All 9 products created and priced
successfully with no deviations from planned values.

## Remaining Work For This Topic
None — Products topic hands-on work is complete. Next topic:
Product Bundles.
