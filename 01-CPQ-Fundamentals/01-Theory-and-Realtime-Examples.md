# CPQ Fundamentals — Theory & Real-Time Examples

## Definition
CPQ stands for **Configure, Price, Quote**. Salesforce CPQ is a native
Salesforce application (managed package) that helps sales teams:
- **Configure** — select the right products and valid combinations
- **Price** — calculate accurate pricing automatically
- **Quote** — generate a professional, accurate sales quote

## Purpose
To remove manual, error-prone quoting from the sales process and replace
it with a guided, rule-driven system built on Salesforce data.

## Why It Is Needed
As product catalogs grow (hardware + software + services, bundles,
options, subscription terms, discount tiers), manual quoting breaks down.
CPQ exists to handle that complexity consistently, at scale, for every
sales rep, every time.

## What Problem It Solves
Without CPQ, a company like TechNova has:
- Reps guessing which products are compatible
- Inconsistent pricing between reps
- Manual discount calculations with no guardrails
- Slow quote turnaround
- No enforced approval process for large discounts
- Disconnected contract/renewal tracking

With CPQ:
- Product compatibility is enforced by rules, not memory
- Pricing is calculated by the system using price books, price rules,
  and discount schedules
- Discounts above a threshold automatically trigger approval
- Quotes generate quickly and consistently
- Quotes flow into Orders → Contracts → Subscriptions → Renewals

## How It Works (Conceptually)
1. A Quote is created, linked to an Opportunity and Account.
2. The rep adds Quote Line Items (products) to the Quote.
3. CPQ's rules engine checks configuration validity (bundles, options,
   dependencies).
4. Pricing waterfall runs: List Price → adjustments → discounts → Net Price.
5. If discounting exceeds defined thresholds, an approval process triggers.
6. Once approved, the Quote is finalized, synced to the Opportunity, and
   can generate an Order.
7. The Order can generate a Contract, which can generate Subscriptions
   for recurring/renewable products.

## Important Terminology
| Term | Meaning |
|---|---|
| Quote | The CPQ record representing a proposed sale |
| Quote Line Item | A single product line on a Quote |
| Product Bundle | A parent product grouping optional/required child products |
| Product Option | A child product inside a bundle |
| Product Rule | Logic that controls what can/must/cannot be selected together |
| Price Rule | Logic that adjusts pricing based on conditions |
| Discount Schedule | Predefined volume/tiered discount tables |
| Subscription | A recurring product tied to a Contract, used for renewals |

## Real-World Example
A telecom company selling internet + TV + phone bundles uses CPQ so that
a customer can't accidentally be quoted "TV package" without a required
"set-top box" product — the bundle rules prevent that automatically.

## Business Scenario (TechNova)
TechNova's rep is quoting 50 laptops with Premium Support. Without CPQ,
the rep might forget that Premium Support requires a minimum 1-year
warranty, or apply the wrong volume discount tier. CPQ's rules and
discount schedules prevent both mistakes.

## Related CPQ Concepts
- Price Books (standard Salesforce, extended by CPQ)
- Product Bundles / Options / Features
- Product Rules (Validation, Selection, Alert)
- Price Rules
- Discount Schedules
- Subscription Pricing
- Approvals
- Contracts & Renewals

*(Each of these gets its own dedicated folder as we progress.)*

## Important Fields/Settings (introduced conceptually here, configured later)
- `SBQQ__Quote__c` — the Quote object (CPQ's core object)
- `SBQQ__QuoteLine__c` — Quote Line Item object
- CPQ Package Settings (org-wide defaults for quoting behavior)

## Best Practices
- Keep product catalog clean before layering CPQ rules on top
- Start rules simple, add complexity only when a real business need exists
- Document every rule's business justification (we'll do this per topic)

## Common Mistakes
- Treating CPQ as "just a pricing calculator" — it's a full configuration
  and process engine
- Overcomplicating bundles before understanding basic product setup
- Skipping Price Book setup, which breaks pricing downstream

## Key Takeaways
- CPQ = Configure + Price + Quote, solving consistency and speed problems
  in complex sales
- It sits on top of standard Salesforce objects (Account, Opportunity,
  Contract) and extends them with its own managed package objects
- Everything flows in one connected path: Quote → Order → Contract →
  Subscription → Renewal
