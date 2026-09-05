# Product Rules — Step-by-Step Build Log

This is the exact sequence followed to build both rules on Business
Laptop. Follow in order — later steps depend on earlier ones existing.

---

# PART 1: VALIDATION RULE
**Goal:** Block "1 Year Warranty" + "Premium Support" from being
selected together.

## Step 1 — Create the Product Rule
Go to: **Product Rules tab → New**

| Field | Value |
|---|---|
| Product Rule Name | `Block 1 Year Warranty with Premium Support` |
| Type | `Validation` |
| Conditions Met | `All` |
| Scope | `Product Options Only` |
| Evaluation Event | `Save` |
| Active | ✅ checked |
| Message | `Premium Support requires 3 Year Warranty. Please select 3 Year Warranty or choose Standard Support instead.` |

Leave Advanced Condition, Evaluation Order, all Lookup fields blank.

**Save.**

## Step 2 — Link the rule to Business Laptop
Go to: **Business Laptop product page → Configuration Rules related list → New**

| Field | Value |
|---|---|
| Product | `Business Laptop` (auto-filled) |
| Product Rule | `Block 1 Year Warranty with Premium Support` |
| Product Feature | leave blank |

**Save.** Confirm Configuration Rules count = 1 on Business Laptop.

## Step 3 — Create Summary Variable #1
Go to: **Summary Variables tab → New**

| Field | Value |
|---|---|
| Name | `1 Year Warranty Sum` |
| Aggregate Function | `Sum` |
| Aggregate Field | `Quantity` |
| Filter Field | (product identifying field available in your org) |
| Filter Operator | `Equals` |
| Filter Value | `TN-OPT-WARRANTY-1YR` |
| Scope | (matching scope option) |

**Save.**

## Step 4 — Create Summary Variable #2
Same place, **New** again:

| Field | Value |
|---|---|
| Name | `Premium Support Sum` |
| Aggregate Function | `Sum` |
| Aggregate Field | `Quantity` |
| Filter Field | same field as Step 3 |
| Filter Operator | `Equals` |
| Filter Value | `TN-SVC-PREMSUPPORT-001` |
| Scope | same as Step 3 |

**Save.**

## Step 5 — Add Error Condition #1
Go to: **The Product Rule from Step 1 → Error Conditions → New**

| Field | Value |
|---|---|
| Tested Object | `--None--` |
| Tested Field | `--None--` |
| Tested Variable | `1 Year Warranty Sum` |
| Operator | `greater than` |
| Filter Type | `Value` |
| Filter Value | `0` |

**Save.**

## Step 6 — Add Error Condition #2
Same rule, **New** again:

| Field | Value |
|---|---|
| Tested Variable | `Premium Support Sum` |
| Operator | `greater than` |
| Filter Type | `Value` |
| Filter Value | `0` |

**Save.** Confirm the rule now shows Error Conditions (2).

## Step 7 — Test
1. Add Business Laptop to a Quote via **Edit Lines → Add Products**.
2. Select **1 Year Warranty** + **Premium Support**.
3. Click **Save** → should show the error message, blocked.
4. Switch to **3 Year Warranty** + **Premium Support**.
5. Click **Save** → should save cleanly, no error.

**Validation Rule complete.**

---

# PART 2: SELECTION RULE
**Goal:** Auto-select Premium Support when 3 Year Warranty is chosen.

## Step 1 — Create Summary Variable
Go to: **Summary Variables tab → New**

| Field | Value |
|---|---|
| Name | `3 Year Warranty Sum` |
| Aggregate Function | `Sum` |
| Aggregate Field | `Quantity` |
| Filter Field | same field used before |
| Filter Operator | `Equals` |
| Filter Value | `TN-OPT-WARRANTY-3YR` |
| Scope | same scope used before |

**Save.**

## Step 2 — Create the Product Rule
Go to: **Product Rules tab → New**

| Field | Value |
|---|---|
| Product Rule Name | `Select Premium Support with 3 Year Warranty` |
| Type | `Selection` |
| Conditions Met | `All` |
| Scope | `Product Options Only` |
| Evaluation Event | `Always` |
| Active | ✅ checked |
| Message | leave blank |

**Save.**

## Step 3 — Link the rule to Business Laptop
Go to: **Business Laptop → Configuration Rules → New**

| Field | Value |
|---|---|
| Product | `Business Laptop` (auto-filled) |
| Product Rule | `Select Premium Support with 3 Year Warranty` |
| Product Feature | leave blank |

**Save.**

## Step 4 — Add the Error Condition
Go to: **This Product Rule → Error Conditions → New**

| Field | Value |
|---|---|
| Tested Variable | `3 Year Warranty Sum` |
| Operator | `greater than` |
| Filter Type | `Value` |
| Filter Value | `0` |

**Save.**

## Step 5 — Add the Action
Same rule → **Actions related list → New**

| Field | Value |
|---|---|
| Type | `Add` |
| Product | `Premium Support` |
| **Required** | ✅ **must be checked** — "Add" type silently fails otherwise |
| Filter Field / Operator / Filter Value / Value Object / Value Field / Value Attribute | leave all blank |

**Save.**

## Step 6 — Test
1. On Business Laptop's configuration screen, select **3 Year Warranty**.
2. Click **Apply Rules** (this org's version needs this manual trigger for "Always" rules to visibly refresh).
3. Confirm **Premium Support** flips to selected in the Support section.

**Selection Rule complete.**

---

## Quick Reference: What Went Wrong Along the Way
1. First tried Error Conditions with Tested Object = Quote Line →
   blocked by scope mismatch → switched to Product Option → still
   couldn't isolate one specific SKU → solved by using Tested
   Variable + Summary Variables instead.
2. First created the Product Rule from the global tab with no
   Configuration Rule → had to add that linking step separately from
   Business Laptop's own related list.
3. Selection Rule's Action didn't fire until the Required checkbox
   was checked (mandatory quirk specific to Type = "Add").
