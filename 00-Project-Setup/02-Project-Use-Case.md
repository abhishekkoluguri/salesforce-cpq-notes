# Project Use Case — TechNova Solutions

## Company
**TechNova Solutions** is a fictional B2B technology company used as the
continuous project for this Salesforce CPQ learning repository.

## Business Model
TechNova sells hardware, software, and services to business customers,
often as bundled deals with multi-year contracts.

## Products

### Hardware
- Business Laptop
- Monitor
- Server

### Software
- Cloud Productivity Suite
- Security Software
- Analytics Platform

### Services
- Implementation Service
- Premium Support
- Training Service

## Current Business Problem
TechNova currently relies on manual quoting. Sales reps manually determine:
- Which products can be sold together
- Which product options are compatible
- Product prices
- Quantity-based pricing
- Customer-specific pricing
- Discounts
- Subscription pricing
- Service charges
- Contract duration
- Renewal requirements

This causes:
- Incorrect product configurations
- Incorrect pricing and discounts
- Slow quote generation
- Manual calculations
- Pricing inconsistency
- Difficulty managing complex bundles
- Lack of centralized business rules
- Approval delays
- Difficult contract and renewal management

## Why CPQ Is Required
Salesforce CPQ centralizes product, pricing, and discounting logic so that:
- Reps can only configure valid combinations of products
- Pricing is calculated automatically and consistently
- Discounts above a threshold trigger approval automatically
- Quotes, contracts, and renewals follow one connected data flow

## Example Customer Requirement
A customer wants:
- 50 Business Laptops
- 50 Monitors
- 50 Premium Support subscriptions
- Cloud Productivity Suite
- Security Software
- Implementation Service
- 3-year contract
- Volume discount

## Proposed Solution
Implement Salesforce CPQ so a rep can select these products on a Quote,
have the system enforce valid configurations, calculate pricing and volume
discounts automatically, route large discounts for approval, and generate
a Contract with Subscriptions that will later support renewal.

## Example Business Rules (to be implemented progressively)
| Rule Type | Description |
|---|---|
| Configuration Rule | If 3-year warranty is selected, Premium Support becomes available |
| Validation Rule | 3-year warranty cannot be selected on products without extended warranty support |
| Pricing Rule | More than 20 laptops → volume discount applies |
| Discount Approval | Discount above threshold → manager approval required |
| Subscription Pricing | Software priced by quantity, term, product, and applicable discounts |

## Quote Process (target end state)
Account → Opportunity → CPQ Quote → Select Products → Configure Products →
Apply Configuration Rules → Calculate Pricing → Apply Discounts → Approval →
Generate Quote

## Contract Process (target end state)
Quote → Order → Contract → Subscription

## Renewal Process (target end state)
Subscription nearing end date → Renewal Opportunity/Quote generated →
Updated pricing and terms → Renewed Contract

## Project Success Criteria
- All core CPQ objects configured and connected in one continuous org
- Example customer requirement above can be fully quoted end-to-end
- Every concept documented with theory, implementation, and interview notes
- Screenshots captured for every configuration step
