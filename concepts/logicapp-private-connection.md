# Logic Apps private connection
Logic Apps using Private endpoint: https://dev.to/pwd9000/securing-azure-logic-apps-with-private-endpoints-4c3f
Based on whether you have Consumption or Standard logic apps, you have these options:
1.	For Standard logic apps, you can privately and securely communicate between logic app workflows and an Azure virtual network by setting up private endpoints for inbound traffic and use virtual network integration for outbound traffic. https://docs.microsoft.com/en-us/azure/logic-apps/secure-single-tenant-workflow-virtual-network-private-endpoint
2.	For Consumption logic apps, you can create and deploy those logic apps in an integration service environment (ISE). That way, your logic apps run on dedicated resources and can access resources protected by an Azure virtual network. https://docs.microsoft.com/en-us/azure/logic-apps/logic-apps-securing-a-logic-app?tabs=azure-portal#isolation-guidance-for-logic-apps
