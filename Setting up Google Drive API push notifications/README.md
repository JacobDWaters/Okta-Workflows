# Setting up Google Drive API push notifications

## Overview
This flopack and instructions explains how to setup Google Drive API push notifcations with Okta Workflows. This allows you to watch for changes to Google Drive resources, such as Google Sheets, Google Docs, or Google Slides, without polling to determine if a change has occurred.


## Prequisites
- An active Google Drive connector in Okta Workflows. [Recommended]

OR

- A custom api connector with an appropriately configured Google Cloud project, Google Drive API enabled, and service account

- Access to the (Google Search Console)[https://search.google.com/search-console/about]
- Access or ownership of the resources you want to monitor

## Instructions

### Configure the Endpoint flow.
- Import the "Configure Endpoint for Google Drive API Push Notifications" flow.
- Open the flow and select endpoint settings (the </> icon) at the bottom of the "API Endpoint" event card.
- Copy the invoke URL.
        Make sure the endpoint is initially exposed as a Public Service, otherwise it will not be possible to verify ownership of the endpoint's invoke url during the next step.
        
### Verify ownership of the endpoint's invoke url.
...Google requires that we verify ownership of the receiving callback endpoint (invoke url) before sending push notifications. We will use Google's Search Console to do this.

- Open (Google Search Console)[https://search.google.com/search-console/about]
- Go to the main menu and select search property, then select + Add Property.
- For property type, select "URL prefix".
- Paste the flow's Invoke URL, select continue.
- From the verify ownership options, select HTML Tag.
- Copy the provided meta tag code only (the alphanumeric string). Do Not select Verify yet!
- Go back to the flow, and in the first Compose code replace "metaTagHere" with the provided meta tag.
- Save & turn ON the flow.
- In Google Search Console select Verify. You should receive a message indicating a successful verification of the flow's invoke URL.
- Once verified you can delete the meta tag compose card and raw return card from the flow.

The flow has now been verified and can be used to receive push notifications.

Once the endpoint flow has been configured and verified, there are two options regarding the type of push notifications that can be received

### Options 1: Create Google Drive API push notification for a single file

This is the easier of the two methods and will allow for monitoring for changes of a single file resource.
- Import the "Create Google Drive API push notification for a single file" flow.
- Add the file ID for the file you want to monitor.
- Add the invoke URL that was configured earlier.
- Save and turn ON the flow.
- Run the flow.

### Option 2: Create a Google Drive API Push Notification for all resource changes

This method allows for the monitoring of all resource changes.
- Import the "Create Google Drive API push notification for all resource changes" flow.
- Add the invoke URL that was configured earlier.
- Save and turn ON the flow.


## Resources
- https://developers.google.com/drive/api/guides/push
