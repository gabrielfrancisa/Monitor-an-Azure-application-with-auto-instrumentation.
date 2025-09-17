# Monitor-an-Azure-application-with-auto-instrumentation.
This project, we create an Azure App Service web app with App Insights enabled, configure AUTO-instrumentation, create & and deploy a Blazor App,& and then view application metrics & and error data in App Insights. Implementing comprehensive app monitoring/observability without requiring code changes makes deployments/migrations simpler.


Tasks performed in this PROJECT:
1. Create a web app resource with Application Insights enabled
2. Configure instrumentation for the web app.
3. Create a new Blazor app and deploy it to the web app resource.
4. View application activity in Application Insights



Create resources in Azure
1. In your browser, navigate to the Azure portal https://portal.azure.com, signing in with your Azure credentials if prompted.

2. Select the + Create a resource located in the Azure Services heading near the top of the homepage.

3. In the Search the Marketplace search bar, enter web app and press enter to start searching.

4. In the Web App tile, select the Create drop-down and then select Web App.


Selecting Create will open a template with a few tabs to fill out with information about your deployment. 
The following steps walk you through what changes to make in the relevant tabs.

Fill out the Basics tab with the information in the following table:

>>> Setting	Action
1. Subscription:	Retain the default value.
2. Resource group:	Select rg-WebApplod54728081.
3. Name: monitorapp54728081
4. Slider under Name setting:	Select the slider to turn it off. This slider only appears in some Azure configurations.
5. Publish	Select the Code option.
6. Runtime stack	Select: .NET 8 (LTS) in the drop-down menu.
7. Operating System:	Select Windows.
8. Region:	Retain the default selection, or choose a region near you. (East US)
9. Windows Plan:	Select Create new, type: ASP-rg-WebApp54728081, and then select OK.
10. Pricing plan:	Select the drop-down and choose the Free F1, Shared D1, or Basic B1 plan.
11. Select, or navigate to, the Monitor + secure tab, and enter the information in the following table:

>>> Setting	Action
Enable Application Insights. Select Yes. If Application Insights on the Monitor + secure tab options are greyed, please select a different pricing plan above.
Application Insights	Select Create new, and a dialogue box will appear. Enter autoinstrument-insights in the Name field of the dialogue box. 
Then select OK to accept the name.
Workspace: Enter Workspace if the field isn't already filled in and locked.
Select Review + create and review the details of your deployment. 
Then select Create to create the resources.

It will take a few minutes for the deployment to complete. When it's finished, select the Go to resource button.

Configure instrumentation settings
To enable monitoring without changes to your code, you need to configure the instrumentation for your app at the service level.

In the left navigation menu, expand Monitoring and select Application Insights.

Locate the Instrument your application section and select .NET Core.

Select Recommended in the Collection level section.

Select Apply and then confirm the changes.

In the left navigation menu, select Overview.




>>> Create and deploy a Blazor app
In this section of the exercise, you create a Blazor app in the Cloud Shell and deploy it to the web app you created. All of the steps in this section are performed in the Cloud Shell.

Use the [>_] button to the right of the search bar at the top of the page to create a new Cloud Shell in the Azure portal, selecting a Bash environment. 
The cloud shell provides a command line interface in a pane at the bottom of the Azure portal. 
If you are prompted to select a storage account to persist your files, select No storage account required, your subscription, and then select Apply.

Note: If you have previously created a cloud shell that uses a PowerShell environment, switch it to Bash.

Run the following commands to create a directory for the Blazor app and change into the directory.

#BASH 1
>>> mkdir blazor
>>> cd blazor

Run the following command to create a new Blazor app in the folder.

#BASH 2
>>> dotnet new blazor

Run the following command to build the application to ensure there are no issues during creation.

#BASH 3
>>> dotnet build

Deploy the app to App Service
To deploy the app, you first need to publish it with the dotnet publish command and then create a .zip file for deployment.

Run the following command to publish the app into a publish directory.

#BASH 4
>>> dotnet publish -c Release -o ./publish

Run the following commands to create a .zip file of the published app. The .zip file will be located in the root directory of the application.

#BASH 5
>>> cd publish
>>> zip -r ../app.zip .
>>> cd ..

Run the following command to deploy the app to App Service. Replace YOUR-WEB-APP-NAME AND YOUR-RESOURCE-GROUP with the values you used when creating the App Service resources earlier in the exercise.

#BASH 6
>>>    az webapp deploy --name monitorapp54728081 \
 >>>   --resource-group rg-WebApplod54728081 \
 >>>   --src-path ./app.zip

When the deployment is completed, select the link in the Default domain field located in the Essentials section to open the app in a new tab in your browser.

Now it's time to view some basic application metrics in Application Insights. Don't close this tab, you'll use it in the rest of the exercise.

View metrics in Application Insights
Return to the tab with the Azure Portal and navigate to the Application Insights resource you created earlier. The Overview tab displays some basic charts:

Failed requests
Server response time
Server requests
Availability
In this section, you will perform some actions in the web app and then return to this page to view the activity. The activity reporting is delayed, so it may take a few minutes for it to appear in the charts.

Perform the following steps in the web app.

1. Navigate between the Home, + Counter, and Weather navigation options in the menu of the web app.

2. Refresh the web page several times to generate the Server response time and Server requests data.

3. To create some errors, select the Home button and then append the URL with /failures. This route doesn't exist in the web app and will generate an error. Refresh the page several times to generate error data.

4. Return to the tab where Application Insights is running, and wait a minute or two for the information to appear in the charts.

In the left navigation, expand the Investigate section and select Failures. It displays the failed request count along with more detailed information about the response codes for the failures.

Explore other reporting options to get an idea of what other types of information are available.




Clean up resources
Now that you have  finished the project, you should delete the cloud resources you created to avoid unnecessary resource usage.

In your browser, navigate to the Azure portal https://portal.azure.com, signing in with your Azure credentials if prompted.
Navigate to the resource group you created and view the contents of the resources used in this exercise.
On the toolbar, select Delete resource group.
Enter the resource group name and confirm that you want to delete it.

NOTE: Deleting a resource group deletes all resources contained within it. 
If you chose an existing resource group for this exercise, any existing resources outside the scope of this exercise will also be deleted.

Congratulations
This is the end of the project


