# Logic App - HTTP request-response, HTTP POST, Extract contents from file

The logic app code in [json file](workflow-invoke-ML.json) does the following. To see this Logic App in action, copy the contents of the json file into the Code section under Developer blade in Logic App. 

The Logic App workflow looks like as shown below:

![Alt text](/images/logicapp-designer-view.png)

1. Accepts HTTP POST request with URL of the file (image) as payload.

![Alt text](/images/http-request.png)

2. Extracts the content of the file from the URL

![Alt text](/images/http-action-getfilecontent.png)

3. Invokes the Azure ML model endpoint with the authorization header & content of the file in the body as payload.

![Alt text](/images//http-action-invoke-post.png)

4. Sends back the response.

![Alt text](/images/http-action-response.png)

## References
* [Receive and respond to inbound HTTPS requests in Azure Logic Apps](https://docs.microsoft.com/en-us/azure/connectors/connectors-native-reqres)
* [Invoke endpoints over HTTP or HTTPS from Azure Logic Apps](https://docs.microsoft.com/en-us/azure/connectors/connectors-native-http)
