# Billing Exports To `BigQuery`

The first step to analysis costs is to export billing data into `BigQuery`, do as the following:

https://cloud.google.com/billing/docs/how-to/export-data-bigquery

Some examples of `SQL` statements follows.

`````sql
-- Finding costs
SELECT * FROM `billing_dataset.enterprise_billing` WHERE Cost > 0

-- Finding Billing Services
SELECT Line_Item, COUNT(*) as NUM FROM `billing_dataset.enterprise_billing` GROUP BY Line_Item

-- or
SELECT Project_ID, COUNT(*) as num FROM `billing_dataset.enterprise_billing` GROUP BY Project_ID

-- or
SELECT Project_ID, COUNT(*) as num FROM `billing_dataset.enterprise_billing` GROUP BY Project_ID

--or
SELECT SUM(cost) as Cost, Project_Name FROM `billing_dataset.enterprise_billing` GROUP BY Project_Name

-- Finding services types
SELECT service.description FROM `ctg-storage.bigquery_billing_export.gcp_billing_export_v1_01150A_B8F62B_47D999` GROUP BY service.description

-- Finding the geolocation where the bill happens
SELECT location.region, COUNT(*) AS num FROM `ctg-storage.bigquery_billing_export.gcp_billing_export_v1_01150A_B8F62B_47D999` GROUP BY location.region
`````

## Terminologies

* Billing Accounts
  * Billing Accounts Owners/Users/Viewers
* Organization
* Payment Profiles



## Reference

* Understanding Your GCP Costs https://www.qwiklabs.com/quests/90?parent=catalog
* BigQuery: Qwik Start - Command Line https://google.qwiklabs.com/focuses/577?parent=catalog