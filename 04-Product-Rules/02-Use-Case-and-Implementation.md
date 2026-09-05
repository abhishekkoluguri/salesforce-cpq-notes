# Product Rules — Use Case & Implementation (TechNova)

## Business Requirement
(Maps to Requirement #4 in `03-Project-Requirements.md`)
A 3-year warranty cannot be combined with a product that doesn't
support extended coverage. Implemented specifically as: 1 Year
Warranty cannot be selected together with Premium Support, since
Premium Support is designed to pair with extended (3-year) coverage
only.

## Why the Project Needs This
Min/Max Option Count (from Product Bundles) only controls selection
count *within* a single feature. It cannot express logic *across*
features — e.g. "this Warranty choice conflicts with that Support
choice." Product Rules exist specifically for this cross-feature
validation.

## Expected Behavior
Selecting 1 Year Warranty + Premium Support together should block
saving the configuration and show a clear error message. Any other
combination (including 3 Year Warranty + Premium Support) should
save normally.

## Configuration Approach
Built as a Validation-type Product Rule, scoped to Business Laptop,
using two Error Conditions combined with "All" (AND logic).

## Objects Involved
- `SBQQ__ProductRule__c` (the rule itself)
- `SBQQ__ConfigurationRule__c` (links the rule to Business Laptop)
- `SBQQ__ErrorCondition__c` (defines the trigger conditions)
- `SBQQ__SummaryVariable__c` (aggregates selection state per product)

## Configuration Steps Taken

1. Created Product Rule: **"Block 1 Year Warranty with Premium Support"**
   - Type: Validation
   - Conditions Met: All
   - Scope: Product Options Only
   - Evaluation Event: Save
   - Message: "Premium Support requires 3 Year Warranty. Please select
     3 Year Warranty or choose Standard Support instead."

2. Linked the rule to Business Laptop via a **Configuration Rule**
   record (created from Business Laptop's own Configuration Rules
   related list, not the global Product Rules tab — this is what
   actually connects a rule to a specific bundle).

3. **First approach attempted (did not work):** Tried testing
   directly on the Product Option object's Unit Quantity field. This
   failed because it couldn't distinguish *which* specific option was
   selected — it would match any selected option, not specifically
   1 Year Warranty or Premium Support.

4. **Working approach:** Created two Summary Variables:
   - `1 Year Warranty Sum` — sums Quantity filtered to Product Code
     = TN-OPT-WARRANTY-1YR
   - `Premium Support Sum` — sums Quantity filtered to Product Code
     = TN-SVC-PREMSUPPORT-001

5. Created two Error Conditions on the Product Rule, each referencing
   one Summary Variable via the **Tested Variable** field:
   - Condition 1: Tested Variable = `1 Year Warranty Sum`, Operator =
     greater than, Filter Type = Value, Filter Value = 0
   - Condition 2: Tested Variable = `Premium Support Sum`, same
     operator/filter structure

## Testing Steps
1. Added Business Laptop to Quote Q-00009.
2. Selected 1 Year Warranty + Premium Support (deliberately invalid
   combination) → clicked Save.
3. Switched to 3 Year Warranty + Premium Support (valid combination)
   → clicked Save.

## Expected Result
Step 2 blocks with the defined error message. Step 3 saves cleanly.

## Actual Result
✅ Both confirmed exactly as expected:
- Invalid combination blocked with the exact configured error message.
- Valid combination (3 Year Warranty + Premium Support) saved with no error.

## Issues Encountered
1. Creating the Product Rule from the global "Product Rules" tab
   left it unlinked to any specific bundle — had to instead create
   the linking Configuration Rule record from Business Laptop's own
   related list.
2. First Error Condition attempt (Tested Object = Product Option,
   Tested Field = Unit Quantity) saved but could not correctly
   isolate a specific product — it tested "is any option's quantity
   greater than 0," not "is THIS option selected."
3. Required fields not obvious from the form alone: Evaluation Event
   was mandatory and easy to miss; Scope options were named
   differently than expected ("Product Options Only" instead of the
   generic "Group" terminology used in older CPQ documentation).

## Troubleshooting
Root cause of the Tested Object/Field approach failing: without a
way to filter to one specific product on that path, the condition
was structurally unable to express "product X is selected" — only
"some product option somewhere has quantity > 0." Summary Variables
solve this by pre-filtering and aggregating to a single product
before the Error Condition ever checks it.

## Lessons Learned
- Product Rules and their linking Configuration Rules are separate
  records — a rule isn't tied to a bundle until a Configuration Rule
  explicitly links them, created from the bundle's own related list.
- Testing a specific product's selection state requires a Summary
  Variable, not a direct object/field test — this is the correct,
  documented CPQ pattern for "is exactly this SKU selected," not a
  workaround.
- Field names and available options can differ across CPQ package
  versions/orgs (e.g. Scope wording) — always read what the actual
  dropdown offers rather than assuming standard documentation
  wording matches exactly.

## Screenshots
- Configuration screen showing blocked save with error message — captured
<img width="1909" height="948" alt="image" src="https://github.com/user-attachments/assets/230c3418-2b76-4030-917f-f87e5a43d293" />

- Configuration screen showing successful save with valid combination — captured (implied, confirm if you have it)

## Remaining Work For This Topic
## Selection Rule Implementation

### Business Requirement
(Maps to Requirement #3 in `03-Project-Requirements.md`)
If the customer selects 3 Year Warranty, Premium Support should
automatically become selected.

### Objects Involved (in addition to earlier ones)
- `SBQQ__ProductAction__c` (defines what the rule actually does)

### Configuration Steps Taken
1. Created Summary Variable `3 Year Warranty Sum` (same pattern as
   the Validation Rule's variables — sums Quantity filtered to
   Product Code = TN-OPT-WARRANTY-3YR).
2. Created Product Rule **"Select Premium Support with 3 Year Warranty"**:
   - Type: Selection
   - Conditions Met: All
   - Scope: Product Options Only
   - Evaluation Event: Always
   - Message: left blank (Selection Rules don't block/error)
3. Linked to Business Laptop via a Configuration Rule (same pattern
   as before).
4. Created an Error Condition: Tested Variable = `3 Year Warranty Sum`,
   Operator = greater than, Filter Type = Value, Filter Value = 0.
5. Created a Product Action: Type = **Add**, Product = Premium Support.

### Issue Encountered
Initial test failed silently — selecting 3 Year Warranty did not
auto-select Premium Support, even with correct conditions and
Evaluation Event = Always.

### Root Cause
Documented CPQ quirk: when a Product Action's Type is set to **"Add,"
the Required checkbox on that Action record MUST be checked**, or the
action does nothing at all. This isn't intuitive from the field name
alone — "Required" here doesn't describe the target product's
selection lock; it's what makes the "Add" action type actually
execute.

### Solution
Checked the **Required** checkbox on the Product Action record.

### Testing Steps
1. Selected 3 Year Warranty on Business Laptop's configuration screen.
2. Clicked **Apply Rules**.
3. Observed Premium Support flip to selected in the Support section.

### Expected Result
Premium Support auto-selects when 3 Year Warranty is chosen.

### Actual Result
✅ Confirmed — after checking Required on the Action, clicking
**Apply Rules** correctly triggers Premium Support to auto-select.
Note: in this org's CPQ version, the "Always" evaluation event
required an explicit "Apply Rules" click to visibly refresh the
configuration screen, rather than firing instantly on radio button
click.

### Lessons Learned
- The "Required" checkbox on a Product Action is not about locking
  the option from being deselected — for "Add" type actions
  specifically, it's a mandatory flag for the action to function at
  all. This is a documented, known quirk, not intuitive from the UI.
- "Apply Rules" is a legitimate manual trigger in this CPQ version
  for reactive Selection Rules — worth checking for this button
  before assuming a live-reactive rule is broken.

## Final Status
Both Validation Rule and Selection Rule implemented and tested
successfully. Product Rules topic complete.
<img width="959" height="474" alt="image" src="https://github.com/user-attachments/assets/5ead00c2-dd47-4081-ae79-24f23269b4e0" />
