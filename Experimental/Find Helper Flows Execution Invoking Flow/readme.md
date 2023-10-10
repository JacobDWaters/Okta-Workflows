# Find Helper Flow's execution Invoking Flow

## Overview
This workflow is considered experimental. It leverages various undocumented Okta Workflows internal APIs. These APIs could change at any moment and using them could result in breaking flows or Okta workflows itself.

This flopack can be used to find which parent flow invoked a given helper flow's execution. Usually, this is not an issue as one can see the parent flows ID and name in the execution history, but sometimes save data was never enabled on a helper flow, data was purged at a later date, or a helper flow has multiple very similar named parent flows which invoked it.


USE WITH CAUTION. 


The workflow consists of the following flows and tables:
1. Find helper flow execution invoking flow
2. Get Okta Workflow folders
3. Get all Okta Workflow flows
4. Find invoke Flow execution for helper flow execution

## Prerequisites
1. An API Connection with `Auth Type` set to `None`
2. Some familiarity with your browser's developer console (in this case Google Chrome) and reading Network data.

## Setup
Import the flowpack before beginning setup.
Create the API Connection

## How to Use
1. In Okta Workflows, navigate to the helper flow you want to find a specific execution of
2. In Google Chrome (next steps may differ depending on the browser used) right click and select `Inspect ` to open the Developer Console. Select the `Network`
3. Select `Execution History` in the helper flow
4. In the Developer Console open the `Network` tab and you should see a list of various calls and data use to render the execution page.
5. Look for the an entry that looks something like the following

    https://`subdomain`.workflows.okta.com/app/api/history/flow?orgId=`orgId`&floId=`flowId`&isMonitor=false&limit=50&endDate=`timestamp`


6. This is the internal API GET call that Okta Workflows makes to get the execution history of a specific flow.
7. In the entry, select the `Response` tab to view the returned results of the flow's execution history
8. Search through the execution history to find the specific `execution` you are wanting to trace back by the `created` value. The date will be ISO 8601 format so you may need to do some conversion to find the specific execution.
    
9. Get the `traceId` of the specific execution.
    The `traceId` value is the id of the execution that triggered the flow. For a helper flow, this ID corresponded to the `execution` value of a Parent flow's execution which invoked the helper flow.
    See `Example - Helper Flow - Execution.json` and  `Example - Parent Flow - Execution.json` as an example of how the `execution` value of a given parent flow is the same as the `traceID` of the helper flow's execution.
10. Copy the `traceId` value of the execution you want. We will need that later when running the flopack
11. Open the `1. Find helper flow execution invoking flow`
12. Enter information in the `assign` card for required data for the flopack to work.
13. For `Cookies`, `Accept-Language`, and `User-Agent` you wil need to go back to Developer Console and select `Headers` in the API call for the execution history earlier. Scroll down to `Request Headers` and copy each value into the `assign` cards fields.
14. For `org_id` you can find that information by looking at the API Call's `Request URL`. i.e the value after `orgId=`
15. Save the flow.
16. Select Run on the flow and paste the `traceId` value from earlier.
17. Select Run Test.
18. Close the flow and navigate to the `4. Find invoke Flow execution for helper flow execution` flow.
19. Wait for the flow to finish running.
20. Open Execution History and select the Status dropdown (next to the search) and select Success.
21. If all worked correctly, the only successful flow wil be the one which includes the correct `floId` for the parent flow that invoked the helper flow.
22. Replace the values in this url https://`subdomain``.workflows.okta.com/app/folders/my/flows/`floId`` and paste it into the browser, then hit enter.
    If the flow does not immediately load, you can click on Execution History or Chart to get the flow to load correctly.
    You can also use this url format to navigate to any flow without having to know its folder too. All you need is the floId.
23. You can now view the flow that invoked the helper flow.

## Limitations and Issues
- Again, these APIs are internal and undocumented. Proceed with extreme caution when using.
- Cookie data is stored in plain-text within the flows to better show how the flopack works. It is however strongly recommended this data be saved in the API Connection with a `Custom` auth type or a custom connection built in order to make sure this information is not saved and readily accessible to others. 
- Parent flows that use a streaming card to invoke the helper flow return data differently in the execution history. The flopack may not work in that case.
- If the Parent flow was deleted, then you may only get errors and never be able to determine which flow invoked the helper flow.
- Okta Workflows stores a limited amount of execution history for each flow. If the execution is older then 30 days, it may not be possible to return any data.

