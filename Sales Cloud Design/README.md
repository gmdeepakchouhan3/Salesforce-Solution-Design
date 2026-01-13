**Sales Cloud Design**
============================================================================

**Architecture Diagram**
--
![Architecture Diagram](https://github.com/gmdeepakchouhan3/SFDC-Solution-Design/blob/c3052a82c92b1b9b7c8fe8f919e8353cb8746e85/Sales%20Cloud%20Design/images/Sales%20Cloud%20Design.png)

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
![Role Hierarchy Diagram](https://github.com/gmdeepakchouhan3/SFDC-Solution-Design/blob/2a6f9252365777871e2a6fde948bce165986ed67/Sales%20Cloud%20Design/images/Sales%20Role%20Hierarchy-2.png)

#### Salesforce Configuration
![Salesforce Configuration](https://github.com/gmdeepakchouhan3/SFDC-Solution-Design/blob/2a6f9252365777871e2a6fde948bce165986ed67/Sales%20Cloud%20Design/images/SF%20Role%20Hierarchy.png)

**5\. Profiles and Permissions**
--------------------------------

Two main profiles are used:

*   **Standard User**
    
*   **Sales User**
    

Extra access is given using **Permission Sets**, for example:

*   Discount approval access
    
*   Bulk order approval access
    
*   Reports and dashboards access
    

This makes security simple and flexible.

**6\. Data Security and Visibility**
------------------------------------

Security is very important in this project.

*   **Opportunities** are private, so sales reps only see their own deals
    
*   **Role hierarchy** allows managers to see team data
    
*   **Territory management** is used to assign records based on country and region
    
*   **Sharing rules** are added only where extra access is needed
    

**7\. Lead Management**
-----------------------

Different lead types are created:

*   Wholesaler Leads
    
*   Retailer Leads
    
*   D2C Leads
    

Leads come from:

*   Website (Web-to-Lead) for D2C
    
*   Partners and APIs for B2B
    
*   Marketing campaigns
    

Leads are automatically assigned based on **country, market, and channel**. Once qualified, leads are converted into **Account, Contact, and Opportunity**.

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
