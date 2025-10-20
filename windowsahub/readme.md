# Windows Azure Hybrid Benefit Queries

The dashboard is built using queries from [Azure Resource Graph](https://learn.microsoft.com/azure/governance/resource-graph/overview) queries.   You can interactive with the dashboard and see the queries within the Azure Portal, but I wanted to document them here for reference. 

# Table of contents

- [Windows Server Azure Hybrid Benefit List](#windows-server-azure-hybrid-benefit-list)
- [Windows Server Azure Hybrid Benefit Count](#windows-server-azure-hybrid-benefit-count)

# Windows Server Azure Hybrid Benefit List

This query lists out all of your Windows Server virtual machines (VM) and displays the following information
- Virtual Machine Name
- Location - the Azure region the VM is located in
- vmSize - the Azure VM SKU being used
- AHUB - whether Azure Hybrid Benefit (AHUB) is enabled or not for the VM

```bash
resources 
| where type =~ 'Microsoft.Compute/virtualMachines'
| extend licenseType = tostring(properties.['licenseType'])
| extend vmSize = tostring(properties.hardwareProfile['vmSize'])
| extend AHUB = iff((licenseType in ("Windows_Server")), "Yes", "No")
| project name, location, vmSize, AHUB
| order by ['AHUB'] asc
```

# Windows Server Azure Hybrid Benefit Count

This query shows a count of how many Windows Servers have Azure Hybrid Benefit (AHUB) enabled and how many do not.

```bash
resources 
| where type =~ 'Microsoft.Compute/virtualMachines'
| extend licenseType = tostring(properties.['licenseType'])
| extend vmSize = tostring(properties.hardwareProfile['vmSize'])
| extend AHUB = iff((licenseType in ("Windows_Server")), "Yes", "No")
| project name, location, vmSize, AHUB
| summarize Count=count() by AHUB
```

# Windows Server Azure Hybrid Benefit List v2

This query lists out all of your Windows Server virtual machines (VM) and displays the following information
- Virtual Machine Name
- Location - the Azure region the VM is located in
- vmSize - the Azure VM SKU being used
- AHUB - whether Azure Hybrid Benefit (AHUB) is enabled or not for the VM
- licenseType - 
- publisher - Who published the image such as Canonical, Microsoft Windows Server etc. 
- SKU - What the SKU is such as 2016-Datacentre, Enterprise etc
- Offer - Generic explaination such as Windows Server or Ubuntu

```bash
resources
| where type =~ 'Microsoft.Compute/virtualMachines'
| extend publisher = tostring(properties.storageProfile.imageReference.publisher)
| extend SKU = tostring(properties.storageProfile.imageReference.sku)
| extend offer = tostring(properties.storageProfile.imageReference.offer)
| extend licenseType = tostring(properties.['licenseType'])
| extend vmSize = tostring(properties.hardwareProfile['vmSize'])
| extend AHUB = iff((licenseType in ("Windows_Server")), "Yes", "No")
| project name, location, vmSize, AHUB, licenseType, publisher, SKU, offer
```
