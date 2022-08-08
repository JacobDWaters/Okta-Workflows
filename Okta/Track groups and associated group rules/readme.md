# Track Groups and Associated Group Rules

## Overview
Okta group rules already include a way to view all groups a user is added to when rule conditions are met. However, without checking each group rule individually there is no easy way to view which group rules are assigned to a specific group. This workflow generates a table containing all groups and their associated group rules. This can be helpful for determine which group rules are controlling membership to a given group. 

Tip - In the table, group rules are a return as an array. This can be hard to view due to the UI. Click the expand arrow next to a group rule cell to better view all associated group rules. 

## Getting Started

The workflow consists of the following flows and tables:

Flows:
1. Stream Group Records
2. Update Groups and Group Rules Table
3. Search Group Rules

Tables:
- Groups and associated Group Rules

### Prerequisites
1. Access to an Okta tenant with Okta Workflows enabled.
2. A configured Okta Connection. To configure a connection, see [Authentication](https://help.okta.com/wf/en-us/Content/Topics/Workflows/connector-reference/okta/overviews/authorization.htm).

### Setup
* If you have not already done so, import the flopack.
* Open each flow and make sure the Okta actions cards are associated with the correct connection.
* Enable the flows.

The workflow is triggered by a "Schedule" event card in the `1. Stream Group Record` flow. You can update the schedule event card to run at your preferred cadence or replace the card entirely with any other event card.

## Limitations & Known Issues
* The "Search Group Rules" card in `2. Update Groups and Groups Rules Table` flow returns the `First 200 Matching Records`. If your tenant has more than 200 group rules, the flow may fail to include all associated rules. 

## Resources
* [About Group Rules](https://help.okta.com/en-us/Content/Topics/users-groups-profiles/usgp-about-group-rules.htm)
