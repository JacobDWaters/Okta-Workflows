# Track User Profile Changes

## Overview
This workflow tracks user profile changes and creates a table with the user's old profile, new profile, and changed attributes. 

## Getting Started

Workflow consists of the following flows and tables:
Flows:
1. Monitor User Profile Changes
2. Fetch Changed Attributes
3. Search User profiles [Optional]
4. Create Initial User Profile Entries [Optional]

Tables:
- User Profile Changes

### Prerequisites
1. Access to an Okta tenant with Okta Workflows enabled.
2. A configured Okta Connection. To configure a connection, see [Authentication](https://help.okta.com/wf/en-us/Content/Topics/Workflows/connector-reference/okta/overviews/authorization.htm).

### Setup
* If you have not already done so, import the appropriate folder.
* Open each flow and make sure the Okta actions cards are associated with the correct connection.
* in "1. Monitor User Profile Changes" flow, add or remove attributes (by variable name) you want to monitor for from the Construct List card. 
* Enable the flows.

Optional
* If you want to generate a list of all users and their profiles, open "3. Search User profiles" and select Test. This will populate the table with each Okta User and a complete profile object. Otherwise, turn Off or delete these flows.

## Limitations & Known Issues

## Resources
* [About Group Rules](https://help.okta.com/en-us/Content/Topics/users-groups-profiles/usgp-about-group-rules.htm)
