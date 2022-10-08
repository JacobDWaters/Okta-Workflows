# Behaviors

## Overview

With behavior detection and evaluation, Okta captures patterns of user behavior and uses this information to create profiles that describe typical patterns based on previous activity. This information can be used as part of sign-on policies for the Okta tenant.

[Okta Documentation - Behaviors](https://help.okta.com/oie/en-us/Content/Topics/Security/proc-security-behavior-detection.htm)

Details about behavior data for any applicable sign-in attempt are recorded in System Log events. To see behavior details for user.`session.start` and `policy.evaluate.sign_on `events, navigate to `DebugContext` and `DebugData` in the System log. This information is also returned as part of some event hooks, such as `User sign in attempt` as well as corresponding Okta event cards in Okta Workflows

## The Issue

Unfortunately, `behaviors` within the `DebugData` object are provided as a string, with each behavior and corresponding result returned in a non-standard json format. 

Example formatting of the behaviors key:value pair
```{
    "behaviors": "{New Geo-Location=NEGATIVE, New Device=POSITIVE, New IP=NEGATIVE, New State=NEGATIVE, New Country=NEGATIVE, Velocity=NEGATIVE, New City=NEGATIVE}"
```

This can make using `behaviors` in a workflow difficult as frequently used cards such as `Get`, `Pluck`, `Filter` will not work correctly.

## Solution
The provided `behaviors.flow` includes an example of how to convert the originally provided `behaviors` into a standard json object. The object and fields can then be used as you see fit elsewhere in your flows. 




