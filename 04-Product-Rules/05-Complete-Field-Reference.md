# Product Rules — Complete Field Reference

This file explains every field we encountered while building Product
Rules, including ones we left blank or didn't use — so the full
picture is documented, not just our specific implementation path.

There are 4 objects involved, always in this relationship:

---

## OBJECT 1: Product Rule
This is the parent record — the rule's identity and overall behavior.

| Field | What It Does | Options / Notes | Did We Use It? |
|---|---|---|---|
| Product Rule Name | Just a label for the rule | Free text | ✅ Yes |
| Type | What kind of rule this is | Validation / Selection / Alert / Filter | ✅ Yes — used both Validation and Selection |
| Conditions Met | AND/OR logic across multiple Error Conditions | All (AND — every condition must be true) / Any (OR — at least one true) | ✅ Yes — used "All" both times |
| Active | Whether the rule runs at all | Checkbox | ✅ Yes — always checked |
| Message | Error text shown to the rep | Free text | ✅ Yes for Validation; ❌ left blank for Selection (Selection Rules don't show errors) |
| Scope | Where the rule is allowed to check/act | Quote / Product Options Only (naming varies by org — some docs call this "Product" or "Group") | ✅ Yes — used "Product Options Only" both times, since our logic lives inside one bundle's configuration |
| Evaluation Order | Controls which rule "wins" if multiple rules could conflict | Number, only matters with multiple competing rules | ❌ Not used — we only ever had one rule active on Business Laptop at a time per type |
| Evaluation Event | WHEN the rule checks its conditions | Save (checks only on save — good for Validation) / Always (checks live, on load and every edit — required for Selection Rules to feel automatic) / Load / Edit (some orgs offer these as separate options) | ✅ Yes — Save for Validation, Always for Selection |
| Advanced Condition | A custom formula instead of simple Error Conditions | Free-text formula syntax | ❌ Not used — our logic was simple enough for standard Error Conditions |
| Lookup Object | Ties the rule to an external custom object for advanced cross-referencing (e.g. checking a Contract's country field) | Picklist of available objects | ❌ Not used — we had no need to look outside the Quote/bundle itself |
| Lookup Type Field | Part of the Lookup Object mechanism — which field identifies record type | Only relevant if Lookup Object is set | ❌ Not used |
| Lookup Product Field | Part of the Lookup Object mechanism — which field maps to a Product | Only relevant if Lookup Object is set | ❌ Not used |
| Lookup Required Field | Part of the Lookup Object mechanism | Only relevant if Lookup Object is set | ❌ Not used |
| Lookup Message Field | Part of the Lookup Object mechanism — pulls a custom error message from the looked-up record | Only relevant if Lookup Object is set | ❌ Not used |

**When would you actually use Lookup Object fields?** Real-world example: a rule that only fires for customers in specific countries, checking a custom "Regional Compliance" object rather than anything on the Quote itself. Advanced, rare, skip until a real use case demands it.

---

## OBJECT 2: Configuration Rule
This is the small linking record — it doesn't contain logic itself,
it just says "this Product Rule applies to this specific Product."

| Field | What It Does | Options / Notes | Did We Use It? |
|---|---|---|---|
| Product | The bundle this rule applies to | Lookup to Product2 | ✅ Yes — Business Laptop |
| Product Rule | The rule being linked | Lookup to the Product Rule record | ✅ Yes |
| Product Feature | Narrows the rule to only run within ONE specific Feature, instead of the whole bundle | Lookup to a Feature | ❌ Not used — our rules needed to see across multiple features (Warranty AND Support), so we left this blank to apply at the whole-bundle level |
| Parent Bundle Condition Level | For nested bundles (a bundle inside another bundle) — controls whether the rule looks at the parent bundle's selections | None / options vary | ❌ Not used — we have no nested bundles in this project |
| Child Bundle Condition Level | Same idea, but for checking a child bundle's selections | None / options vary | ❌ Not used |
| Child Bundle Action Level | Same idea, but for where an Action applies in a nested structure | None / options vary | ❌ Not used |

**When would you use Product Feature here?** If you had a rule that only needed to check/act within the RAM feature specifically (e.g. "if 16GB RAM selected, show a note") — scoping to one Feature avoids the rule needlessly re-checking on unrelated feature changes.

**When would you use the Bundle Level fields?** Real-world example: TechNova sells a "Server Rack" bundle that itself contains a "Server" bundle inside it (nested). A rule checking something on the child Server's selections, but acting on the parent Rack, would need these fields.

---

## OBJECT 3: Error Condition
Defines WHEN the rule's condition is true. A rule can have multiple
Error Conditions, combined by the parent rule's "Conditions Met" (All/Any).

| Field | What It Does | Options / Notes | Did We Use It? |
|---|---|---|---|
| Rule | Which Product Rule this condition belongs to | Auto-filled from context | ✅ Yes |
| Tested Object | Which object/context to check a field on directly | Quote / Quote Line / Quote Line Group / Product Option / Configuration Attributes / Upgraded Asset | ❌ Not used in our final version — we tried Product Option + Unit Quantity first, but it couldn't isolate ONE specific product; we switched to Tested Variable instead |
| Tested Field | The specific field to check, once Tested Object is set | Depends on Tested Object chosen | ❌ Not used in final version, same reason |
| Tested Attribute | Checks a Configuration Attribute's value instead of a standard field | Lookup to Attribute Items | ❌ Not used — we have no Configuration Attributes in this project yet |
| Tested Variable | Checks a Summary Variable's calculated value instead | Lookup to a Summary Variable record | ✅ Yes — this is what actually worked for isolating specific products |
| Operator | The comparison being made | Equals, Not Equal, Greater Than, Less Than, etc. | ✅ Yes — "Greater Than" |
| Filter Type | Whether we're comparing to a fixed value or another variable | Value / Variable | ✅ Yes — "Value" |
| Filter Value | The literal number/text being compared against (used when Filter Type = Value) | Free text/number | ✅ Yes — "0" |
| Filter Variable | A second Summary Variable to compare against, instead of a fixed value (used when Filter Type = Variable) | Lookup to another Summary Variable | ❌ Not used — we always compared to a fixed number (0), not another calculated variable |

**When would Tested Object/Tested Field actually work?** They're valid for scopes like "Quote" (checking something across the whole Quote, not isolated to one bundle's options) — our specific combination (Product Options Only scope + wanting one exact SKU) is exactly the case that Salesforce docs point toward Summary Variables for.

**When would you use Filter Variable instead of Filter Value?** Real-world example: "Product A's quantity should not exceed Product B's quantity" — comparing two calculated sums to each other, rather than either one to a fixed number.

---

## OBJECT 4: Product Action (Selection Rules only — Validation Rules don't use this)
Defines WHAT HAPPENS when the rule's conditions are true.

| Field | What It Does | Options / Notes | Did We Use It? |
|---|---|---|---|
| Rule | Which Selection Rule this action belongs to | Auto-filled | ✅ Yes |
| Type | The actual action performed | Add, Remove, Enable, Disable, Enable Add, Disable Remove, Show, Hide, Show and Add, Hide and Remove, Default Filter, Optional Filter | ✅ Yes — "Add" |
| Product | The target product the action applies to | Lookup to Product2 | ✅ Yes — Premium Support |
| **Required** | **Critical quirk:** MUST be checked when Type = "Add," or the action silently does nothing. Must be UNCHECKED for Hide/Disable/Remove types, or those won't work either. | Checkbox | ✅ Yes — checked (this was our actual bug fix) |
| Filter Field | Dynamically targets a group of products by field value, instead of one specific Product | Picklist of fields | ❌ Not used — we targeted one exact product (Premium Support) directly |
| Operator | Comparison operator for the Filter Field/Value combo | Same style as Error Condition operators | ❌ Not used |
| Filter Value | The value being filtered on | Free text | ❌ Not used |
| Value Object | Advanced — used when the action's effect should pull from another object's field dynamically | Picklist | ❌ Not used |
| Value Field | Paired with Value Object | Picklist | ❌ Not used |
| Value Attribute | Paired with dynamic Configuration Attribute-based actions | Lookup | ❌ Not used |

**When would you use Type variants like "Enable Add" vs plain "Add"?**
Real-world example from Trailhead: "Enable & Add" both enables an
option AND auto-selects it in one action — useful when the option
starts disabled/hidden and needs both states changed at once. Plain
"Add" assumes the option is already enabled/visible and just needs
selecting.

**When would you use Filter Field instead of Product?** Real-world
example: "Disable all dairy-related options" — instead of creating
one Action per dairy product, filter by Product Family = "Dairy" and
disable all matching options in one Action record.

---

## SEPARATE OBJECT: Summary Variable
Not part of the Product Rule hierarchy directly — a standalone helper
that Error Conditions reference via "Tested Variable."

| Field | What It Does | Options / Notes | Did We Use It? |
|---|---|---|---|
| Name | Label for the variable | Free text | ✅ Yes |
| Aggregate Function | How values are combined | Sum / Count / Max / Min | ✅ Yes — "Sum" |
| Aggregate Field | Which field's values get aggregated | e.g. Quantity | ✅ Yes — "Quantity" |
| Filter Field | Which field narrows down WHICH lines get included in the aggregate | e.g. Product Code | ✅ Yes |
| Filter Operator | Comparison for the filter | Equals, etc. | ✅ Yes — "Equals" |
| Filter Value | The value being filtered to | e.g. our specific product code | ✅ Yes |
| Scope | Where this variable calculates within (must generally match the Product Rule's Scope that will use it) | Same family of options as Product Rule Scope | ✅ Yes |

---

## Summary: Why We Hit Errors

| Error We Hit | Root Cause | Field That Fixed It |
|---|---|---|
| "This combination of ProductRule.Scope and ErrorCondition.TestedObject is not valid" | Tried Tested Object = Quote Line while Scope = Product Options Only — incompatible pairing | Switched to Tested Variable (bypasses this restriction) |
| Couldn't isolate one specific product using Tested Object/Field | Direct field tests can't filter to one exact SKU within this scope | Used Summary Variable with Filter Field/Value to pre-filter to one product |
| Selection Rule created but Premium Support never auto-selected | Action Type = "Add" was used with Required left unchecked | Checked Required on the Action record |
| Rule not linked to any bundle at first | Created Product Rule from the global tab, no Configuration Rule existed yet | Created the Configuration Rule from Business Laptop's own related list |

## Key Takeaway
Almost every error we hit came down to one of two things: **a
field/scope combination that Salesforce restricts** (fixed by
switching mechanisms, e.g. to Summary Variables), or **a
non-intuitive required field that doesn't do what its name suggests**
(the Required checkbox on Actions). Neither was really "wrong
configuration" — they're genuine, documented CPQ quirks worth
knowing going into any real implementation.
