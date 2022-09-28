# Activate Okta Users prior to Start Date

## Overview
This workflow allow you to activate Okta users prior to their start date

The workflow consists of the following flow(s) and table(s):

Flows
1. Schedule list of Users to be Activated
2. Activate New Users

## Prerequisites
1. Access to an Okta tenant with Okta Workflows enabled
2. A configured Okta Connection. To configure a connection, see [Authentication](https://help.okta.com/wf/en-us/Content/Topics/Workflows/connector-reference/okta/overviews/authorization.htm).

## Setup
1. Set the date and time you want the `Scheduled Flow` event card to run on.
2. Set the variable name of your Start Date field in your default Okta user profile. default is set to `startDate`
2. Set the # and unit to subtract from the `Current Time` taken from the `Scheduled Flow` event card. This determines how early to activate the Users. For example, activate users two day earlier than the `Scheduled Flow` event card's current date.

## Limitations & Known Issues


