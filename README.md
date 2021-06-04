# dbt
dbt personal documentation
------------
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

Example: 

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
----------
