# Product Rules — Interview Questions

## Basic
**Q: What's the difference between a Validation Rule and a Selection Rule?**
A: Validation Rules block an invalid combination and show an error
message. Selection Rules automatically change what's selected/enabled
based on another selection — no error, just automatic behavior.

**Q: What object links a Product Rule to a specific bundle?**
A: A Configuration Rule — a separate record connecting the rule
definition to a specific Product. A rule isn't active on any bundle
until this link exists.

## Intermediate
**Q: How do you test whether one specific product option is
currently selected, if simply checking "Quantity > 0" on the Product
Option object doesn't work?**
A: Use a Summary Variable — a helper record that sums/counts a
specific filtered set of quote lines (e.g. filtered to one exact
Product Code), then reference that variable in the Error Condition's
Tested Variable field instead of testing the raw object field
directly.

**Q: Why would "Conditions Met = All" matter for a two-condition
Validation Rule?**
A: It determines AND vs OR logic. "All" requires both conditions true
simultaneously (both products selected) before the rule fires — using
"Any" instead would incorrectly block if even one of the two products
was selected alone.

## Advanced / Scenario-Based
**Q: A Validation Rule isn't firing at all, even when the invalid
combination is clearly selected on the configuration screen. What
would you check first?**
A: Check whether a Configuration Rule actually links the Product Rule
to that specific bundle — a rule with correct conditions still does
nothing if it's never linked to the product being configured. Also
verify Active is checked on both the rule and any linking record.

**Q: Why might testing a field directly on an object (like Unit
Quantity on Product Option) fail to correctly identify a specific
product, and how does a Summary Variable solve that?**
A: A direct field test only knows the field's value on whatever
record it evaluates against broadly — it can't narrow to one exact
SKU on its own within this scope. A Summary Variable pre-filters to
one exact product (by Product Code or similar) and pre-aggregates
before the Error Condition checks it, giving precise per-product
testing that a raw field test can't achieve alone.

## Troubleshooting-Based
**Q: Your Error Condition form throws "This combination of
ProductRule.Scope and ErrorCondition.TestedObject is not valid."
What does this mean and how do you fix it?**
A: The Tested Object you chose isn't compatible with the Product
Rule's Scope setting. Different scopes support different Tested
Object types — check which Tested Object options are actually valid
for your chosen Scope, or switch to a Summary Variable-based
condition, which sidesteps this restriction entirely.

## Real-World Implementation
**Q: Why is it valuable to document a failed configuration attempt,
not just the final working one?**
A: It captures the actual reasoning path — useful in interviews to
demonstrate real troubleshooting skill, and useful for your own
future reference so you don't repeat the same dead-end approach on a
similar problem later.
