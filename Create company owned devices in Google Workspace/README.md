# Create company owned devices in Google Workspace

## Overview

This flopack is a helper flow that creates [company owned devices](https://support.google.com/a/answer/7129612?hl=en) in Google Workspace using Google's [Cloud Identity Devices API](https://cloud.google.com/identity/docs/concepts/overview-devices).

## Prequisites
- This method requires your org to have one of the following Google Workspace SKUs: Enterprise Standard, Enterprise Plus, Enterprise for Education, and Cloud Identity Premium
- You must setup the Devices API and create a Google Cloud project. See https://cloud.google.com/identity/docs/how-to/setup-devices
  - Project requires one of the following Oauth Scopes
    - https://www.googleapis.com/auth/cloud-identity.devices
    - https://www.googleapis.com/auth/cloud-identity
- You must have a custom connection in Okta Workflows that connects to the Google Cloud Project. 

## Notes
- Recommend creating a parent flow and using an in-built connector like JAMF or Kandji to GET or steam a list of devices to the helper flow. If so, make sure the platform or device type is correctly mapped to the "Platform" field.
- The Create Device request only requires deviceType and serialNumber be included in the body. 
  
## To do
- [ ] Add guide for how to set up a custom connection with a google cloud project to be included later.

## References
- [Device API References](https://cloud.google.com/identity/docs/reference/rest#rest-resource:-v1.devices)
