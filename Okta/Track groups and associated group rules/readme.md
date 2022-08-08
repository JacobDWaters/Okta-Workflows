# Track Groups and Associated Group Rules

## Overview
This workflow can be used to generate return shipping labels with ShipEngine. This can be helpful in automating the offboarding process for remote users and having them return equipment back. The flow can be readily adapted to support shipping to users as well.

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
* Open the flow.
* If you would like to do tracking pages as part of the flow, create a ShipEngine Theme and enter the `Tracking Theme Guid` in the `Branded Tracking Theme GUID` card. If no value is entered, the flow will skip this step.
* Make sure the API Connector cards are associated the ShipEngine API connection created earlier.
* Make sure the Okta and Gmail actions cards are associated with the correct connections.
* `Ship To` card, enter your return shipping information. This could be a company address, warehouse, etc.
* `Package Weight` card, enter the aproximate weight of the package.
* `Package Dimensions` card, enter the aproximate dimensions of the package.
* `Shipment` card, enter the ShipEngine `service_code` for the courrier (USPS, Fedex, UPS, etc) you will be using. Enter `label_layout` (letter, 4x6, etc) for the generated shipping label.
* `Email Subject` card, compose your email subject line.
* `Email Body` card, compose your email body. Drag and drop fields as needed.

3. ### Enable the Flow
Enable the flows!

## Limitations & Known Issues
* The group rules
## Resources
* [About Group Rules](https://help.okta.com/en-us/Content/Topics/users-groups-profiles/usgp-about-group-rules.htm)
