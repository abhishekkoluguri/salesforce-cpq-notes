Salesforce CPQ — Complete Real-World Example
CloudNova Technologies → ABC Technologies
Scenario
CloudNova Technologies sells CRM software.
ABC Technologies wants to purchase a CRM solution for its employees.
ABC initially needs 100 CRM users for 12 months.
1. Account
CloudNova creates/uses an Account:
ABC Technologies
This identifies the customer organization.
2. Opportunity
CloudNova creates an Opportunity:
ABC Technologies — CRM Implementation
This represents the potential CRM deal.
3. Products
CloudNova has these Products:
CloudNova CRM Enterprise
Premium Support
Implementation Service
4. Price Book
CloudNova's Standard Price Book contains:
CRM Enterprise: ₹1,000/user/month
This gives CPQ the base product price.
5. Quote
The salesperson creates a Quote for ABC.
The quote represents the commercial proposal CloudNova is making to ABC.
6. Quote Lines
The Quote contains lines such as:
CRM Enterprise — 100 users
Premium Support
Implementation Service
Each individual item is represented by a Quote Line.
7. QLE
The salesperson opens the Quote Line Editor.
They select the CRM package, configure the required options, enter the required values, and review the calculated pricing.
QLE acts like an intelligent shopping cart.
8. Bundle
CloudNova configures CRM Enterprise Package as a Bundle.
The bundle can contain:
CRM Enterprise
Support
Implementation
The salesperson can configure the complete solution from the bundle.
9. Product Feature
Inside the bundle, CloudNova creates a Feature:
Support
This groups the available support options.
10. Product Option
Under the Support Feature:
Premium Support
is configured as a Product Option.
11. Option Constraint
CloudNova does not want customers to select both:
Basic Support
Premium Support
Therefore, an Option Constraint prevents the incompatible combination.
12. Configuration Attribute
During configuration, the salesperson enters:
Number of Users = 100
This is captured through a Configuration Attribute.
13. Product Rule
CloudNova has a business requirement:
Enterprise customers must have Premium Support.
A Product Rule checks the configuration and ensures Premium Support is selected.
14. Pricing Waterfall
CRM Enterprise has a list price of:
₹1,000/user/month
For 100 users:
100 × ₹1,000 = ₹100,000/month
CPQ then applies the applicable pricing and discounts to arrive at the final selling price.
15. Discount Schedule
CloudNova offers volume discounts:
1–50 users → 0%
51–100 users → 10%
101–500 users → 15%
ABC buys 100 users, so the applicable volume discount is 10%.
16. Block Pricing
Suppose CloudNova also sells an implementation package as:
1–100 users = ₹50,000
The price is based on the defined block rather than simply multiplying a unit price.
17. Percent of Total
CloudNova can price Implementation Service as:
10% of the applicable CRM value
For example, if the relevant CRM value is ₹100,000, implementation can be calculated as ₹10,000.
18. Contracted Price
ABC has negotiated a special CRM price.
Standard price:
₹1,000/user/month
ABC's contracted price:
₹800/user/month
CPQ can apply the customer-specific Contracted Price.
19. Price Rule
CloudNova has another business requirement:
ABC Technologies receives a special implementation fee.
A Price Rule can identify ABC and modify the implementation pricing.
20. Price Condition
The Price Rule condition is:
Customer = ABC Technologies
This is the IF part.
21. Price Action
When the condition is true:
Set Implementation Fee = ₹50,000
This is the THEN part.
22. Lookup Query
Instead of hardcoding customer prices, CloudNova can maintain pricing data in lookup data.
CPQ looks up:
Customer = ABC + Product = CRM Enterprise
and retrieves the applicable special price.
23. Summary Variable
CloudNova wants a rule based on total users.
If the total CRM users across the quote are greater than 500, a special commercial rule can be applied.
A Summary Variable can calculate the required total.
24. Subscription Product
CRM Enterprise is a recurring subscription product.
ABC purchases:
100 users × 12 months
The customer pays for the recurring CRM service during the subscription term.
25. Proration
Suppose ABC starts the subscription partway through a billing period.
CPQ can calculate the charge for only the applicable portion of that period.
26. MDQ
Later, ABC wants different quantities each year:
Year 1: 100 users
Year 2: 150 users
Year 3: 200 users
MDQ allows the quote to represent these different time segments.
27. Quote Template
After pricing is complete, CloudNova generates the customer-facing quote.
The Quote Template controls the document layout, including:
Customer information
Products
Quantities
Prices
Discounts
Terms
28. Approval
The salesperson wants to provide ABC with a discount greater than the allowed threshold.
CloudNova requires manager approval.
The quote goes through the required Approval process before it can proceed.
29. Order
ABC accepts the quote.
CloudNova creates an Order representing the accepted purchase.
The Order contains the products/services ABC purchased.
30. Contract
CloudNova creates a Contract for the agreement.
Example:
CRM Enterprise — 12-month agreement
The Contract represents the formal customer agreement.
31. Subscription
ABC now has a subscription for:
100 CRM users for 12 months
This represents the recurring service purchased under the contract.
32. Amendment
After six months, ABC needs more users.
Original:
100 users
New requirement:
150 users
CloudNova processes an Amendment to modify the active subscription/contract.
33. Renewal
At the end of the 12-month term, ABC wants to continue using CloudNova CRM.
CloudNova starts the Renewal process and prepares the next subscription term.
34. QCP
Suppose CloudNova introduces a highly complex calculation involving multiple quote lines and custom business logic that standard CPQ configuration cannot easily handle.
A Quote Calculator Plugin (QCP) can be used to implement the custom calculation using JavaScript.
35. Integrations
CloudNova may integrate CPQ with external systems.
Example:
Salesforce CPQ → Billing System
The accepted order information can be sent to the billing system for invoicing.
36. Complete Customer Journey
ABC's complete journey is:
ABC Technologies
      ↓
Account
      ↓
Opportunity
      ↓
Quote
      ↓
QLE
      ↓
Bundle
      ↓
Features + Options
      ↓
Configuration Attributes
      ↓
Product Rules
      ↓
Pricing
      ↓
Discounts / Contracted Price
      ↓
Price Rules
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
37. Final Mental Picture
Think of CloudNova's CPQ process as a salesperson answering five questions:
1. WHO?
Account → ABC Technologies
2. WHAT ARE THEY BUYING?
Products → CRM Enterprise, Support, Implementation
3. WHAT CAN THEY CONFIGURE?
Bundle → Features → Options → Attributes → Product Rules
4. HOW MUCH SHOULD THEY PAY?
Price Book → Pricing → Discounts → Contracted Price → Price Rules
5. WHAT HAPPENS AFTER THEY BUY?
Quote → Approval → Order → Contract → Subscription → Amendment → Renewal
That is the complete CloudNova CPQ story.
