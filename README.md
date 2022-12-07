## Azure Synapse - Schedule Dedicated Pool OFF 

Many customer are worried about cost to incur using Synapse Analytics dedicated pool. 
Especially during product evaluation, customer wants to afford "least cost as possible"

The capabilities to pause dedicated pool, really hep to achieve this aim,
but the lack of "integrated" way to perform it, has a bittersweet taste.

This 1-click deployment, allows user to deploy a Logic App to enable creation of Logic app to schedule "Turn off Synapse dedicated pool" wherever  dedicated pool is.

## Prerequisites

Owner role (or Contributor roles) for the Azure Subscription the template being deployed in. 

## Deployment Steps

1. Click 'Deploy To Azure' button given below to deploy all the resources.

[![Deploy to Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fgianlucadardia%2FSchedule_Off_Synapse_Dedicated_Pool%2Fmain%2Fazuredeploy.json)

   - Provide the values for:

     - Resource group (create new)**
     - Logic App name
     - Dedicated pool name (ones you want to turn off)
     - Synapse workspace resource group
     - Synapse Workspace name
     - Frequency
     - Time Zone
     - Pause Time   
     
   - Click 'Review + Create'.
   - On successful validation, click 'Create'.

** **Currently resource group need to be the same of the Synapse workspace ones**

![Deployment-1](https://github.com/gianlucadardia/Schedule_Off_Synapse_Dedicated_Pool/raw/main/images/deployment01.jpg)

## Azure Services being deployed
This template deploys necessary resources to run a scheduled Logic App, to Pause Synaps Dedicated Pool, specified on configuration phase

Following resources are deployed with this template along with some RBAC role assignments:

- A Logic App to Pause the SQL Pool at defined schedule
- Assign contributor role to Logic App Managed Identity

## Post Deployment
- After the deployment is complete, click 'Go to resource group'.
- You'll see Logic App deployed in the resource group.


## Technical details

### Behavior
Logic app, in order to puase dedicated pool, on scheduled basis perform following steps:
- Inititalize variables needed to launch commands
- Retrieve dedicated pool state
- If pool is paused, nothing happens
- If pool is Online, logi app wait until there are no running queries and turn off the pool

![Details-1](https://github.com/gianlucadardia/Schedule_Off_Synapse_Dedicated_Pool/raw/main/images/techdetails01.jpg)


### Limitation
- Currently Logic App need to be deployed in the same resource group of synpase workspace