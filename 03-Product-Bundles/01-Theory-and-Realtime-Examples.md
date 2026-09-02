# Product Bundles — Theory & Real-Time Examples

## Definition
A **Product Bundle** in Salesforce CPQ is a parent product that
contains other products (called **Product Options**) nested beneath
it. When a rep adds the bundle to a Quote, they configure it by
choosing which options apply — the bundle and its selected options
then appear together as a structured set of Quote Line Items.

## Purpose
Real products are rarely sold as a single flat item. A laptop isn't
just "a laptop" — it has RAM, storage, warranty, and support choices.
Bundles let CPQ represent that complexity as one manageable unit
instead of forcing reps to manually add 4-5 separate unrelated line
items and remember which combinations are valid.

## Why It Is Needed
Without bundles: a rep quoting a laptop would need to know, from
memory, which RAM/storage/warranty/support products exist, add each
one manually as a separate line, and hope they picked a valid
combination. Error-prone and slow — exactly the problem CPQ exists
to solve.

## How It Works (Conceptually)
1. A Product2 record is marked with **Configuration Type =
   "Allowed"** or **"Required"** — this is what turns a normal
   product into a bundle. ("Required" forces configuration every
   time it's added; "Allowed" makes it optional to configure.)
2. Inside the bundle, you create **Product Features** — these are
   just labeled groupings, like "RAM" or "Storage." A Feature is not
   a product itself; it's an organizational container.
3. Inside each Feature, you add **Product Options** — these ARE
   real Product2 records (e.g. "8GB RAM", "16GB RAM") linked to the
   bundle as children.
4. Each Option has settings controlling behavior:
   - **Selected by Default** — pre-checked when the bundle opens
   - **Required** — must be chosen, can't leave the feature empty
   - **Min/Max Option Count** — how many options can be picked
     within that feature (e.g. exactly 1 of 2 RAM choices)
   - **Quantity Editable** — whether the rep can change quantity of
     that specific option
5. When a rep adds the bundle to a Quote, a configuration screen
   opens showing all Features and their Options, letting them build
   a valid product from the allowed choices.
6. On save, the bundle line and its selected option lines appear as
   related Quote Line Items, with the bundle acting as the parent.

## Important Terminology
| Term | Meaning |
|---|---|
| Bundle | A parent Product2 with Configuration Type = Allowed/Required |
| Product Feature | A labeled grouping inside a bundle (not a real product) |
| Product Option | A child Product2 linked to a bundle, nested under a Feature |
| Configuration Type | The field that makes a product act as a bundle |
| Min/Max Option | Controls how many options can be selected per Feature |
| Selected by Default | Pre-checks an option when configuration opens |

## Real-World Example
A car manufacturer's CPQ system might bundle "Sedan Model X" with
Features like "Engine," "Color," "Interior Package" — each Feature
has 2-4 Options, and the buyer must pick exactly one per Feature
before the configuration is considered complete/valid.

## Business Scenario (TechNova)
Business Laptop needs to become a bundle with 4 Features:
- **RAM** — 8GB / 16GB (pick exactly 1)
- **Storage** — 512GB SSD / 1TB SSD (pick exactly 1)
- **Warranty** — 1 Year / 3 Years (pick exactly 1)
- **Support** — Standard Support / Premium Support (pick exactly 1,
  though we'll later add a rule so 3-Year Warranty makes Premium
  Support available/preferred — that's a Product Rule, next topic
  after this one)

Each option (8GB RAM, 16GB RAM, etc.) has to exist as its own small
Product2 record first — bundles don't contain "settings," they
contain real linked products.

## Related CPQ Concepts
- Product Rules (Selection/Validation) — control cross-feature logic,
  covered right after Bundles
- Pricing — bundle options can be priced individually or bundled into
  one price (we'll use individual pricing to keep it transparent)
- Quote Line Items — bundles produce a parent-child line structure

## Important Fields/Settings
- `Product2.SBQQ__ConfigurationType__c` = Allowed/Required (makes it a bundle)
- `SBQQ__ProductFeature__c` — the Feature object
- `SBQQ__ProductOption__c` — links an Option product to a bundle + Feature
- Fields on Product Option: `SBQQ__Required__c`, `SBQQ__SelectedByDefault__c`,
  `SBQQ__MinOptionCount__c`, `SBQQ__MaxOptionCount__c`

## Best Practices
- Create every Option as its own small Product2 record FIRST — you
  can't reference an option that doesn't exist yet
- Keep Feature names short and business-friendly (reps will see these
  labels on the configuration screen)
- Use Min=Max=1 on features where exactly one choice is required —
  this is the most common real-world pattern

## Common Mistakes
- Forgetting to create the small option products before trying to
  add them to a Feature
- Not setting Min/Max Option Count, leaving a Feature where a rep
  could select zero or multiple conflicting options by accident
- Confusing "Feature" (a label/grouping) with "Option" (an actual
  product) — Features are not products and have no price

## Key Takeaways
- Bundle = parent product + Configuration Type set
- Feature = organizational grouping, no price, no product record
- Option = real product, nested under a Feature, has its own price
- Min/Max Option Count is what actually enforces valid selections —
  without it, the bundle exists but doesn't constrain the rep
