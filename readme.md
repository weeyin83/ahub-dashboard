# Azure Hybrid Benefit Dashboard

This dashboard 




If you'd like to see what [Azure Resource Graph](https://learn.microsoft.com/azure/governance/resource-graph/overview) queries are used to create this dashboard. You can find the Windows queries [here](/windowsahub/windowsahubqueries.md) and the SQL queries are [here](sqlahub/sqlahubqueries.md).


# How to Enable Azure Dashboard for Arc Windows/Linux
This article will show you how to use the [.json](json) file to create a custom dashboard in the [Azure portal](https://learn.microsoft.com/azure/azure-portal/azure-portal-dashboards).



### Steps to Follow

1. Log in to [Azure Portal](https://portal.azure.com/)
2. Click on **Dashboard** from the Azure Portal menu. You may already see the dashboard view by default.
![](https://learn.microsoft.com/azure/azure-portal/media/azure-portal-dashboards/portal-menu-dashboard.png)
3. Click on **Create**
   <p><img width="521" alt="create" src="https://github.com/weeyin83/Azure-Arc-Windows-Linux-Dashboard/assets/13692824/a99bc4f5-9b2a-4bec-94ca-014d145cbde4"></p>
4. Select **Custom** Dashboard
   <p><img width="618" alt="custom" src="https://github.com/weeyin83/Azure-Arc-Windows-Linux-Dashboard/assets/13692824/c155d39f-0311-4e28-b21b-3b6f16216950"></p>
5. You will be prompted to customise the new dashboard, click on **cancel**
   <p><img width="405" alt="cancel" src="https://github.com/weeyin83/Azure-Arc-Windows-Linux-Dashboard/assets/13692824/247550e0-e749-4c8c-983f-49b6f031752a"></p>
6. Now select **Upload** and upload the [.json](Azure-Arc-Windows-Linux-Dashboard.json) file
   <p><img width="517" alt="upload" src="https://github.com/weeyin83/Azure-Arc-Windows-Linux-Dashboard/assets/13692824/559006e6-ce32-4c9b-82cc-be52aade8c26"></p>
7. If you want to edit the dashboard, please refer to this [link](https://learn.microsoft.com/azure/azure-portal/azure-portal-dashboards#edit-a-dashboard).

<a name=disclaimers></a>

## Disclaimers
The code included in this sample is not intended to be a set of best practices on how to build scalable enterprise grade applications. This is beyond the scope of this quick start sample.
