Salesforce CPQ — Technical Notes

1. CPQ — Configure, Price, Quote

Definition: Salesforce CPQ (Configure, Price, Quote) is a Salesforce solution used to configure the right products, calculate the correct price, and generate customer quotes.


Example: ABC wants 100 CRM users. CPQ helps select the correct CRM package, apply pricing/discount rules, and create the quote.


Flow: Configure → Price → Quote



2. Account

Definition: An Account represents a customer organization or company in Salesforce.


Example: ABC Technologies is the customer buying CloudNova CRM, so ABC Technologies is the Account.



3. Opportunity

Definition: An Opportunity represents a potential sales deal with a customer.


Example: CloudNova creates an Opportunity for ABC Technologies for a potential ₹10 lakh CRM deal.



4. Product

Definition: A Product represents an item or service that a company sells.


Example: CloudNova CRM Enterprise, Premium Support, and Implementation Service can each be Products.



5. Price Book

Definition: A Price Book is a collection of products and their prices.


Example: CloudNova may have a Standard Price Book with CRM Enterprise at ₹1,000 per user/month and a Partner Price Book with special pricing.



6. Quote

Definition: A Quote is a formal sales proposal containing the products, quantities, prices, discounts, and terms offered to a customer.


Example: CloudNova creates a quote for ABC containing 100 CRM Enterprise users and Premium Support.



7. Quote Line

Definition: A Quote Line represents an individual product/service and its quantity and pricing details on a Quote.


Example: On ABC's quote, “CRM Enterprise — 100 users” is one Quote Line.



8. Quote Line Editor (QLE)

Definition: QLE is the CPQ interface used by sales users to add products, configure bundles, modify quantities, apply discounts, and review pricing.


Example: A salesperson opens QLE, selects CRM Enterprise, chooses 100 users, adds support, and sees the calculated price.



9. Bundle

Definition: A Bundle is a product configured with related child products/options that can be selected together as one solution.


Example: “CloudNova CRM Enterprise Package” can be a bundle containing CRM licenses, Premium Support, and Implementation.



10. Product Feature

Definition: A Product Feature is a logical grouping of product options inside a bundle.


Example: Inside the CRM bundle, a “Support” Feature can contain Standard Support and Premium Support options.



11. Product Option

Definition: A Product Option is a child product that can be selected as part of a bundle.


Example: Premium Support is a Product Option of the CRM Enterprise bundle.



12. Option Constraint

Definition: An Option Constraint controls whether one product option can or cannot be selected with another option.


Example: “Basic Support” cannot be selected together with “Premium Support.”


Simple idea: Product-to-product compatibility control.



13. Configuration Attribute

Definition: A Configuration Attribute is a field displayed during product configuration to capture a value that influences or describes the bundle configuration.


Example: When configuring CRM, the user enters “Number of Users = 100” or selects “Deployment = Cloud.”



14. Product Rule

Definition: A Product Rule applies business logic during product configuration to control product selection and configuration.


Main types:



Validation

Selection

Filter

Alert


Example: If ABC selects Enterprise CRM, CloudNova automatically requires Premium Support.



15. Pricing / Pricing Waterfall

Definition: CPQ pricing determines the final selling price of a product by applying the applicable pricing methods, discounts, and adjustments.


Simplified waterfall:


List Price → Discount → Regular Price → Additional Discount → Customer Price → Net Price


Example: A CRM license has a list price of ₹1,000. A customer discount reduces the selling price to ₹850.



16. Discount Schedule

Definition: A Discount Schedule applies different discounts based on quantity or other defined tiers.


Example:



1–50 users → 0% discount

51–100 → 10%

101–500 → 15%


If ABC buys 120 users, the applicable tier can provide a 15% discount.



17. Block Pricing

Definition: Block Pricing charges a fixed price for a defined quantity block rather than calculating price simply as quantity × unit price.


Example: 1–100 users may cost ₹50,000 as one block. Buying 80 or 100 users can therefore use the same block price.



18. Percent of Total

Definition: Percent of Total pricing calculates a product's price as a percentage of other quote line values.


Example: CloudNova charges Implementation Service at 10% of the total CRM subscription value.



19. Contracted Price

Definition: A Contracted Price is a customer-specific negotiated price for a product.


