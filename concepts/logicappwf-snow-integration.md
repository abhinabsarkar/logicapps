# Logic Apps - ServiceNow integration with Azure Defender for Cloud

## Pre-requisites
* [Azure subscription access](https://azure.microsoft.com/en-us/)
* [Service Now access](https://developer.servicenow.com/dev.do)
* Basic understanding of the following:
    * [Logic Apps](https://docs.microsoft.com/en-us/azure/logic-apps/logic-apps-overview) 
    * [Microsoft Defender for Cloud (formerly known as Azure Security Center)](https://docs.microsoft.com/en-us/azure/defender-for-cloud/defender-for-cloud-introduction)
    * [Service-Now](https://www.servicenow.com/products-by-category.html)

## Automate responding to alerts in Cloud by creating records in ServiceNow
Microsoft Defender for Cloud - includes AWS, GCP (formerly known as Azure Security Center) provides recommendations to protect workloads from known security risks & generates alerts to defend workloads in real-time.

Logic Apps has built-in connectors for Microsoft Defender for Cloud to capture the recommendations & alerts. It can also create records (Incidents) in Service-Now based on the recommendations & alerts.

## Steps to create the Logic App
1. Search for Logic Apps in Azure Portal. In the Logic Apps Designer, select the Blank Logic App template. Create a Logic App with Consumption Plan type.

    ![Alt txt](/images/logic-app-consumption.png)

    > *The Logic App has to be created as **Consumption** plan type or else the Logic App is not recognized by the **Workflow Automation** in Defender* which will be done after the step # 4.

2. In the Logic App designer, add a trigger for Microsoft Defender for Cloud Alert or Recommendation or Compliance. If you need all, create Logic Apps for each one of them.

    ![Alt txt](/images/defender-triggers.png)

3. Click on **+ New Step** and search for **ServiceNow**. Select **Create Record** as the action. You will be required to create a **ServiceNow Connection**. For this article, a free version of developer instance is created in Service-Now. From the developer dashboard, you will get the required details.

    ![Alt txt](/images/servicenow-connection.png)

4. Pass the values from the Defender from Cloud trigger to populate the Service-Now record based on your organization's requirements. Two of the triggers: Recommendation & Alert are shown below:

    > Note that two different Logic Apps are created for the different triggers in this article.

    ### a. Logic App 1 - lapp-demo-alert: Create record (Incident) in Service-Now based on the Alerts in Defender for Cloud

    ![Alt txt](/images/defender-alert-servicenow.png)

    ### b. Logic App 2 - lapp-demo: Create record (Incident) in Service-Now based on the Recommendations in Defender for Cloud

    ![Alt txt](/images/defender-recommendation-servicenow.png)

## Steps to filter Logic App triggers via Defender for Cloud using Workflow Automation
1. Search for Defender for Cloud in Azure portal & click on it. In the resource menu, on the left pane, click on Workflow automation under Management. Click on Add Workflow automation.

2. Workflow automation allows to filter on the trigger conditions for which the Alerts will be fired through the Logic App. For instance, when Alert Severity is set to "Medium, High", only those alerts will be triggered which are marked as Medium or High in Defender.

    ![Alt txt](/images/defender-workflow-automation.png)

3. Workflow automation for the Trigger type Recommendation can be configured as shown below.

    ![Alt txt](/images/defender-workflow-automation-recommendation.png)

## Test the Defender integration with ServiceNow

### Test the creation of ServiceNow records for Defender Alerts
1. Open Defender for Cloud in Azure portal. In the Resource Menu on the left pane, click on Security Alerts. In the command bar, click on Sample Alerts. Click on Create Sample Alerts. This will create a bunch of sample alerts in the Defender for Cloud. 

2. Once the sample alerts are created, click on any alert. This will open a sidebar, click on Take action --> expand Trigger Automated response --> Trigger Logic App. Another sidebar will open listing the logic app(s), select the one which has been configured previously for Alerts i.e. lapp-demo-alert --> click on Trigger. This will trigger the logic app & create an incident in ServiceNow using the sample alert.

    ![Alt txt](/images/servicenow-alert-incident.png)

### Test the creation of ServiceNow records for Defender Recommendation
1. Open Defender for Cloud in Azure portal. In the Resource Menu on the left pane, click on Recommendations. In the Recommendations pane, click on any recommendation which is marked unassigned.

2. Select the unassigned recommendation --> click on Logic App. A sidebar will open listing the logic app(s), select the one which has been configured previously for Recommendations i.e. lapp-demo --> click on Trigger. This will trigger the logic app & create an incident in ServiceNow for the Recommendation.

    ![Alt txt](/images/servicenow-recommendation-incident.png)

## References
* [Automate responses to Microsoft Defender for Cloud triggers](https://docs.microsoft.com/en-us/azure/defender-for-cloud/workflow-automation)
* [Automate Microsoft Defender for Cloud (formerly known as Azure Security Center) actions with Playbooks and ServiceNow](https://techcommunity.microsoft.com/t5/microsoft-defender-for-cloud/automate-azure-security-center-actions-with-playbooks-and/ba-p/264843)
* [Microsoft Defender for Cloud – Workflow automation](https://jadsonalves.com.br/microsoft-defender-for-cloud-workflow-automation/)
* [Automate responses to Microsoft Defender for Cloud triggers](https://docs.microsoft.com/en-us/azure/defender-for-cloud/workflow-automation)
* [Create an automatic response to a specific security alert using an ARM template or Bicep](https://docs.microsoft.com/en-us/azure/defender-for-cloud/quickstart-automation-alert?tabs=CLI)