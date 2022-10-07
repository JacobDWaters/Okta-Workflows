# Google
While Okta provides some pre-built connectors for working Google apps (Gmail, Google Calendar, Google Workspace, etc) these connectors sometimes lack the necessary scopes and actions to build more complex workflows. Instead, Connector Builder can be used to create a custom connection with the desired scopes and actions.

Connector Builder supports custom OAuth connections. However, certain parameters (specifically `"access_type": "offline"`) are required for correctly authenticating a Workflows connection wtih Google via OAuth. Connector builder currently does not support adding parameters to the initial Authorization Call. Luckily, we can use Google's Developer OAuth 2.0 Playground and a Custom auth type connection to achieve this.


Note - Connector Builder is currently in Beta. 

### Resources
* [Google Cloud API Console](https://console.cloud.google.com/apis/dashboard)
* [Google Developer OAuth 2.0 Playground](https://developers.google.com/oauthplayground/)
* [Okta Workflows Connector Builder](https://help.okta.com/wf/en-us/Content/Topics/Workflows/connector-builder/connector-builder.htm)

# Setup

## Google Cloud Project and Oauth App

1. ### Create the Google Cloud Project
* Go to [cloud.google.com](https://console.cloud.google.com/) and create a new project 

2. ### Enable the APIs
* In the left menu, select "APIs and services" > "Enabled Apis and services". 
* Select "+ Enable APIs and Services" at the top.
* Search for the APIs you want to enable (e.g. Google Drive). You will need to add each API you want the connector to work with.
* On each API's page, "Enable" the API. The API is now enabled ready to be used.

3. ### Create the OAuth Client Credentials
* In the left menu, navigate to "Credentials", select "+ Create Credentials" > "OAuth client ID"
* Since this is the first time we're creating an OAuth client ID, we will need to configure a consent screen first, select "Configure Consent Screen"
* Select `Internal` for user type.
* Fill out the required fields for App Name, User support email, etc.
* In the scopes section, add the scopes you want your connector to have. Remember which scopes you added! For example, add `https://www.googleapis.com/auth/drive` for Google Drive.  If you are unsure about which scopes you need, read the apps associated API Reference documentation for guidance. 
* Make sure to save. The OAuth consent screen is now created.
* Select "+ Create Credentials" >  "OAuth client ID"
* From application type, select `Web application`, give the Web app a name.
* For Authorized redirect URIs enter `https://developers.google.com/oauthplayground`
* Select create.
* Copy and save the `Client ID` and `Client Secret`. This information is sensitive, store somewhere secure.

4. ### Get the Refresh Token
* Go to [Google's OAuth 2.0 Playgound](https://developers.google.com/oauthplayground/)
* Select the "Cog" in the upper-right to configure the OAuth 2.0 connection.
* Make sure the following is set:
    * OAuth Flow = `Server-side`
    * OAuth endpoints = `Google`
    * Authorization endpoint = `https://accounts.google.com/o/oauth2/v2/auth`
    * Token endpoint = `https://oauth2.googleapis.com/token`
    * Access token location = `Authorization Header w/ Bearer prefix`
    * Access Type = `Offline`
    * Force prompt = `Consent Screen`
    * User your own OAuth Credentials = `CHECKED`
    * OAuth Client ID = `<YourClientID>`
    * OAuth Client secret = `<YourClientScret>`
* Under "Select & authorize APis", find the APIs you enabled and add all relevant scopes. Once done, select "Authorize APIs".
* You will be prompted to a Google account to authorize with.
* Once done, select "Exchange Authorization code for tokens" and then save the `refresh token` somewhere secure.

## Okta Workflows

5. ### Create a Connector in Connector Builder
* Before you can create a connector, make sure "Workflows Connector Builder" is enabled as an Early Access feature in your Okta tenant.
* Go to Okta Workflows, select "Connector Builder".
* Next to "Connectors", select + to create a new connector. Give it a name.

6. ### Configure Authentication
* In the Authentication section, select "setup authentication"
* For Authentication, enter the following:
    * Auth Type = `Custom`
    * Parameters (Label, Key, Type)
        * Client ID, `client_id`, text
        * Client Secret, `client_secret`, password
        * Grant Type, `grant_type`, text
        * Refresh Token, `refresh_token`, password
* Save the Authentication
![Connector - Authentication](/Connectors/Google/Connector%20-%20Authentication.png)

7. ### Test the Connection
* Go to the conenector's "Test Connections" section, select "+ New Connection"
* For the new connection, enter the following:
    * Connection Nickname = `SomethingHelpful`
    * Client ID = `<YourClientID>`
    * Client Secret = `<YourClientSecret>`
    * Grant Type = `refresh_token`
    * Refresh Token = `<YourRefreshToken>`
* Select "Create" to create and save the new test connection.
![Connector - Test Connection](/Connectors/Google/Connector%20-%20Test%20Connection.png)

8. ### Configure the httpHelper Flow
* Configure the httpHelper flow as follows. The flow will use the refresh token to grab an access token each time it runs. The flow can then make the necessary API calls. If you have never built a httpHelper flow before, read Okta's [Build a httpHelper flow](https://help.okta.com/wf/en-us/Content/Topics/Workflows/connector-builder/capia-httphelper.htm) for instructions.

![Connector - httpHelper](/Connectors/Google/Connector%20-%20httpHelper.png)

9. ### Create Additional Flows
* Create additional flows for the connector. There are a myriad of options here, so build whatever flows are going to be most useful for you!

#### Custom API Action and _authping cards
flows for doing a `Custom API Action` card as well as handling `_authping`(authentication validation) have been included. These flows must be downloaded and individually uploaded to the connector.

the  connector is Google API agnostic, so you will need to determine which endpoint and HTTP request you want to use for the `_authping` flow first. Update and save before implementing. I strongly recommend you use a simple GET Http request for authentication verification. HTTP requests like `GET https://www.googleapis.com/drive/v3/files` may take a long time to process or fail outright.


Note: neither card has been fully tested currently and may fail. If that happens, file a pull request or send a message and I will fix. 

10. ### Deploying the Connector
* Once you have created the additional flows and are done testing, go to "Deployment" to deploy the connector.
* Select "Validate connector", Okta will check to make sure there are no validation errors.
* You have a choice to either deploy a `test version` or `local connector`
    * `Test version` will be deployed to your Okta workflows but only be available if you select "include test connectors" when choosing from the "Add app action" cards. Should only be used for testing.
    * `Local connector` will be deployed to your Okta workflows and will be available under "My Connected Apps". Can be used for testing or in production.
* Select your preferred deployment method and wait for deployment to complete.

The connector is now available in Okta Workflows! Create a New Connection in Workflows and start usinng the connector and cards in your workflows.
Tip - if you are unsure about how to setup the next connection, look at section "#7. Test the Connection" of the setup instructions for help.