Example: Standard CRM price is ₹1,000/user/month, but ABC has negotiated ₹800/user/month.



20. Price Rule

Definition: A Price Rule is used to apply custom pricing logic during the CPQ calculation process.


Simple logic:


IF condition → THEN perform pricing action.


Example: If the customer is ABC Technologies, apply a special implementation fee.



21. Price Condition

Definition: A Price Condition defines the condition that must be true for a Price Rule to execute.


Example: Customer = ABC Technologies.


This is the IF part of the rule.



22. Price Action

Definition: A Price Action defines what CPQ should change when the Price Rule conditions are satisfied.


Example: Set the Implementation Fee to ₹50,000.


This is the THEN part of the rule.



23. Lookup Query

Definition: A Lookup Query allows CPQ to retrieve a value from lookup data and use that value in pricing logic.


Example: A pricing table stores special prices by customer and product. CPQ looks up ABC's CRM price and applies it.



24. Summary Variable

Definition: A Summary Variable summarizes or aggregates information from quote lines so that CPQ rules can use the result.


Example: Calculate the total number of CRM users across quote lines. If total users exceed 500, apply a special discount.



25. Subscription Product

Definition: A Subscription Product is a product sold for a recurring period and generates recurring charges.


Example: CRM Enterprise costs ₹1,000 per user per month and is subscribed to for 12 months.



26. Proration

Definition: Proration calculates a charge based on the actual portion of a subscription period used.


Example: If an annual subscription starts halfway through a billing period, CPQ can calculate only the applicable partial-period amount.



27. MDQ — Multi-Dimensional Quoting

Definition: MDQ allows a subscription quote to be divided into time segments so that quantity, price, or discount can vary across different periods.


Example:



Year 1 → 100 users

Year 2 → 150 users

Year 3 → 200 users


Each segment can have its own values.



28. Quote Template

Definition: A Quote Template controls the structure and presentation of the customer-facing quote document.


Example: CloudNova's quote PDF contains the customer details, products, quantities, pricing, discounts, terms, and company branding.



29. Approval

Definition: An Approval process ensures that certain quotes or commercial decisions are reviewed before they can proceed.


Example: If a salesperson gives ABC a discount greater than 20%, manager approval may be required.



30. Order

Definition: An Order represents the customer's accepted purchase and the products/services that should be fulfilled.


Example: ABC accepts the quote for 100 CRM users, and CloudNova creates an Order.



31. Contract

Definition: A Contract represents the formal agreement between the seller and customer for the purchased products/services.


Example: ABC signs a 12-month agreement with CloudNova for CRM services.



32. Subscription

Definition: A Subscription represents a recurring product/service purchased under a contract, including its term, quantity, and recurring pricing information.


Example: ABC has 100 CRM Enterprise subscriptions for 12 months.



33. Amendment

Definition: An Amendment changes an existing contract/subscription during its active term.


Example: ABC originally purchased 100 users but later increases the subscription to 150 users. CPQ processes the change through an Amendment.



34. Renewal

Definition: Renewal is the process of extending a customer's expiring subscription or contract for another term.


Example: ABC's 12-month CRM contract is ending. CloudNova creates a renewal opportunity/quote for the next 12 months.



35. QCP — Quote Calculator Plugin

Definition: QCP is a JavaScript-based customization mechanism used to extend CPQ's standard calculation behavior when standard configuration cannot satisfy a requirement.


Example: CloudNova needs a complex custom calculation involving multiple quote lines that cannot be achieved using standard pricing configuration. QCP can implement the calculation.



36. Integrations

Definition: CPQ integrations connect Salesforce CPQ with external systems so that quote, order, customer, billing, or product information can move between systems.


Example: After ABC accepts the quote, CPQ can send order information to a billing or ERP system for invoicing and fulfillment.



37. Complete CPQ Business Flow

Definition: The complete CPQ lifecycle connects customer, sales, product configuration, pricing, quoting, approval, ordering, contracting, subscription management, amendments, and renewals.


Flow:


Account
↓
Opportunity
↓
Quote
↓
Configure Products
↓
Product Rules
↓
Pricing
↓
Price Rules / Discounts
↓
Approval
↓
Quote Template
↓
Customer Accepts
↓
Order
↓
Contract
↓
Subscription
↓
Amendment
↓
Renewal

