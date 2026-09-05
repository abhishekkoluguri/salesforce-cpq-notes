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
