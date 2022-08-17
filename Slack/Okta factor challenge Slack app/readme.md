# Okta Factor Challenge Slack App 

## Overview
This workflow is a proof of concept.

Being able to verify a users identity is a frequent and critical part of the modern IT process. There are plenty of cases where one may want to validate a user's identity before providing sensitive information or making changes on their behalf. This Slack app and workflows provide a means by which to verify a user's identity with Okta directly within Slack itself. 

The workflow consists of the following flows:
1. Trigger Okta Factor Challenge
2. Filter Factor List
3. Create Verification Options Slack Block
4. Slack Interactivity Endpoint
5. Start Okta Factor Verification 
6. Verify Okta Factor Challenge

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

In flows  #1, #5, and #6 make sure the custom `API Connector` cards are correctly associated with the newly created API connector. 

3. ### Customizing the flows
Make the following changes to customize the flows.
* `2. Filter Factor List`. This flow creates a list of approved factors that a user can choose to verify with. Remove `factors` you dont want available to users from the first "Construct List" card. Do the same for `providers` on the second "Construct List" card.
* `5. Start Okta Factor Verification`. For push notification verification to work, enter your okta subdomain (e.g. acme) in the `okta subdomain` field of the first "Assign" card. This info is used to help parse out the `poll url` for verifying push notifications.

4. ### Testing
The workflow should now be configured. To test, go to "1. Trigger Okta Factor Challenge" flow and select Test. Enter your Okta User ID in the input fields. 

5. ### aditional configuration
To trigger the workflow, add a "Call Async Flow" card to another workflow and point it to flow #1. make sure to pass the appropriate Okta User IDs to flow #1.

You will likekly want to update "6. Verify Okta Factor Challenge" to call other flows or include additional information depending on the returned `factorResult`. Update the branch of the `if/elseif` card handling `factorResults` to do so.


## Limitations & Known Issues
1. Supported Factors

The Slack app ONLY supports the following factors:
* `call`
* `email`
* `push`
* `sms`
* `token:software:totp`

    Cannot read inputs from `token:hardware`, `utf`, `web`, and `webauthn`. `question` is not supported as security question answers are not temporary and may be stored in Slack logs and readable by admins or other systems.

2. Supported Providers

The Slack app ONLY support the following providers:
* `OKTA`
* `GOOGLE`

Other providers generally rely on `token`, `web`, or `webauthn`. 

3. [Okta Workflow Limitations](https://help.okta.com/wf/en-us/Content/Topics/Workflows/workflows-system-limits.htm)

 
    It is strongly recommended you consider the needs of your org and work environment before implementing.
 
    The Slack app may fail to verify a factor within the required time frame due to "times executions taking take longer than 60 seconds." Further, "Workflows doesn't guarantee execution latency. In most cases, flows run very fast, but Workflows is a "multi-tenant system and does not have a latency SLA." 

    Synchronous flows such as customizing an auth decision or orchestrating user interaction are considered "Unsupported use cases."

4. Okta User and Slack User Association

    The workflow relies on `email/primary email` in order to associate an Okta User with their Slack account. An assumption is made that the user's email in Okta will match a user's email in Slack. If that is not the case, the flow will need to be updated in order to associate a given Okta User with their corresponding Slack account.

5. Security Risks 

    Please carefully consider any other possible security risks before using! Certain info such as `okta user id`, `factor id` and `passCode` needs to be passed to Slack in order for the workflow and bot to work. This may be info you are not comfortable exposing to Slack. 

    `call`, `email`, `sms` are not secure means of doing user verification - they are included as a proof of concept. Recommend reading [About Multifactor Authentication](https://help.okta.com/en-us/Content/Topics/Security/mfa/about-mfa.htm) to determine which factors you want to support.
