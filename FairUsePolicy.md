
<img _ngcontent-c2="" src="https://avatars2.githubusercontent.com/u/31601407?s=70&amp;u=f3c6e1cfc8a26665e4a4df6d8da4a7ee527aeceb&amp;v=4" style="background-color: transparent;"> 

# Fair Use Policy


This API is protected by copyright laws and is provided only to our players, partners and affiliates.

The use of this resource is subject to our "Fair Use Policy" which is set out below.

Use of the API constitutes your agreement to this policy. You understand and agree that at our sole discretion, and without prior notice, we may block access to our site if we believe that your use of our site has violated or is inconsistent with this Fair Use Policy. 

We may at any time, and at our sole discretion, modify this Fair Use Policy, with or without prior notice. Any such modification will be effective immediately upon public posting. Your continued use of our APIs and this site following such modification constitutes your acceptance of the modified terms in this Fair Use Policy.

 

### Fair usage

The API is provided to players to facilitate wagering and may not be used for data gathering, scraping or for any other purpose. The API usage must be proportionate to wagering activities as determined on a case-by-case basis by Pinnacle.


Unless explicitly agreed in writing by Pinnacle, the commercial usage of the API will lead to the permanent suspension of your access.


You will not attempt, nor encourage others to:
- interfere with, disrupt, or disable any API features;
- use the API for commercial purposes without a written agreement with Pinnacle;
- sell, rent, lease, sublicense, redistribute, or syndicate the API to any third party without prior written approval from Pinnacle.

### Rules 
 
1. Delta and snapshot calls are supported in `/fixtures` and `/odds` endpoints.  Delta calls return changes since the provided  `since` value . For delta calls `since` parameter must not set to 0 or 1, it must always be set with the `last` value the previous call response. Snapshot calls return the current state and `since` parameter must not be provided at all.

2. Always first issue a snapshot call and continue with the delta calls. This would result in faster response time and smaller response payload, as a result, client will have get the odds/fixtures updates faster. 

3. Client must not call `/odds` or `/fixture` endpoint for each league or fixture in the loop.  If client is interested in certain leagues only,  `leagueIds` parameter must be set with all the league identifiers.


4. The following limitations must be observed for `/sports` call:
-  Requests made for the `/sports`  must be restricted to once every 60 minute. List of sports does not change often. The count of active events is obsolete functionality, that will eventually be decommissioned.  


5. The following limitations must be observed per sport:
- Snapshot call to `/fixtures` and `/odds` endpoints must be restricted to once every 60 seconds, regardless of the `leagueIds`, `eventIds` or `islive` paramaters.
- Delta calls to  `/fixtures` and `/odds` endpoints must be restricted to once every 5 seconds, regardless of the `leagueIds`, `eventIds` or `islive` paramaters.
- Calls to `/leagues` must be restricted to once every 60 minute.

6. Client must not call `/line` endpoint in the loop. The purpose of this endpoint is to check the price prior the bet placing.
