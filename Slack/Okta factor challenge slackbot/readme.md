# Okta Factor Challenge Slackbot

WORK IN PROGRESS

## Overview
This slack and workflows are a proof of concept. Please read the `Limitations and Known Issues` section THOROUGHLY before deciding to implement at your org or not!

Being able to verify a users identity is a frequent and critical part of the modern IT process. There are plenty of cases where one may want to validate a user is who they are, before providing sensitive information or making changes on behalf of a user. This slack bot and workflows provide a means by which to verify a user's identity with Okta directly within Slack itself. 

The workflow consists of a the following flows:
1.
2.
3.
4.
5. 

## Thank You
This slack bot would not be possible without the following contributions!
* Dmitri (@Dmitri in MacAdmins). This slackbot was heavily inspired by their [Filevault Recovery Retrieval](https://www.naviguidance.com/blog/filevault-recovery-retrieval) workflow! They've been incacluably helpful in advancing my IT career as well!
* Gabiral (@Gabriel in MacAdmins). For their guidance and input in working with Okta's API and factors in general. Also for pushing me to see if this is doable with not only `push` but other factors as well!


## Prerequisites
1. Access to an Okta tenant with Okta Workflows enabled
2. A configured Okta Connection. To configure a connection, see [Authentication](https://help.okta.com/wf/en-us/Content/Topics/Workflows/connector-reference/okta/overviews/authorization.htm).
3. Access to Slack with the ability to create and edit slack bots.
4. A configured Slack Connection. To configure a connection, see [Slack Connector](https://help.okta.com/wf/en-us/Content/Topics/Workflows/connector-reference/slack/slack.htm)
5. A API Connection for the slackbot itself. Please see the "Setup" section for how to configure the slackbot and connection.
6. A configured "API Endpoint" event card for the slackbot to send interactivty events to. Please see the "Setup" section.

## Setup

TBD!

## Limitations & Known Issues
1. Supported Factors

The slackbot ONLY supports the following factors:
* - call
* - email
* - push
* - sms
* - token:software:totp

    Currently unable to find a way to read inputs from `token:hardware`, `utf`, `web`, and `webauthn`. `question` is not supported as security question answers are not-temporary and this could pose a serious security risk. Answers may be stored in slack logs and readable by Slack Admins or other systems.

2. Supported Providers

The slackbot ONLY support the following providers:
* - OKTA
* - GOOGLE

Other providers generally rely on `token`, `web`, or `webauthn`. 

3. [Okta Workflow Limitations](https://help.okta.com/wf/en-us/Content/Topics/Workflows/workflows-system-limits.htm)

 
    It is strongly recommended you consider the needs of your org and work environment before implementing.
 
    The slackbot may fail to verify a factor within the required time frame due to "times executions taking take longer than 60 seconds." Further, "Workflows doesn't guarantee execution latency. In most cases, flows run very fast. Further, "Workflows is a multi-tenant system and does not have a latency SLA." 

    Synchronous flows such as customizing an auth decision or orchestrating user interaction are considered "Unsupported use cases."

4. Okta User and Slack User Association

    The workflow relies on `email/primary email` in order to associate an Okta User with their slack ID. An assumption is made that the user's emails in Okta will match a user's email in their slack profile. If that is not the case, the flow will need to be updated in order to associate a given Okta User with their corresponding slack account.

5. Security Risks 

    Please carefully consider any other possible security risks before implementing! Certain info such as `okta user id`, `factor id` and factor answers needs to be passed to Slack in order for the workflow and bot to work. This may be info you are not comfortable exposing to Slack. 

    `call`, `email`, `sms` are not secure means of doing user verification. Recommend reading [About Multifactor Authentication](https://help.okta.com/en-us/Content/Topics/Security/mfa/about-mfa.htm) to determine which factors you want to support.