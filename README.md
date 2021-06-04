# dbt
dbt personal documentation
abridged introduction cut down from the dbt dev recommended structure at:
https://discourse.getdbt.com/t/how-we-structure-our-dbt-projects/355
__________________
#DBT data has three distinct checkpoints: 

Sources: Schemas and tables in a source-conformed structure 
(i.e. tables and columns in a structure based on what an API 
returns), loaded by a third party tool. (src)

Staging models: The atomic unit of data modeling. Each model bears 
a one-to-one relationship with the source data table it represents. 
It has the same granularity, but the columns have been renamed, 
recast, or usefully reconsidered into a consistent format. (stg)

Marts models: Models that represent business processes and entities, 
abstracted from the data sources that they are based on. (marts)

Of note here is that there is a distinct change that occurs between 
the staging and marts checkpoints – sources and staging models 
are source-centric, whereas marts models are business-centric.

# Example: 

Sources: Payment records from the Stripe API and payment records 
from the Braintree API, loaded into their data warehouse by 
a third party tool.

Staging models: Both the Stripe and Braintree payments are recast 
into a consistent shape, with consistent column names.

Marts models: A monthly recurring revenue (MRR) model that classifies 
revenue per customer per month as new revenue, upgrades, downgrades, 
and churn, to understand how a business is performing over time. 
It may be useful to note whether the revenue was collected via Stripe 
or Braintree, but they are not fundamentally separate models.
_____________________

The goal of the staging layer is to create staging models. Staging 
models take raw data, and clean and prepare them for further analysis. 
For a user querying the data warehouse, a relation with a stg_ prefix 
indicates that:

Fields have been renamed and recast in a consistent way.
Datatypes, such as timezones, are consistent.
Light cleansing, such as replacing empty string with NULL values, has 
occurred.
If useful, flattening of objects might have occurred.
There is a primary key that is both unique and not null (and tested).


Fact and Dimension tables: 

fct_<verb>: A tall, narrow table representing real-world processes 
  that have occurred or are occurring. The heart of these models 
  is usually an immutable event stream: sessions, transactions, 
  orders, stories, votes.

dim_<noun>: A wide, short table where each row is a person, place,
or thing; the ultimate source of truth when identifying and describing 
entities of the organization. They are mutable, though slowly changing: 
customers, products, candidates, buildings, employees.

Where the work of staging models is limited to cleaning and preparing, 
fact tables are the product of substantive data transformation: choosing 
(and reducing) dimensions, date-spining, executing business logic, 
and making informed, confident decisions.








Recommended reading for more depth:
https://discourse.getdbt.com/t/how-we-structure-our-dbt-projects/355

