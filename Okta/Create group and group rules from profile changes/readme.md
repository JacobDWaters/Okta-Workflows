# Create groups and group rules from Okta profile changes

## Overview
Thie workflow can be useful for dynamically creating groups and group rules as new teams, departments, organizations (or anyone other profile attribute) are added to your Okta tenant. For example, your org creates a new Customer Enablement team? Automatically create a group and group rule and assign all members of the Customer Enablement team to the group.

To do this, the workflow monitors for changes to a specified profile attribute (e.g. department) in the Okta user profile. If the value of profile attribute changes (e.g. from IT to Engineering) the flow looks to see if a group already exists, if not the flow creates a corresponding active group and group rule.

The workflow consists of a single flow and one table:
- **Create group and group rule from profile changes** the flow will trigger when a user's Okta profile is updated.
- **Monitor profile attributes** a table for tracking changes to the specified profile attribute.

## Prerequisites
1. Access to an Okta tenant with Okta Workflows enabled
2. A configured Okta Connection. To configure a connection, see [Authentication](https://help.okta.com/wf/en-us/Content/Topics/Workflows/connector-reference/okta/overviews/authorization.htm).

## Setup
1. in the `Assign` card at the beginning, change the folowing values
    * `monitored profile attribute` = the variable name for the user profile attribute to monitor.
        * Example: for Department, use `department`
    * `group name prefix` = the prefix used to identify the group type.
        * Example: for Department, use `Dept - `. 
2. Update the `Compose` card for creating the group rule's expression conditions.
    * Example: `user.department=="Department"`
3. Update the `Monitored profile attributes` table
    * The flow assumes that any monitored attribute value already listed in the table has a pre-existing group and group rule. To exempt an attribute value from creating a new group and group rule, add them to the table prior to enabling the flow.
## Flow Chart

## Limitations & Known Issues
1. The flow currently only supports monitoring for changes to a single profile attribute.
