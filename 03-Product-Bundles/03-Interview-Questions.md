# Product Bundles — Interview Questions

## Basic
**Q: What makes a product a "bundle" in Salesforce CPQ?**
A: Setting its Configuration Type field to "Allowed" or "Required."
This unlocks Product Features and Product Options related lists on
that product.

**Q: What's the difference between "Allowed" and "Required" Configuration Type?**
A: "Allowed" makes the configuration screen optional to open when
adding the bundle to a Quote. "Required" forces it every time.

**Q: What is a Product Feature?**
A: An organizational grouping/label inside a bundle (e.g. "RAM") —
it has no price and is not itself a product; it just groups related
Options together for display.

## Intermediate
**Q: How do you enforce that a customer must pick exactly one option
within a feature?**
A: Set Min Option Count = 1 and Max Option Count = 1 on that Feature.
Min alone prevents zero selections; Max alone prevents multiple
selections; both together enforce exactly one.

**Q: How is bundle pricing typically calculated?**
A: Additively by default — the parent product's price plus the price
of each selected option, summed into the Quote's Net Total. (Bundles
can also be configured with a single rolled-up bundle price, which is
a variation covered separately.)

**Q: Can the same product be reused as an Option across multiple bundles?**
A: Yes — for example, we reused an existing standalone "Premium
Support" product as an Option inside the Business Laptop bundle
rather than duplicating it, which mirrors real-world reuse of shared
products.

## Advanced / Scenario-Based
**Q: A customer reports that a bundle configuration screen allows
zero options to be selected in a feature that should be mandatory.
How would you troubleshoot it?**
A: Check the Feature's Min Option Count — if it's 0 or blank, that's
the likely gap; setting Min Option Count = 1 fixes a "can be left
empty" bug.

**Q: You need a feature where a customer can select up to 3 options
out of 5 available add-ons. How would you configure that?**
A: Set Min Option Count = 0 (or 1, depending on whether at least one
is mandatory) and Max Option Count = 3 on that Feature — the same
mechanism used for exactly-one selection, just with different values.

## Troubleshooting-Based
**Q: You add a product to a bundle as an Option, but it doesn't show
up on the configuration screen at all. What are common causes?**
A: The Option product itself might be Inactive, or missing an active
Price Book Entry in the Quote's Price Book — both product AND pricing
must be valid, same requirement as any standalone product.

## Real-World Implementation
**Q: Why is it good practice to build and test one Feature in
isolation before adding several at once?**
A: It isolates problems — in our own implementation, testing RAM
alone first let us catch and fix a Price Book naming collision issue
cleanly, without also having Storage/Warranty/Support configuration
errors mixed into the same debugging session.
