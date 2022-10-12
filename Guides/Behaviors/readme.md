# Behaviors

## Overview

With behavior detection and evaluation, Okta captures patterns of user behavior and uses this information to create profiles that describe typical patterns based on previous activity. This information can be used as part of sign-on policies for the Okta tenant.

[Okta Documentation - Behaviors](https://help.okta.com/oie/en-us/Content/Topics/Security/proc-security-behavior-detection.htm)

Details about behavior data for any applicable sign-in attempt are recorded in System Log events. To see behavior details for user.`session.start` and `policy.evaluate.sign_on `events, navigate to `DebugContext` and `DebugData` in the System log. This information is also returned as part of some event hooks, such as `User sign in attempt` as well as corresponding Okta event cards in Okta Workflows.

Behaviors can be useful in building custom notifications or securing accounts when potentialy malicious actions occur. 

## The Issue

Detection Logic in System Log events, which include behaviors, found within `logOnlySecurityData` are captured in a json format `{"Key":"Value"}`. Detections that evaluate behaviors `(debugContext.debugData.behaviors)` take the form of `Key=Value`. Unfortunately, behaviors returned as `Key=Value` are difficult to work within in workflows as frequently used cards such as `Get`, `Pluck`, `Filter` will not work be able parse them. 

Example behaviors formatted in `Key=Value`
```{"behaviors": "{New Geo-Location=NEGATIVE, New Device=POSITIVE, New IP=NEGATIVE, New State=NEGATIVE, New Country=NEGATIVE, Velocity=NEGATIVE, New City=NEGATIVE}"}
```

## Solution

The provided `behaviors.flow` includes logic for determing which format behaviors are returned in (based on whether `logOnlySecurityData is present`) and then converts `Key=Value` format to `{"Key":"Value"}`. Behaviors can then be used as you see fit elsewhere in your flows. 




