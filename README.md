# Logic Apps which use Azure Functions and Azure Media Services

## Prerequisites for all Logic Apps deployments

### 1. Create an Azure Media Services account

Create a Media Services account in your subscription if don't have it already.

### 2. Create a Service Principal

Create a Service Principal and save the password. It will be needed in step #4. To do so, go to the API tab in the account ([follow this article](https://docs.microsoft.com/en-us/azure/media-services/media-services-portal-get-started-with-aad#service-principal-authentication))

### 3. Make sure the AMS streaming endpoint is started

To enable streaming, go to the Azure portal, select the Azure Media Services account which has been created, and start the default streaming endpoint.

![Screen capture](images/start-se-1.png?raw=true)

![Screen capture](images/start-se-2.png?raw=true)

### 4. Deploy the Azure functions
If not already done : fork the repo, or download the repo.

Open the sln file in visual studio and deploy the functions to Azure.
Once deplooyed, add the Application Settings as follows

![Funtion App, Application Settings.](images/FunctionApp-Settings.PNG 'Application Settings')



## Logic App : An advanced VOD workflow

This template creates a Logic app which

* monitors a container in Azure Storage (blob trigger),
* copies new file to an Azure Media Services asset,
* triggers an encoding job,
* converts the English audio to text (using Media Indexer v2),
* translates the English subtitles to French (using Bing translator),
* copies back the French subtitles to the subtitles asset,
* publishes the output assets,
* generates a short playback URL (using bitlink)
* sends an email with Outlook when the process is complete or if the job failed. In the email, the playback link includes the two subtitles.

<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure-Samples%2Fmedia-services-dotnet-functions-integration%2Fmaster%2Fmedia-functions-for-logic-app%2Flogicapp3-advancedvod-deploy.json" target="_blank">
    <img src="http://azuredeploy.net/deploybutton.png"/>
</a>

![Screen capture](images/logicapp3-advancedvod-1.png?raw=true)
![Screen capture](images/logicapp3-advancedvod-2.png?raw=true)
![Screen capture](images/logicapp3-advancedvod-3.png?raw=true)



## Logic App : Live stream analysis using Video Indexer

This [page](LiveStreamAnalysis.md) presents a near real time video analytics solution which relies on Video Indexer to process a live stream.

[![Test Player](images/live-media-analytics-player1.png?raw=true)](LiveStreamAnalysis.md)


## Functions documentation
This [page](Functions-documentation.md) lists the functions available and describes the input and output parameters.
