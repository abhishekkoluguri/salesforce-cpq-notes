# Selection Rules — Theory (Addendum to Product Rules)

## What's Different From a Validation Rule
A Validation Rule checks a condition and BLOCKS with an error if true.
A Selection Rule checks a condition and AUTOMATICALLY CHANGES a
selection — no error, no blocking, just an automatic action.

## The New Piece: Product Actions
Where Validation Rules only need Error Conditions (check + message),
Selection Rules need Error Conditions (the trigger) PLUS a
**Product Action** (what actually happens) — the "then do X" half
that Validation Rules don't have.

## Key Difference: Evaluation Event
Validation Rules typically use Evaluation Event = **Save** (check when
saving). Selection Rules use Evaluation Event = **Always** — this
means the rule reacts live, both when the configuration screen first
opens AND whenever the customer changes a selection, not just at save
time. This makes sense: you want Premium Support to auto-select the
moment 3 Year Warranty is picked, not only after clicking Save.

## Our Rule
**Trigger:** 3 Year Warranty is selected
**Action:** Premium Support becomes selected automatically
