# Generate return shipping labels with ShipeEngine

## Overview
This workflow can be used to generate return shipping labels with ShipEngine. This can be helpful in automating the offboarding process for remote users and having them return equipment back. The flow can be readily adapted to support shipping to users as well.


The workflow consists of a single helper flow:
- **Generate Return Shipping Labels with Ship Engine**.

## Prerequisites
1. Access to an Okta tenant with Okta Workflows enabled
2. A configured Okta Connection. To configure a connection, see [Authentication](https://help.okta.com/wf/en-us/Content/Topics/Workflows/connector-reference/okta/overviews/authorization.htm).
3. A [ShipEngine](https://www.shipengine.com/) account.
4. A [ShipEngine Carrier](https://www.shipengine.com/docs/carriers/setup/).
5. Optional - A [ShipEngine Theme](https://app.shipengine.com/#/portal/themes. 
6. A custom API connection for the ShipEngine account. 
7. A configured email provider connection (i.e. Gmail). See [Connectors](https://help.okta.com/wf/en-us/Content/Topics/Workflows/connector-reference/connector-reference.htm)

## Setup
1. ### Create ShipEngine API Connection**
Make sure you have create a ShipEngine account and an `<API-Key>` beforehand.
* In Workflows go to "Connections" > "+ New Connection"
* Select "API Connector" from the list of available options
* Configure the API connector as follows:
    * Connection Nickname = `<NAME>`
    * Auth Type = `Custom`
    * Header Name = `API-Key`
    * Header Value = `<API-Key>`
* Select create to save.

2. ### Configure the flow.
* If you have not already done so, import the workflow.
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
Enable the flow and add it as a helper flow to your existing offboard flows. You can also copy/modify the flow to support Shipping To users as well!


## Limitations & Known Issues

## Resources
* [ShipEngine API Doucmentation](https://www.shipengine.com/docs/)
