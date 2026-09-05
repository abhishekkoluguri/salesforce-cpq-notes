# Product Rules — Theory & Real-Time Examples

## Definition
A **Product Rule** in Salesforce CPQ is a piece of business logic
that controls what happens during bundle configuration — beyond what
Min/Max Option Count alone can enforce. Rules react to *what the
customer has already selected* and either change what's available,
show a message, or block an invalid save.

## Purpose
Min/Max Option Count only controls "how many options within THIS
feature." It can't express cross-feature logic like "if you pick
Warranty option A, make Support option B available" — that's exactly
what Product Rules exist for.

## Why It Is Needed
Real products have dependencies between different parts of their
configuration. Min/Max alone can't say "these two choices only make
sense together" or "this combination is invalid" — you need rules
that look across features, not just within one.

## The Four Types of Product Rules
| Type | What It Does | Example |
|---|---|---|
| **Validation Rule** | Blocks an invalid combination with an error message | 3-Year Warranty can't pair with a non-extended-coverage product |
| **Selection Rule** | Automatically selects/deselects/enables an option based on another selection | Selecting 3-Year Warranty auto-enables/selects Premium Support |
| **Alert Rule** | Shows a warning message but does NOT block saving | "Note: Premium Support is recommended with 3-Year Warranty" |
| **Filter Rule** | Filters which options are even shown, based on other selections | Only show Storage options above 512GB when Server is selected (not used yet in our project) |

## How It Works (Conceptually)
1. You create a **Product Rule** record (scoped to a specific bundle,
   e.g. Business Laptop), with a **Rule Type** (Validation/Selection/
   Alert/Filter).
2. You define **Error Condition(s)** or **Rule Actions** — these
   reference specific Product Options using "lookup formulas" or a
   simple condition builder depending on rule type.
3. For Validation: define the condition that makes the combination
   invalid, plus the error message shown.
4. For Selection: define a **Product Rule Action** — which specific
   option gets selected/enabled/unselected when the trigger condition
   is met.
5. The rule fires live on the configuration screen as the customer
   makes selections — no separate "save and check" step; it's
   immediate.

## Important Terminology
| Term | Meaning |
|---|---|
| Product Rule | The parent record defining rule type and scope |
| Rule Condition | What triggers the rule (a specific option being selected) |
| Error Condition | The specific combination a Validation Rule blocks |
| Product Rule Action | What a Selection Rule actually does (select/unselect/enable/disable) |
| Lookup Object / Lookup Object Field | Advanced way to reference options in conditions (we'll use simpler condition builder first) |

## Real-World Example
A phone company's CPQ might have a Validation Rule: "You cannot select
an international calling plan without also having an active SIM
product on the Quote" — blocking an order that wouldn't actually work
for the customer.

## Business Scenario (TechNova)
Two rules from our original project plan, now that Bundles exist:

**Selection Rule:** If the customer selects **3 Year Warranty**, the
**Premium Support** option should automatically become selected (or
at minimum, enabled/highlighted) — since it makes business sense to
pair long warranty with premium support.

**Validation Rule:** For this project, we'll implement it as: a
customer **cannot** select **1 Year Warranty** together with
**Premium Support** — because Premium Support is designed to pair
with extended (3-year) coverage only. This gives us a concrete,
testable validation scenario using options we already built.

## Related CPQ Concepts
- Product Bundles/Options/Features (already built — rules operate on
  top of these)
- Price Rules (different concept — those adjust pricing values, not
  selection logic; covered in the Pricing topic)

## Important Fields/Settings
- `SBQQ__ProductRule__c` — parent rule record
- `SBQQ__ErrorCondition__c` — condition definition for Validation Rules
- `SBQQ__ProductAction__c` — what a Selection Rule actually does
- Rule Type field: Validation / Selection / Alert / Filter
- Scope: which bundle the rule applies to (Business Laptop, in our case)

## Best Practices
- Start with the simplest possible condition (single option triggers
  single action) before building multi-condition logic
- Write clear, customer-facing error messages on Validation Rules —
  "Invalid combination" tells a rep nothing useful
- Test each rule immediately after creating it, one at a time

## Common Mistakes
- Scoping a rule to the wrong bundle/product, so it never fires
- Writing a Validation Rule condition that's technically backwards
  (blocks the valid combination instead of the invalid one) — always
  re-read the condition literally before saving
- Forgetting that Selection Rules need an explicit **Action** record,
  not just a condition — the condition alone does nothing without a
  defined action

## Key Takeaways
- Product Rules add cross-feature logic that Min/Max Option Count
  cannot express alone
- Validation = blocks and errors; Selection = automatically changes
  what's picked; Alert = warns without blocking; Filter = changes
  what's shown
- Every rule needs both a trigger condition AND (for Selection) an
  explicit action — one without the other does nothing
