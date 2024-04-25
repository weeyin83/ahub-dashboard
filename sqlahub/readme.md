# SQL Azure Hybrid Benefit Queries

The dashboard is built using queries from [Azure Resource Graph](https://learn.microsoft.com/azure/governance/resource-graph/overview) queries.   You can interactive with the dashboard and see the queries within the Azure Portal, but I wanted to document them here for reference. 

# Table of contents

- [SQL Azure Hybrid Benefit List](#sql-azure-hybrid-benefit-list)

# SQL Azure Hybrid Benefit List

This query lists out all of your SQL virtual machines (VM) and displays the following information
- Virtual Machine Name
- License type - whether that is Pay as You Go (PAYG), Azure Hybrid Benefit (AHUB) or something else
- Image type - what flavour of Windows Server and SQL server is installed
- SQL SKU - whether you are running Standard, Enterprise or Web SQL

```bash
resources
| where type =~ 'Microsoft.SqlVirtualMachine/SqlVirtualMachines'
| extend license = properties.sqlServerLicenseType
| extend Image = properties.sqlImageOffer
| extend SQLSKU = properties.sqlImageSku
| project name, license, Image, SQLSKU
```

# SQL Azure Hyrbid Benefit Count

This query shows a count of how many SQL Servers have Azure Hybrid Benefit (AHUB) enabled for the SQL part of the install and how many do not.

```bash
resources
| where type =~ 'Microsoft.SqlVirtualMachine/SqlVirtualMachines'
| extend license = properties.sqlServerLicenseType
| extend Image = properties.sqlImageOffer
| extend SQLSKU = properties.sqlImageSku
| extend AHUB = iff((license in ("AHUB")), "Yes", "No")
| project name, license, Image, SQLSKU, AHUB
| summarize Count=count() by AHUB
```