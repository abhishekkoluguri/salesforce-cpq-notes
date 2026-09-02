# Products — Interview Questions

## Basic
**Q: What is a Product2 in Salesforce?**
A: The standard Salesforce object representing anything a company
sells. CPQ extends it with additional fields for bundling, pricing
method, and subscription behavior, but doesn't replace it.

**Q: What's the difference between a Product and a Price Book Entry?**
A: A Product defines *what* is sold (name, code, family). A Price
Book Entry defines *how much* it costs within a specific Price Book.
A product with no active Price Book Entry cannot be added to a Quote.

## Intermediate
**Q: Why might a product not appear when trying to add it to a Quote,
even though the Product2 record is Active?**
A: Most likely it has no active Price Book Entry in the Price Book
being used by that Quote — the product and its pricing are separate
records, both must be active.

**Q: What is Product Family used for?**
A: Grouping products for reporting and organization (e.g. Hardware,
Software, Services) — it doesn't affect pricing or configuration
logic by itself, but it's used heavily in reports and sometimes in
rule conditions.

## Advanced / Scenario-Based
**Q: A customer-specific Price Book shows a different price than the
Standard Price Book for the same product. How does CPQ decide which
price to use on a Quote?**
A: The Quote itself is tied to a specific Price Book (usually inherited
from the Opportunity). Whatever Price Book Entry matches that Quote's
Price Book is what's used — not the Standard Price Book by default,
unless that's the one assigned.

**Q: You're setting up a new product catalog for a client with 200
products across 5 price books. What's your approach to avoid pricing
inconsistencies?**
A: Establish a clear product coding convention up front (as we did
with TN-HW/SW/SVC prefixes), create products first in the Standard
Price Book, then systematically add entries to each additional price
book, ideally using Data Loader for bulk consistency rather than
manual entry at that scale.

## Configuration-Based
**Q: Walk through the steps to make a new product sellable on a Quote.**
A: Create the Product2 record with Name, Code, Family, set Active.
Add a Price Book Entry (Standard Price Book at minimum) with a List
Price, set Active. Confirm both are active before expecting it to
appear on a Quote.

## Real-World Implementation
**Q: Why is it a common mistake for new CPQ admins to create products
without pricing them immediately?**
A: Because the UI lets you save a Product2 record successfully with
no Price Book Entry at all — there's no built-in warning. It looks
"done" but silently won't work when a rep tries to quote it, which
usually gets discovered later during testing rather than at creation
time.
