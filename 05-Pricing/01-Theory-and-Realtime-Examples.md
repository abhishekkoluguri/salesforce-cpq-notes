# Pricing — Theory & Real-Time Examples

## Definition
Pricing in Salesforce CPQ determines how the **Net Price** of each
Quote Line is calculated — starting from a base List Price and
applying whatever pricing logic, adjustments, and methods are
configured, before any manual discount is even applied.

## Purpose
Different products need to be priced differently: a one-time hardware
sale, a per-seat monthly software subscription, and a fixed-fee
service shouldn't all use the same math. Pricing configuration is
what tells CPQ *how* to calculate each type correctly and
consistently, without the rep doing math by hand.

## Why It Is Needed
Without configured pricing methods, every product would just show
its flat List Price with no ability to reflect quantity-based
subscription math, cost-based markups, or customer-specific
contracted rates — exactly the "manual, inconsistent pricing"
problem from TechNova's original business case.

## The Pricing Waterfall (Conceptual Flow)
This is the order CPQ works through for every Quote Line:
List Price
↓
Pricing Method applied (List / Cost / Block / Percent of Total)
↓
Price Rules applied (if any — automated field adjustments)
↓
Discounts applied (Discount Schedules, manual discounts)
↓
Net Price (final calculated price shown to customer)


## Important Terminology
| Term | Meaning |
|---|---|
| List Price | The base price from the Price Book Entry |
| Pricing Method | The field on Product2 controlling how price is calculated (List, Cost, Block, % of Total) |
| Net Price | The final calculated price after all adjustments/discounts |
| Price Rule | Automated logic that adjusts price-related fields based on conditions |
| Subscription Pricing | Pricing tied to a recurring term (monthly/annual), quantity-based |
| Contracted Price | A customer-specific negotiated price, overriding the standard price book |

## Pricing Methods Explained
| Method | How It Works | Example |
|---|---|---|
| **List** | Uses the flat List Price as-is | Business Laptop at $1,200 flat |
| **Cost** | Price = Cost + a defined markup (% or fixed amount) | A distributor reselling at cost+15% |
| **Block** | Price changes based on quantity tiers/blocks, not a smooth discount curve | "1-10 units = $X each, 11-50 = $Y each" as fixed blocks |
| **% of Total** | Price is calculated as a percentage of another product/bundle's total | Implementation Service priced at 10% of the hardware total |

## How Subscription Pricing Works (Conceptually)
For recurring products (like Premium Support, Cloud Productivity
Suite), CPQ needs additional info beyond a flat price:
- **Subscription Term** — how long the subscription runs (e.g. 12
  months, 36 months)
- **Billing Frequency** — how often it's billed within that term
  (monthly, annually, one-time)
- **Pricing per unit** — often per-seat/per-license, multiplied by
  quantity and term

The Net Total for a subscription product reflects quantity × unit
price × relevant term factor, not just a flat one-time number like
hardware.

## Real-World Example
A SaaS company selling per-seat software might price "50 seats,
12-month term" as: $15/seat/month × 50 seats × 12 months = $9,000
annual contract value — CPQ calculates this automatically once
subscription fields are configured, rather than the rep doing this
math by hand.

## Business Scenario (TechNova)
- **Business Laptop, Monitor, Server** — one-time Hardware sales,
  List pricing method, flat price × quantity.
- **Cloud Productivity Suite, Security Software, Analytics Platform,
  Premium Support** — subscription products, priced per user per
  month/term.
- **Implementation Service, Training Service** — one-time Services,
  flat List pricing.

This mixed catalog is exactly why Pricing Methods matter — TechNova
can't treat a $1,200 one-time laptop and a $15/month software seat
the same way.

## Related CPQ Concepts
- Discount Schedules (next topic) — applied AFTER pricing method
  calculates the base Net Price
- Price Rules — automated adjustments, different from manual
  discounting
- Contracted Pricing — customer-specific negotiated rates, relevant
  later in Contracts/Renewals

## Important Fields/Settings
- `Product2.SBQQ__PricingMethod__c` — List / Cost / Block / % of Total
- `Product2.SBQQ__SubscriptionPricing__c` — marks a product as
  subscription-priced
- `Product2.SBQQ__SubscriptionType__c` / Term fields — govern
  subscription duration and billing

## Best Practices
- Decide pricing method per product deliberately — don't leave
  everything on default "List" if a product genuinely needs
  cost-based or percent-of-total logic
- Keep subscription term fields consistent across similar products
  (e.g. don't mix monthly and annual billing arbitrarily)

## Common Mistakes
- Marking a one-time product (like Implementation Service) as
  subscription-priced by accident, causing incorrect recurring totals
- Forgetting that Pricing Method changes require testing on an actual
  Quote — the change alone doesn't visually confirm correctness until
  you see the calculated Net Total

## Key Takeaways
- Pricing Method determines the base calculation approach before any
  discount touches the price
- Subscription products need term/quantity/frequency fields, not just
  a flat price
- TechNova's mixed catalog (hardware + subscription software +
  one-time services) is a realistic reason to understand more than
  one pricing method
