# Okta Password Reset Alert Bot

## Overview
![Example](/Slack/Okta%20Password%20Reset%20Alert%20bot/Example.png)
This Slack bot sends an alert to a user anytime their Okta account password has been reset. Based on the information provided, the user can decided to protect their account by triggering account suspension and clearing of all active user sessions.

the bot message includes the following activity details to help a user determine if a password reset was malicious or not.
* Browser
* OS
* Date & Time
* Geographical Context
* IP Address

The workflow consists of the following flows and tables:

Flows:
1. User Okta Password Reset Updated
2. Slack Interactivity Endpoint
3. Suspend Okta User and Clear Sessions


WARNING - When testing the workflow, make sure you do not test on active user accounts. Accounts could be erroneously suspended!

## Prerequisites
1. Access to an Okta tenant with Okta Workflows enabled
2. A configured Okta Connection. To configure a connection, see [Authentication](https://help.okta.com/wf/en-us/Content/Topics/Workflows/connector-reference/okta/overviews/authorization.htm).
3. Access to Slack with the ability to create and edit Slack bots.
4. A configured Slack Connection. To configure a connection, see [Slack Connector](https://help.okta.com/wf/en-us/Content/Topics/Workflows/connector-reference/Slack/Slack.htm)
5. A API Connection for the Slack app itself. Please see the "Setup" section for how to configure the Slack app and connection.
6. A configured "API Endpoint" event card for the Slack app to send interactivty events to. Please see the "Setup" section.

## Setup
Import the flowpack before beginning setup.

1. ### Slack Bot Setup

Go to https://api.Slack.com/apps and click “Create New App”. Give the app a name and select an appropriate workspace.

Navigate to the “Interactivity & Shortcuts” page. Toggle "ON" Interactivity. We need to provide Slack with the appropriate `Request URL` for Slack to send user interaction data. To do so, we will fetch the `Invoke URL` from  the "4. Slack Interactivty Endpoint" flow.

Open the "4. Slack Interactivity Endpoint" flow. On the API Endpoint event card, select Endpoint settings `</>`. Copy the `Invoke URL`. Save the flow. Paste the `Invoke URL` into the `Request URL` field in the Slack app, then Save Changes.

Navigate to the “OAuth & Permissions” page from the left menu bar. Select the "Add an OAuth Scope" under "Bot Token Scopes” section. The bot will need the following permissions
* `im:read`
* `im:write`
* `im:history`
* `chat:write`

This will allow the bot to start direct messages with users and read messages between the bot and the user. 

At the top of the page select "Install to Workspace" under the “OAuth Tokens for Your Workspace” section. Once authorized and installed, a `Bot User OAuth Token` will be available. Copy and save it, the token will be needed for the next step.

2. ### Custom API Connection for Slack app
In Okta Workflows Open the `Connections` tab, select "+ New Connection". Select API Connector type and enter the following information:
* Connection Nickname = Whatever your like (e.g. Okta Factior Challenge Slack app)
* Auth Type = `Custom`
* Header Name = `Authorization`
* Header Value = `Bearer <Bot User OAuth Token>`

Select Create to save.

In flows  #1 and #2 make sure the custom `API Connector` cards are correctly associated with the newly created API connector.

3. ### Additional Configuration
No additional configuration is required. 


## Limitations & Known Issues

