Salesforce CPQ — Easy Memory Notes

37 Topics at a Glance


Memory story: CloudNova sells CRM to ABC Technologies.



#	Topic	Remember It As	Example
1	CPQ	Configure + Price + Quote	Build ABC's CRM quote
2	Account	Who is the customer?	ABC Technologies
3	Opportunity	Potential deal	₹10L CRM deal
4	Product	What are we selling?	CRM Enterprise
5	Price Book	Product + Price list	₹1,000/user/month
6	Quote	What are we offering?	100 users + support
7	Quote Line	One item on quote	CRM — 100 users
8	QLE	CPQ shopping cart	Add/configure products
9	Bundle	Package	CRM Enterprise Package
10	Product Feature	Group inside bundle	Support
11	Product Option	Child item	Premium Support
12	Option Constraint	Compatibility	Basic + Premium not together
13	Configuration Attribute	Input during configuration	Users = 100
14	Product Rule	Product/configuration logic	Enterprise requires Support
15	Pricing Waterfall	How final price is reached	List → discounts → net
16	Discount Schedule	Volume tiers	100+ users = 15%
17	Block Pricing	Fixed price per quantity block	1–100 = ₹50K
18	Percent of Total	Price based on total	Implementation = 10%
19	Contracted Price	Customer-specific price	ABC gets ₹800
20	Price Rule	Custom pricing logic	IF ABC → special price
21	Price Condition	IF	Customer = ABC
22	Price Action	THEN	Set price = ₹800
23	Lookup Query	Find a value	Look up ABC price
24	Summary Variable	Aggregate quote data	Total users = 500
25	Subscription Product	Recurring product	CRM monthly
26	Proration	Partial-period charge	Mid-period start
27	MDQ	Different values by time	Y1 100, Y2 150
28	Quote Template	Customer-facing document	Quote PDF
29	Approval	Permission before proceeding	>20% discount
30	Order	Accepted purchase	ABC buys 100 users
31	Contract	Formal agreement	12-month agreement
32	Subscription	Recurring purchase record	100 users for 12 months
33	Amendment	Change existing contract	100 → 150 users
34	Renewal	Continue after expiry	Next 12 months
35	QCP	Custom JavaScript calculation	Complex custom logic
36	Integrations	Connect other systems	CPQ → ERP/Billing
37	Complete Flow	End-to-end CPQ	Account → Renewal

Super-Short Memory Map

WHO?

Account = customer


DEAL?

Opportunity = potential sale


WHAT?

Product = item/service


HOW MUCH?

Price Book = standard price
Discount Schedule = volume discount
Block Pricing = block price
Percent of Total = percentage price
Contracted Price = customer-specific price
Price Rule = custom pricing logic


HOW TO BUILD?

Bundle = package
Feature = group
Option = child product
Constraint = compatibility
Configuration Attribute = input
Product Rule = configuration logic


QUOTE?

Quote = proposal
Quote Line = individual item
QLE = configure and price screen
Quote Template = final document


RECURRING?

Subscription Product = recurring product
Proration = partial period
MDQ = time-based segments


AFTER SALE?

Order = accepted purchase
Contract = agreement
Subscription = recurring commitment
Amendment = change
Renewal = extend


CUSTOM / EXTERNAL?

QCP = custom JavaScript
Integration = external system connection


Most Important Relationships

Account
   ↓
Opportunity
   ↓
Quote
   ↓
Quote Lines
   ↓
Products / Bundles
   ↓
Product Rules
   ↓
Pricing
   ↓
Price Rules
   ↓
Approval
   ↓
Quote Template
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

Three Easy Rules to Remember

Product Rule = WHAT can/cannot be configured


Price Rule = HOW the price should be changed


Option Constraint = Simple product compatibility


QCP = Use custom JavaScript when standard CPQ configuration is not enough


