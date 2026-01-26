**Sales Cloud Design**
============================================================================

**Sales Cloud Data Model**
--
![Sales Cloud Data Model](https://github.com/gmdeepakchouhan3/Salesforce-Solution-Design/blob/0949e6a0c792d089182c8099db2ca2ec258cb0fd/Sales%20Cloud%20Design/images/Salesforce%20Sales%20Cloud%20Data%20Model.png)

**1\. Project Overview**
------------------------

This project is about designing and setting up **Salesforce Sales Cloud** for a global electronics company. The company sells **Mobiles, Tablets, and Digital Watches** to different types of customers.

The business works in three ways:

*   Selling to **Wholesalers** (B2B)
    
*   Selling to **Retailers** (B2B)
    
*   Selling **Directly to Customers (D2C)**
    

The company operates in four main regions:

*   **EMEA** – Europe, Middle East, Africa (UK, Germany, UAE, South Africa)
    
*   **APAC** – Asia-Pacific (India, China, Japan, Australia)
    
*   **LATAM** – Latin America (Brazil, Mexico, Argentina, Chile)
    
*   **North America** – USA and Canada
    

The Salesforce solution is designed so that sales processes are the same across the world but still flexible for each country and sales channel.

**2\. Business Goals**
----------------------

The main goals of this project are:

*   Manage the **complete sales journey** in one system
    
*   Support **global sales teams** across multiple countries
    
*   Track **leads, opportunities, and revenue** easily
    
*   Provide **clear pipeline and forecast visibility** to management
    
*   Control **pricing, discounts, and bulk orders**
    
*   Give **role-based dashboards** to executives, managers, and sales reps
    

**3\. Salesforce Data Model**
-----------------------------

The solution uses mostly **Standard Salesforce objects**, which makes it stable and easy to maintain.

Main objects used:

*   **Leads** – New potential customers
    
*   **Accounts** – Wholesalers, Retailers, and End Customers
    
*   **Contacts** – People working in those accounts
    
*   **Opportunities** – Sales deals
    
*   **Products** – Mobiles, Tablets, Digital Watches
    
*   **Price Books** – Different prices for each region and channel
    
*   **Quotes and Orders** – For correct pricing and order processing
    

**4\. Users and Role Structure**
--------------------------------

Sales users are arranged in a clear hierarchy so data visibility is controlled.

Role flow:

*   **Market VP** – Top level for each region
    
*   **Country Manager** – Handles one country
    
*   **Channel Head** – Manages Wholesaler, Retailer, or D2C channel
    
*   **Sales Representative** – Works on leads and opportunities
    

Managers can see their team’s data, but sales reps can only see their own territory data.

#### Role Hierarchy Diagram
---
![Role Hierarchy Diagram](https://github.com/gmdeepakchouhan3/Salesforce-Solution-Design/blob/e465fa2bd85e604866c98663e1bbaafe2c61c2e6/Sales%20Cloud%20Design/images/Sales%20Role%20Hierarchy-2.png)

#### Salesforce Configuration
---
![Salesforce Configuration](https://github.com/gmdeepakchouhan3/Salesforce-Solution-Design/blob/e465fa2bd85e604866c98663e1bbaafe2c61c2e6/Sales%20Cloud%20Design/images/SF%20Role%20Hierarchy.png)

**5\. Profiles and Permissions**
--------------------------------

One main profiles are used:

*   **Sales User**
    

Extra access is given using **Permission Sets**, for example:

- Global Sales Head (Sales Core Access)
- Sales Market VP (Sales Core Access)
- Sales Country Manager (Sales Core Access)
- Retailer Sales Head
- Retailer Sales Representative
- Wholesaler Sales Head
- Wholesaler Sales Representative
- D2C Sales Head
- D2C Sales Representative
- Discount approval access
- Bulk order approval access
- Reports and dashboards access
    

This makes security simple and flexible.


#### Salesforce User Configuration
---
- **One Base Profile**

   * All sales users use a basic profile (Sales User – Base)
   * No approvals, no special pricing, no delete access

- **Permission Sets for Control**

   * Functional access is added using permission sets
   * Easy to audit and change without profile impact

- **Least Privilege Model**

   * Users get only what they need
   * Higher roles get broader visibility, not more edit power

#### Permission Set Matrix
---

| Permission Set          | Sales Rep | Channel Head | Country Manager | Market VP | Global Sales Head |
| ----------------------- | --------- | ------------ | --------------- | --------- | ----------------- |
| Sales_Core_Access       | ✅         | ✅            | ✅               | ✅         | ✅                 |
| Wholesaler_Access       | ✅*        | ✅            | ❌               | ❌         | ❌                 |
| Retailer_Access         | ✅*        | ✅            | ❌               | ❌         | ❌                 |
| D2C_Access              | ✅*        | ✅            | ❌               | ❌         | ❌                 |
| Discount_Approver_L1    | ❌         | ✅            | ❌               | ❌         | ❌                 |
| Discount_Approver_L2    | ❌         | ❌            | ✅               | ❌         | ❌                 |
| Discount_Approver_L3    | ❌         | ❌            | ❌               | ✅         | ❌                 |
| Discount_Approver_L4    | ❌         | ❌            | ❌               | ❌         | ✅                 |
| Bulk_Order_Approval     | ❌         | ✅            | ✅               | ❌         | ❌                 |
| Team_Report_Access      | ❌         | ✅            | ❌               | ❌         | ❌                 |
| Country_Report_Access   | ❌         | ❌            | ✅               | ❌         | ❌                 |
| Regional_Report_Access  | ❌         | ❌            | ❌               | ✅         | ❌                 |
| Executive_Report_Access | ❌         | ❌            | ❌               | ❌         | ✅                 |
| Forecast_User           | ❌         | ❌            | ✅               | ❌         | ❌                 |
| Forecast_Manager        | ❌         | ❌            | ❌               | ✅         | ❌                 |
| Forecast_Admin          | ❌         | ❌            | ❌               | ❌         | ✅                 |

- Assigned based on the user’s sales channel

#### Permission Set Descriptions
---
- Sales_Core_Access

Assigned to **all sales users**.

* Create/Edit Leads and Opportunities
* Add Products to Opportunities
* Log Tasks and Activities


#### Channel Access Permission Sets
---
Wholesaler_Access / Retailer_Access / D2C_Access

* Access to channel-specific record types
* Visibility to relevant price books
* Channel-specific sales stages

A sales rep gets **only one channel permission set**.


#### Discount Approval Permission Sets
---
| Permission Set       | Role              |
| -------------------- | ----------------- |
| Discount_Approver_L1 | Channel Head      |
| Discount_Approver_L2 | Country Manager   |
| Discount_Approver_L3 | Market VP         |
| Discount_Approver_L4 | Global Sales Head |

Includes:

* Approve / Reject actions
* Approval work item visibility
* Read-only pricing fields

#### Reporting Permission Sets
---

* **Team_Report_Access** – Channel-level dashboards
* **Country_Report_Access** – Country-level dashboards
* **Regional_Report_Access** – Region-level dashboards
* **Executive_Report_Access** – Global dashboards


#### Forecast Permission Sets
---

* **Forecast_User** – Submit forecast
* **Forecast_Manager** – Adjust team forecast
* **Forecast_Admin** – Global forecast control

---

### Real-Life Example:
#### India Wholesaler Sales Rep

* Profile: Sales User – Base
* Permission Sets:

  * Sales_Core_Access
  * Wholesaler_Access

Result: Can work on wholesaler deals in India only.


#### India Country Manager
---
* Permission Sets:

  * Sales_Core_Access
  * Discount_Approver_L2
  * Country_Report_Access
  * Forecast_User

Result: Can approve discounts and see all India sales data.


#### Benefits of This Approach
---
* No profile explosion
* Easy onboarding and offboarding
* Strong security and compliance
* Easy audits and access reviews
* Salesforce-recommended best practice

#### Object-Level Access Matrix
---
This section defines **which Salesforce objects each role can access** and what level of access is provided. Profiles remain minimal, and access is granted using Permission Sets.

#### Object-Level Access Table

| Salesforce Object | Sales Rep | Channel Head | Country Manager | Market VP | Global Sales Head |
| --- | --- | --- | --- | --- | --- |
| Lead | C, R, E | C, R, E | C, R, E | R | R |
| Account | R | R, E | R, E | R | R |
| Contact | R | R, E | R, E | R | R |
| Opportunity | C, R, E | C, R, E | C, R, E | R | R |
| Opportunity Product | C, R, E | C, R, E | R | R | R |
| Quote | C, R | C, R, E | R | R | R |
| Order | R | R | R | R | R |
| Campaign Member | R | R | R | R | R |
| Task / Event | C, R, E | C, R, E | C, R, E | R | R |
| Report | R (Own) | R (Team) | R (Country) | R (Region) | R (Global) |
| Approval Requests | ❌ | Approve | Approve | Approve | Approve |

**C: Create, R: Read, E: Edit**
- No Delete access for business users (best practice)
- Assign related object page layouts/Flexipage to the New Sales Profile

#### Real-Life Example:

A Sales Rep can:
- Create leads & opportunities    
- But **cannot delete opportunities** or modify pricing after approval


#### Field-Level Security (FLS) Matrix
---

Field-level security ensures **sensitive data is visible only to the right roles**, even when users can access the same record.

#### Key Opportunity Fields

| Field Name         | Sales Rep  | Channel Head | Country Manager | Market VP | CSO  |
| ------------------ | ---------- | ------------ | --------------- | --------- | ---- |
| Opportunity Amount | E       | E         | E            | R      | R |
| Discount %         | E (≤7%) | E         | E            | R      | R |
| Margin %           | ❌       | R         | E            | R      | R |
| Stage              | E       | E         | E            | R      | R |
| Forecast Category  | R       | E         | E            | E      | E |
| Close Date         | E       | E         | E            | R      | R |

**R: Read, E: Edit**
#### Real-Life Example:

A **Sales Rep** can enter discounts up to 7%, but **cannot see margin percentage**. The **Channel Head** can view margins before approving discounts.


#### Product & Pricing Fields
---

This section explains access to **product catalog and pricing-related fields**, critical for multi-country and multi-currency sales.


#### Product Object – Key Fields

| Field Name     | Sales Rep | Channel Head | Country Manager | Market VP | CSO  |
| -------------- | --------- | ------------ | --------------- | --------- | ---- |
| Product Name   | R      | R         | R            | R      | R |
| Product Family | R      | R         | R            | R      | R |
| Cost Price     | ❌      | ❌         | R            | R      | R |
| Active         | R      | R         | E            | E      | E |

**R: Read, E: Edit, H: Hidden**

#### Price Book Entry Fields

| Field Name       | Sales Rep | Channel Head | Country Manager | Market VP | CSO  |
| ---------------- | --------- | ------------ | --------------- | --------- | ---- |
| List Price       | R      | R         | R            | R      | R |
| Discounted Price | R      | R         | E            | E      | E |
| Currency         | R      | R         | R            | R      | R |
| Volume Tier      | R      | R         | E            | E      | E |

**R: Read, E: Edit**

#### Real-Life Example:

For **EMEA Wholesaler Price Book**, a **Sales Rep** can view prices but cannot change them. The **Country Manager (Germany)** can update bulk pricing tiers for local market needs.


#### Best Practices Followed
---

* Minimal profiles, access via Permission Sets
* Sensitive financial fields protected using FLS
* Price governance maintained at manager levels
* Scalable model for adding new regions or channels


**6\. Data Security and Visibility**
------------------------------------


Security is a critical requirement in this Salesforce Sales Cloud implementation. The design ensures that users can access **only the data they are authorized to see**, based on role, region, and responsibility. The model follows Salesforce best practices using **OWD, Role Hierarchy, Territory Management, Sharing Rules, and Permission Sets**.


#### Organization-Wide Defaults (OWD)
---
OWD defines the base level of access for all users.

#### OWD Configuration

| Object        | OWD Setting          | Reason                              |
| ------------- | -------------------- | ----------------------------------- |
| Opportunities | Private              | Sales reps see only their own deals |
| Accounts      | Private              | Access controlled by territory      |
| Contacts      | Controlled by Parent | Follows Account visibility          |
| Leads         | Private              | No cross-rep visibility             |
| Campaign      | Private              | Sales rep drives immediate revenue via high-intensity, targeted action               |
| Campaign Member | Controlled by Parent | Follows Campaign visiblity               |
| Quotes        | Private              | Pricing is sensitive                |
| Orders        | Private              | Financial data protection           |

#### Real-Life Example:

An **India Sales Rep** can only see opportunities they own. A **Germany Sales Rep** cannot see India deals at all.


#### Role Hierarchy (Manager Visibility)
---
Role hierarchy is used for **upward visibility only**. Managers automatically see records owned by their team members.

#### Role Structure

```
Global Sales Head
 └── Market VP
      └── Country Manager
           └── Channel Head
                └── Sales Representative
```

#### Key Setting

* Grant Access Using Hierarchies = Enabled

#### Real-Life Example:

When a Sales Rep creates an opportunity, the Channel Head, Country Manager, and Market VP can see it automatically.

#### Territory Management (Country-Based) – Salesforce Setup
---
**Enterprise Territory Management (ETM)** is implemented in Salesforce to control **country and market wise data visibility**. Territories decide **which records users can see**, while roles decide **who reports to whom**.

This setup ensures:

* No cross-country data leakage
* Clear market (APAC / EMEA / LATAM / NA) visibility
* Clean forecasting and reporting


#### Salesforce - Territory Settings
---
![Territory Settings](https://github.com/gmdeepakchouhan3/Salesforce-Solution-Design/blob/e465fa2bd85e604866c98663e1bbaafe2c61c2e6/Sales%20Cloud%20Design/images/Territory%20Settings.png)

#### Territory Types with Priority (Very Important)
---

Territory Types define **level + priority**. Priority decides which territory wins when an Account matches multiple territories.

#### Priority Order (High → Low)

| Priority    | Territory Type     | Purpose                    |
| ----------- | ------------------ | -------------------------- |
| 1 (Highest) | Country Territory  | Actual selling & ownership |
| 2           | Regional Territory | Regional visibility        |
| 3 (Lowest)  | Global Territory   | Executive reporting        |

#### Real-life Example

Account Country = India, Region = APAC

Matches:
- India (Country)
- APAC (Region)

India territory wins because **Country has higher priority**.

![Territory Types](https://github.com/gmdeepakchouhan3/Salesforce-Solution-Design/blob/ad73a0de9e244b9ee92f6f48d0d91dc44fd08987/Sales%20Cloud%20Design/images/Territory%20Types.png)

#### Territory Model Structure (Market → Country)
---
```
Global
 ├── APAC
 │    └── India
 ├── EMEA
 │    └── Germany
 ├── LATAM
 │    └── Brazil
 └── North America
      └── USA
```

* Market = Region level
* Country = Selling territory

#### Create Territory Model
----
```
Setup → Territory Management → Territory Models
→ New Territory Model
```

| Field | Value                        |
| ----- | ---------------------------- |
| Name  | Global Sales Territory Model |
| State | Draft                        |


#### Create Territories
---
| Territory Name | Parent Territory |
| -------------- | ---------------- |
| Global         | —                |
| APAC           | Global           |
| EMEA           | Global           |
| NA             | Global           |
| India          | APAC             |
| Germany        | EMEA             |
| USA            | NA               |

![Territory Model](https://github.com/gmdeepakchouhan3/Salesforce-Solution-Design/blob/ad73a0de9e244b9ee92f6f48d0d91dc44fd08987/Sales%20Cloud%20Design/images/Territory%20Model.png)

![Territory-India](https://github.com/gmdeepakchouhan3/Salesforce-Solution-Design/blob/ad73a0de9e244b9ee92f6f48d0d91dc44fd08987/Sales%20Cloud%20Design/images/Territory-India.png)

#### Territory Assignment Rules (Country-Based)
---
Territories are assigned using **Account country fields**.

#### Account Field Used

* Billing Country (Standard)

#### Example: Rules

**India Territory**

```
If BillingCountry = 'India'
→ Assign to India Territory
```

**Germany Territory**

```
If BillingCountry = 'Germany'
→ Assign to Germany Territory
```

**USA Territory**

```
If BillingCountry = 'United States'
→ Assign to USA Territory
```

Accounts are auto-assigned on create or edit.

![Territory Assignment Rule](https://github.com/gmdeepakchouhan3/Salesforce-Solution-Design/blob/ad73a0de9e244b9ee92f6f48d0d91dc44fd08987/Sales%20Cloud%20Design/images/Territory%20Assignment%20Rule.png)

![Territory Accounts](https://github.com/gmdeepakchouhan3/Salesforce-Solution-Design/blob/ad73a0de9e244b9ee92f6f48d0d91dc44fd08987/Sales%20Cloud%20Design/images/Territory%20Accounts.png)

#### Assign Users to Territories
---
Users are assigned to territories with **territory roles**.

#### Territory Roles Used

* Sales Rep
* Manager
* Executive

#### Example: India Territory

| User              | Salesforce Role | Territory | Territory Role  |
| ----------------- | --------------- | --------- | --------------- |
| India Sales Rep   | Sales Rep       | India     | Sales Rep       |
| Channel Head      | Channel Head    | India     | Manager         |
| Country Manager   | Country Manager | India     | Territory Owner |
| APAC Market VP    | Market VP       | APAC      | Executive       |
| Global Sales Head | CSO             | Global    | Executive       |


#### How Territory and Role Hierarchy Work Together
---

| Component            | Purpose               |
| -------------------- | --------------------- |
| Role Hierarchy       | Manager visibility    |
| Territory Management | Geographic visibility |
| OWD (Private)        | Base security         |
| Permission Sets      | Functional access     |


#### Reports and Forecasting
---

* Pipeline by Country
* Revenue by Market
* Territory-based forecasts

Forecast roll-up:

```
Sales Rep → Country Manager → Market VP → Global Head
```

#### Activation Checklist
---
Before activation:

* Users assigned to territories
* Territory rules tested
* Sample accounts validated

#### Activate Model
```
Territory Models → Activate
```

#### Benefits
---
* Clear country ownership
* Market-level visibility
* No manual sharing rules
* Scalable for new countries

This territory setup uses **market-to-country hierarchy** with automatic account assignment based on billing country. It ensures secure data access, clean reporting, and scalable global sales operations.

#### Opportunity Access via Territory
---
Opportunity access follows the Account territory.

#### Salesforce Setting

* Enable Opportunity Access Using Territories

#### Result

Opportunities created under an India Account are visible only to India territory users and above.


#### Sharing Rules (Exceptions Only)

Sharing rules are used **only when extra access is required**.

#### Example 1: Presales Access

* Object: Opportunity
* Shared With: Presales Public Group
* Access Level: Read Only

#### Example 2: Finance Access

* Object: Opportunities, Orders
* Shared With: Finance Group
* Access Level: Read Only

#### Real-Life Example:

Finance can review revenue but cannot edit deals or pricing.


#### Profiles and Permission Sets
---
#### Profiles

* Minimal access
* No sensitive permissions
* Same profile across regions

#### Permission Sets

Used to control:

* Discount approvals
* Margin visibility
* Forecast access
* Advanced reports

Security is **permission-set driven**, not profile-driven.


#### End-to-End Security Flow
---
```
OWD (Private)
   ↓
Role Hierarchy
   ↓
Territory Management
   ↓
Sharing Rules (Exceptions)
   ↓
Permission Sets
```

#### Security Testing Scenarios
---
#### Scenario 1: Sales Rep

* Sees only own opportunities
* Cannot see margin

#### Scenario 2: Country Manager

* Sees all country opportunities
* Can approve discounts

#### Scenario 3: Market VP

* Read-only access
* Full regional visibility

#### Benefits
---
* Strong data security
* No cross-country data leakage
* Audit-friendly access model
* Scalable for new regions

This security model ensures **data protection, correct visibility, and scalability** by combining Private OWD, role hierarchy, territory management, controlled sharing rules, and permission sets.

    

**7\. Lead Management**
-----------------------

Lead Management in this Salesforce Sales Cloud solution is designed to handle **different lead types across regions and countries**, ensuring the right sales team receives the right lead automatically.

Lead flow supports:

* B2B (Wholesalers & Retailers)
    
* B2C (Direct-to-Consumer)
    
* Global markets with country-level ownership

#### Lead Process
---
A **standard Lead Process** is defined with **channel flexibility**, so all teams follow the same lifecycle while capturing channel specific details.

#### Lead Status Values

| Lead Status            |
| -----------------------|
| Open - Not Contacted   |
| Working - Contacted    |
| Closed - Converted     |
| Closed - Not Converted |


At present, default lead statuses are in use. These can be customized by defining separate Lead Processes for B2B and D2C

![Lead Process](https://github.com/gmdeepakchouhan3/Salesforce-Solution-Design/blob/fee8b47027f6beae9e3fa86321e79b0159382ccb/Sales%20Cloud%20Design/images/Lead%20Process.png)

#### Lead Types (Record Types)
---

Separate Lead Record Types are created to manage different sales channels.

| Lead Type          | Record Type        | Used For                 |
| -------------------|--------------------|--------------------------|
| Wholesaler         |	Wholesaler        |	Bulk & partner sales    |
| Retailer           |	Retailer          |	Store / franchise sales |
| Direct-to-Consumer | Direct-to-Consumer |	Direct online customers |

Why Record Types?

* Different page layouts

* Different qualification fields

* Channel specific validation rules

![Lead Types](https://github.com/gmdeepakchouhan3/Salesforce-Solution-Design/blob/fee8b47027f6beae9e3fa86321e79b0159382ccb/Sales%20Cloud%20Design/images/Lead%20Record%20Type.png)

**8\. Product and Pricing Setup**
---------------------------------

Products are grouped into families:

*   Mobiles
    
*   Tablets
    
*   Digital Watches
    

Different **Price Books** are created for each region and channel, for example:

*   EMEA Wholesaler Price Book
    
*   APAC Retailer Price Book
    
*   NA D2C Price Book
    

Multi-currency is enabled so prices are correct for each country.Special pricing is handled for **bulk orders and volume discounts**.

**9\. Opportunity and Sales Process**
-------------------------------------

The standard sales process is: **Lead → Opportunity → Quote → Negotiation → Closed Won → Order**

Some stages are different for each channel:

*   Wholesalers – Partner onboarding, contract finalisation
    
*   Retailers – Store rollout planning
    
*   D2C – Checkout and payment
    

All opportunities are used for **pipeline tracking and forecasting**.

**10\. Approval Processes**
---------------------------

To control discounts and big deals, approvals are added.

*   **Discount more than 7%** needs approval
    
*   **Bulk orders** go through multiple approvals
    

Approval flow: Sales Rep → Channel Head → Country Manager → Market VP

After final approval, the opportunity can move to the next stage.

**11\. Reports and Analytics**
------------------------------

Important reports include:

*   Pipeline by region, country, and stage
    
*   Revenue by channel and product
    
*   Sales comparison between B2B and D2C
    
*   Lead conversion by market
    
*   Sales rep activity and performance
    
*   Aging leads and opportunities
    
*   Discount and bulk order analysis
    
*   Approval cycle time reports
    

**12\. Dashboards**
-------------------

#### Executive Dashboards

*   Total sales vs target
    
*   Pipeline by stage
    
*   Sales by region and country
    
*   Top customers
    

#### Manager Dashboards

*   Team pipeline and activities
    
*   Win rate by sales rep
    
*   Discount usage
    

#### Sales Rep Dashboards

*   My open opportunities
    
*   My tasks and follow-ups
    
*   My quota vs achievement
    
*   Recent wins
    

**13\. Conclusion**
-------------------

This Salesforce Sales Cloud solution gives the company a **single, clear system** to manage global sales. It supports different sales channels, keeps data secure, controls discounts, and provides powerful reports and dashboards. The design is scalable, easy to maintain, and suitable for long-term business growth.
