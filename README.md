<img _ngcontent-c2="" src="https://avatars2.githubusercontent.com/u/31601407?s=70&amp;u=f3c6e1cfc8a26665e4a4df6d8da4a7ee527aeceb&amp;v=4" style="background-color: transparent;"> 


# Overview

Pinnacle API is a RESTful service for betting all bet types on all sports. 

**Authentication**


The API uses HTTP Basic access authentication. Always use HTTPS to access the API.

You need to send HTTP Request header like this:
```
Authorization: Basic <Base64 value of UTF-8 encoded “username:password”> 
```

**Example**

```
Authorization: Basic U03MyOT23YbzMDc6d3c3O1DQ1 
```


Please note that in order to access Pinnacle API, you must have a funded account.

**Data Formats**

Pinnacle API supports only JSON format.
HTTP header `Accept` must be set:
```
    Accept: application/json
```
POST HTTP Request must have JSON body content and `Content-Type` HTTP header must be set:

```
    Content-Type: application/json
```

**Compression**

Pinnacle API supports HTTP compression. We strongly recommend using compression as it would give the best performance.

Please make sure to set the `User-Agent` HTTP header or compression might not work.

**Date Time Format**

All dates and times are in GMT time zone, ISO 8601 format

**Deduplication**

When a client issues a network request, it is always possible for the request to timeout or return an error status code indicating that the bet may not have been accepted. This opens up the possibility of the same request being sent more than once, which could create duplicate bets. Deduplication is a technique to avoid creating these duplicates when retrying a create request. We do the deduplication automatically for you.  

If the bet is accepted, we store the uniqueRequestId in the system for 30 min. If you try again within that time range to place a bet with the same uniqueRequestId, you will get the appropriate error.

All place bet requests support deduplication.


# API Reference

**[Pinnacle API Open API Specification](https://github.com/pinnacleapi/OpenAPI-Specification)** is hosted on github.

The API reference documentation:

**[Lines API](https://pinnacleapi.github.io/linesapi)**

**[Bets API](https://pinnacleapi.github.io/betsapi)**

**[Customer API](https://pinnacleapi.github.io/customerapi)**



### When is event's period open for betting? 


A period in an event is open for betting if in [Get Odds](https://pinnacleapi.github.io/linesapi#tag/Odds) response:
1. Period `status` = 1
2. Period has odds 
3. Period has `cutoff` is in the future.

Please note that for live events, odds change quite frequently as well as the period `status`, 
Due to these frequent changes, it’s possible that you will be getting status NOT_EXISTS in the Get Line response more often than for the pre-game events.



###  Betting on Events with Live Delay

Bets placed on events with live delay are treated differently than other bets. They get betId  assigned only once they are `ACCEPTED`.


The only way to find out the `status`  of such a bet is by querying  Get Bets V2 by `uniqueRequestIds`:

`/v2/bets?uniqueRequestIds=86a90ab9-fca1-4703-a11c-ce329a85584e`

As long as the bet is in `PENDING_ACCEPTANCE`, the response would be:

```json
{
    "straightBets": [
        {
            "uniqueRequestId": "86a90ab9-fca1-4703-a11c-ce329a85584e",
            "betStatus": "PENDING_ACCEPTANCE"
        }
    ]
}

```



NOTE: Status can change from `PENDING_ACCEPTANCE` to `NOT_ACCEPTED` or `ACCEPTED`


If the bet was `NOT_ACCEPTED`, the response would be:

```json

{
    "straightBets": [
        {
            "uniqueRequestId": "86a90ab9-fca1-4703-a11c-ce329a85584e",
            "betStatus": "NOT_ACCEPTED"
        }
    ]
}


```

If the bet was `ACCEPTED`, the response includes the full bet details:

```json

{
    "straightBets": [
        {
            "betId": 800110193,
            "uniqueRequestId": "86a90ab9-fca1-4703-a11c-ce329a85584e",
            "wagerNumber": 1,
            "placedAt": "2017-12-20T21:57:22Z",
            "betStatus": "ACCEPTED",
            "betType": "MONEYLINE",
            "win": 2519.25,
            "risk": 11991.63,
            "oddsFormat": "AMERICAN",
            "updateSequence": 175277412,
            "sportId": 29,
            "leagueId": 5595,
            "eventId": 799939900,
            "price": -476,
            "teamName": "Universitario",
            "team1": "Universitario",
            "team2": "Club Petrolero",
            "periodNumber": 0,
            "isLive": "TRUE"
        }
    ]
}
 
```

We apply live delay of around 6 seconds, so the first call to Get Bets V2 should be 6 seconds after placing a bet. 

30 minutes after placing a bet, we will stop returning a response for provided uniqueRequestId. This is due to cache cleanup to maintain optimal performance.

Please also note that the `RUNNING` bet list does not return any live delay bets that are `PENDING_ACCEPTANCE` or `NOT_ACCEPTED`.









 # Disclaimer

 Pinnacle is not liable for use of the API for any purpose. The API is provided on an “as is” and “as available” basis, without warranties of any kind, either expressed or implied, including, without limitation, implied warranties of merchantability and fitness for a particular purpose or non-infringement.

 
