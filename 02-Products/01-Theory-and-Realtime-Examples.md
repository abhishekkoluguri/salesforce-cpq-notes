# Products — Theory & Real-Time Examples

## Definition
In Salesforce CPQ, a **Product** (standard object `Product2`) is the
base unit of anything a company sells — hardware, software, or a
service. CPQ doesn't replace this object; it extends standard
Salesforce Products with additional fields (bundle configuration,
subscription behavior, pricing method) via its managed package.

## Purpose
Every Quote Line Item traces back to a Product. Without a clean
Product catalog, nothing else in CPQ — bundles, rules, pricing,
discounting — has anything to attach to.

## Why It Is Needed
A company can't quote what isn't defined as a sellable item with a
price. Products are the foundation layer; every other CPQ concept
(bundles, rules, pricing) is built on top of Product2 records.

## How It Works
1. A Product2 record is created (Name, Code, Family, Active status).
2. It's added to one or more **Price Books** with a **List Price** —
   this is what makes it appear as priceable on a Quote.
3. Only **Active** products in an **Active** price book entry can be
   added to a Quote Line.
4. From here, CPQ-specific fields (Configuration Type, etc.) turn a
   simple product into a bundle, option, or subscription product —
   covered in later topics.

## Important Terminology
| Term | Meaning |
|---|---|
| Product2 | The standard Salesforce object representing a sellable item |
| Product Code | A unique internal code used for reporting/integration |
| Product Family | A category grouping (Hardware, Software, Services) |
| Price Book | A list of products with defined prices |
| Price Book Entry | The specific price of a product within a given price book |
| Standard Price Book | The default price book every Salesforce org has |

## Real-World Example
A hardware retailer might have "Laptop Model X" as a Product2 record,
listed in a "US Retail Price Book" at one price and a "Enterprise
Price Book" at a discounted price — same product, different pricing
context.

## Business Scenario (TechNova)
TechNova needs Business Laptop, Monitor, Server (Hardware), Cloud
Productivity Suite, Security Software, Analytics Platform (Software),
and Implementation Service, Premium Support, Training Service
(Services) all defined as Products before any of them can be quoted,
bundled, or discounted.

## Related CPQ Concepts
- Product Bundles / Options / Features (next topic)
- Price Books & Pricing Methods
- Discount Schedules (apply to specific products)

## Important Fields/Settings
- `Name`, `ProductCode`, `Family`, `IsActive` — standard fields
- Price Book Entry `UnitPrice`, `IsActive` — controls whether the
  product is priceable and visible on a Quote

## Best Practices
- Always set a Product Code, even in a learning org — it mirrors
  real implementations and matters for reporting later
- Add every product to the Standard Price Book immediately after
  creation — an "orphan" product with no price book entry is a very
  common early mistake

## Common Mistakes
- Creating a product but forgetting to add it to a price book (it
  will exist but never appear as addable on a Quote)
- Leaving a product Inactive by accident
- Inconsistent naming/coding across products, which breaks reporting
  in larger orgs

## Key Takeaways
- Product2 + Price Book Entry together make a product usable on a Quote
- Everything else in CPQ (bundles, rules, pricing, discounts) is layered
  on top of this foundation
