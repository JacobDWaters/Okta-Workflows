# Get All Okta User's Last App Access Dates

## Overview
This workflow can be used to build a table containing every Okta user's last access date for each app assigned to them. This can be helpful when conducting access reviews and audits for compliance or security purposes. It can also be useful information when doing licensing or procurement reviews.


The workflow consists of the following flow(s) and table(s):

Flows
- 1. List Active Okta Users
- 2. List user's assigned applications
- 3. Retrieve user's last app access date

Tables
- Access Review Report

## Prerequisites
1. Access to an Okta tenant with Okta Workflows enabled
2. A configured Okta Connection. To configure a connection, see [Authentication](https://help.okta.com/wf/en-us/Content/Topics/Workflows/connector-reference/okta/overviews/authorization.htm).

## Setup
1. In "List Active Okta Users" flow, set your preferred schedule for the flow to run on.
2. Enable all flows.

### Optional
adjust the randomized wait times in "2. List user's assigned applications" and "3. Retrieve user's last app access date" flows. Please read "Limitations & Known Issues" first!


## Limitations & Known Issues
1. Search Log Retention Period
    Okta's search logs only contains 90-days worth of history. Access dates older then 90 days will be missing. `Last Access Date` in the table will be blank.
2. Rate Limits
    The flows include a randomized wait time in an attempt to prevent breaching Okta's API rate limits. However, at a certain organizational size (# of users and apps) it may not be possible to stay within the rate limits without making the flow take an exceedingly long time.
3. Non-SSO Apps
    Non-SSO Apps access dates may not be logged. The flow uses `user.authentication.sso` as the search log `event type` to find relevant log entries. You can customize the search log filters to attempt to find other app login entries.

