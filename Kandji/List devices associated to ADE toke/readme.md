# List Kandji Devices Associated to ADE token

## Overview
This workflow returns a list of all devices associated with a particular ADE (Automated Device Enrollment) integration in Kandji.

The workflow consists of the following flow(s) and table(s):

Flows
1. List devices associated with ADE token
2. Paginate

## Prerequisites
1. Access to an Okta tenant with Okta Workflows enabled
2. A Kandji API token with the appropriate permission for ADE. See [Kandji API](https://support.kandji.io/support/solutions/articles/72000560412-kandji-api)
3. A configured Kandji Connection. To configure a connection, see [Authentication](https://support.kandji.io/support/solutions/folders/72000559397).
4. The `ade_token_id` for a particular ADE integration. This can be found by doing a GET call to list all ADE integrations via the [Kandji API](https://api.kandji.io/). The `id` listed at the top of each entry is the `ade_token_id`.


## Setup
1. Add an event card in "1. List devices associated with ADE token" flow so the flow has a trigger.
2. In "1. List devices associated with ADE token" flow, set the `ade_token_id` in the Assign card to the appropiate ADE integration.

## Limitations & Known Issues
The workflow is not designed to list all devices associated with all ADE integrations in a Kandji tenant. The flow can be readily adapted to do so if needed.

