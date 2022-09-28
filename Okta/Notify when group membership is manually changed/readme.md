# Notify when group membership is manually changed

## Overview
This workflow sends a slack notification whenever group membership is manually changed (add or remove) by an Okta admin. This can be helpful in monitoring for unwanted changes to groups managed by group rules.

The workflow consists of the following flow(s) and table(s):

Flows
1. Manual group membership change notification - user added
2. Manual group membership change notification - user removed

## Prerequisites
1. Access to an Okta tenant with Okta Workflows enabled
2. A configured Okta Connection. To configure a connection, see [Authentication](https://help.okta.com/wf/en-us/Content/Topics/Workflows/connector-reference/okta/overviews/authorization.htm).
3. A configured Slack Connection. To configure a connection, see [Slack Connector](https://help.okta.com/wf/en-us/Content/Topics/Workflows/connector-reference/Slack/Slack.htm)

## Setup
1. In both flows, set the `okta subdomain` field in the assign card to your subdomain. example `acme`
2. In both flows, select `options` in the "Send Message to Channel" Slack card and choose the appropriate channel. Update any other message settings.

## Limitations & Known Issues
* Both flows will triggers on manual changes made to any group. Add a continue if card and user the `Group ID` variable to trigger the flows for a specific group only. You can also use a if/else card with `contains` and a list of group ids to trigger on multiple specified groups.
