# Track or Report Groups and Associated Group Rules

## Overview
Okta group rules already include a way to view all groups a user is added to when rule conditions are met. However, without checking each group rule individually there is no easy way to view which group rules are assigned to a specific group. This workflow generates a table containing all groups and their associated group rules. This can be helpful for determine which group rules are controlling membership to a given group. 

Tip - In the table, group rules are returned as an array. This can be hard to view due to the UI. Click the expand arrow next to a group rule cell to better view all associated group rules. You can also search within the expanded view.

## Getting Started

Two different workflows are available.
#### Track Groups and Associated Group Rules
Use in tenants with less than 200 group rules. Design to be run on a schedule.

Flows:
1. Stream Group Records
2. Update Groups and Group Rules Table
3. Search Group Rules

Tables:
- Groups and associated Group Rules

#### Report on Groups and Associated Group Rules
Supports up to the 20,000 group rules via streaming. Design to be run ad-hoc due to potential large data sets.

Flows:
1. Initiate flow
2. Iterate through group rule assignments
3. Populate "Group Rules" table
4. Populate "Groups with Associated Group Rules" Table
5. Rebuild group rule object

Tables:
- Group Rules
- Groups and associated Group Rules


### Prerequisites
1. Access to an Okta tenant with Okta Workflows enabled.
2. A configured Okta Connection. To configure a connection, see [Authentication](https://help.okta.com/wf/en-us/Content/Topics/Workflows/connector-reference/okta/overviews/authorization.htm).

### Setup
* If you have not already done so, import the appropriate folder.
* Open each flow and make sure the Okta actions cards are associated with the correct connection.
* Enable the flows.

## Limitations & Known Issues

## Resources
* [About Group Rules](https://help.okta.com/en-us/Content/Topics/users-groups-profiles/usgp-about-group-rules.htm)
