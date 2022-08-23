# Audit All App Groups

## Overview
This workflow allow you to generate a list of all apps and all assigned groups. 

This flow is a redsign of @pro4tlzz's wonderful [App Group Report Workflow](https://github.com/JacobDWaters/ITSupportTools/tree/main/okta-workflows/app_group_audit).

The workflow consists of the following flow(s) and table(s):

Flows
- "1. Schedule run list applications"
- "2. Paginate"
- "3. Get groups for app"
- "4. Get info for groups"

Tables
- Application Groups

## Prerequisites
1. Access to an Okta tenant with Okta Workflows enabled
2. A configured Okta Connection. To configure a connection, see [Authentication](https://help.okta.com/wf/en-us/Content/Topics/Workflows/connector-reference/okta/overviews/authorization.htm).

## Setup
1. In "Schedule run list applications" flow, set your preferred schedule for the flow to run on.
2. Enable all flows.

## Limitations & Known Issues


