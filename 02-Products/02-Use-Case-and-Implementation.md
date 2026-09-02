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

## Remaining Products To Create (this topic continues)
- [ ] Monitor (Hardware)
- [ ] Server (Hardware)
- [ ] Cloud Productivity Suite (Software)
- [ ] Security Software (Software)
- [ ] Analytics Platform (Software)
- [ ] Implementation Service (Services)
- [ ] Premium Support (Services)
- [ ] Training Service (Services)
