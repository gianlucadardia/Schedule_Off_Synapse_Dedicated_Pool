## Azure Synapse - Schedule Dedicated Pool Pause

Many customer has cost concern related to **Synapse Analytics Dedicated Pool** usage. 
Especially in product evaluation phase, customer needs to keep cost under strict control

Capabilities to pause dedicated pool, could help to mitigate this concern, but the lack of **"Native"** way to perform this task, could be an entry barrier.

This 1-click deployment, try to help, allowing user to deploy a Logic App that can **Pause Synapse Dedicated Pool** on scheduled basis.

## Prerequisites

Owner role (or Contributor roles) for the Azure Subscription the template being deployed in. 

## Deployment Steps

1. Click 'Deploy To Azure' button given below to deploy all the resources.

[![Deploy to Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fgianlucadardia%2FSchedule_Off_Synapse_Dedicated_Pool%2Fmain%2Fazuredeploy.json)

   - Provide the values for:

     - Resource group (create new)**
     - Logic App name
     - Dedicated Pool name (ones you want to turn off)
     - Synapse Workspace resource group
     - Synapse Workspace name
     - Frequency
     - Time Zone
     - Pause Time   
     
   - Click 'Review + Create'.
   - On successful validation, click 'Create'.

** **Currently resource group need to be the same of the Synapse workspace ones**

![Deployment-1](https://github.com/gianlucadardia/Schedule_Off_Synapse_Dedicated_Pool/raw/main/images/deployment01.jpg)

## Azure Services being deployed
This template deploys necessary resources to run a scheduled Logic App, to Pause Synaps Dedicated Pool, specified at configuration phase

Following resources are deployed with this template along with some RBAC role assignments:

- A **Logic App** to Pause the SQL Dedicate Pool at defined schedule
- Assign **contributor role** to Logic App Managed Identity

## Post Deployment
- After the deployment is complete, click 'Go to resource group'.
- You'll see Logic App deployed in the resource group.


## Technical details

### Behavior
Logic App perform following steps:
- Inititalize variables needed to launch commands
- Retrieve dedicated pool state
- If it's **Paused**, nothing happens
- If it's **Online**, Logic App wait until there are no running queries and then **Pause** the pool

![Details-1](https://github.com/gianlucadardia/Schedule_Off_Synapse_Dedicated_Pool/raw/main/images/techdetails01.jpg)


### Limitation
- Logic App need to be deployed in the same resource group of Synpase Workspace

## Enhancement

Once Logic App is deployed, you can further customize behavior, adding any kind of step, leveraging its large number of connectors

e.g.
- Send email notification
- Trigger specific Workflow
- Starting DataOps pipeline
- .........