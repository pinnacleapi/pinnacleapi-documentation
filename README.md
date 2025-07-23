<img _ngcontent-c2="" src="https://avatars2.githubusercontent.com/u/31601407?s=70&amp;u=f3c6e1cfc8a26665e4a4df6d8da4a7ee527aeceb&amp;v=4" style="background-color: transparent;"> 


# Overview

Pinnacle API is a RESTful service for betting all bet types on all sports. 
```
api.pinnacle.com
```


Please note that in order to access Pinnacle API you must contact [Pinnacle Solution](
https://www.pinnaclesolution.com/en/contact-us) for the approval.


#### Authentication 


The API uses HTTP Basic access authentication. Always use HTTPS to access the API.

You need to send HTTP Request header like this:
```
Authorization: Basic <Base64 value of UTF-8 encoded “username:password”> 
```

Example:

```
Authorization: Basic U03MyOT23YbzMDc6d3c3O1DQ1 
```


Please note that in order to access Pinnacle API, you must have a funded account.

#### Data Formats 

Pinnacle API supports only JSON format.
HTTP header `Accept` must be set:
```
    Accept: application/json
```
POST HTTP Request must have JSON body content and `Content-Type` HTTP header must be set:

```
    Content-Type: application/json
```

#### Compression 

Pinnacle API supports HTTP compression. We strongly recommend using compression as it would give the best performance.

Please make sure to set the `User-Agent` HTTP header or compression might not work.

#### Date Time Format 

All dates and times are in GMT time zone, ISO 8601 format

#### Deduplication

When a client issues a network request, it is always possible for the request to timeout or return an error status code indicating that the bet may not have been accepted. This opens up the possibility of the same request being sent more than once, which could create duplicate bets. Deduplication is a technique to avoid creating these duplicates when retrying a create request. We do the deduplication automatically for you.  

If the bet is accepted, we store the `uniqueRequestId` in the system for 30 min. If you try again within that time range to place a bet with the same `uniqueRequestId`, you will get the appropriate error.

All place bet requests support deduplication.




## API Reference

##### Customer API

[v1](https://redocly.github.io/redoc/?url=https://raw.githubusercontent.com/pinnacleapi/openapi-specification/master/customerapi-oas.yaml&nocors) - Current

##### Lines API

 **[v2](https://redocly.github.io/redoc/?url=https://raw.githubusercontent.com/pinnacleapi/openapi-specification/master/linesapi-oas.yaml&nocors)** - Current

##### Bets API

**[v3](https://redocly.github.io/redoc/?url=https://raw.githubusercontent.com/pinnacleapi/openapi-specification/master/betsapi-oas.yaml&nocors)** - Deprecated

**[v4](https://redocly.github.io/redoc/?url=https://raw.githubusercontent.com/pinnacleapi/openapi-specification/master/betsapi.v4-oas.yaml&nocors)** - Current

 
 
### Rules and Rate Limits
 
1. Delta and snapshot calls are supported in `/fixtures`, `/fixtures/special` , `/odds` and `/odds/special`  endpoints.  Delta calls return changes since the provided  `since` value. For delta calls `since` parameter must not be set to 0 or 1, it must be always set with the `last` property value of the previous call response. Snapshot calls return the current state,  `since` parameter must not be provided for snapshot calls.

2. Always first issue a snapshot call and continue with the delta calls. This would result in a faster response time and a smaller response payload. As a result, the client will   get the odds/fixtures updates faster. 

3. Client must not call `/odds` or `/fixture` endpoint for each sport league or fixture in the loop.  If the client is interested in certain leagues only,  `leagueIds` parameter must be set with all the league identifiers. 
 Same for the `eventIds` parameter, the client should use it only if interested in specific events in which case all event identifiers must be provided in the same call. 


4. The following limitations must be observed for `/sports` call:
-  Requests made for the `/sports`  must be restricted to once every 60 minute. List of sports does not change often. The count of active events is obsolete functionality, that will eventually be decommissioned.  


5. The following limitations must be observed per sport:
- Snapshot call to `/fixtures` and `/odds` endpoints must be restricted to once every 120 seconds, regardless of the `leagueIds`, `eventIds` or `islive` parameters.
- Delta calls to  `/fixtures` and `/odds` endpoints must be restricted to once every 120 seconds, regardless of the `leagueIds`, `eventIds` or `islive` parameters.
- Calls to `/leagues` must be restricted to once every 60 minutes.

6. Client must not call `/line` endpoint in the loop. The purpose of this endpoint is to check the price prior to the bet placing.




#### Rate Limits


To enforce the [Fair Use Policy](FairUsePolicy.md#rules) and ensure stable service to all the clients we have API rate limits in place, a number of API calls clients can make within a given time period.

If the limit is exceeded, the client may get the error response HTTP status code `429`, with HTTP header `Retry-After` that specifies after how many seconds the client can retry.

Example:

```
HTTP/1.1 429 Too Many Requests
Content-Type: application/json
Content-Length: 240
Retry-After: 60
 
{
"code": "TOO_MANY_REQUESTS",
"message": "Too many snapshot requests. For more details see https://github.com/pinnacleapi/pinnacleapi-documentation#rate-limits
}

```



`Lines API` snapshot calls are limited, up to 1 call per minute per sport per endpoint. Following endpoints support snapshots:

* /fixtures
* /fixtures/special 
* /odds
* /odds/special 


Examples of snapshot calls that are counted towards the same sport-endpoint call rate counter:

* /v1/fixtures?sportid=29 
* /v1/fixtures?sportid=29&islive=1 
* /v1/fixtures?sportid=29&leagueIds=1980,5487,2627
* /v1/fixtures?sportid=29&eventIds=1550526772,1550667755&currencycode=EUR

 


# More ...

[Getting Started](GettingStarted.md)

[API Change Log](APIChangelog.md) 

[FAQ](FAQ.md)

[Fair Use Policy](FairUsePolicy.md)


# Disclaimer

 Pinnacle is not liable for use of the API for any purpose. The API is provided on an “as is” and “as available” basis, without warranties of any kind, either expressed or implied, including, without limitation, implied warranties of merchantability and fitness for a particular purpose or non-infringement.

 
