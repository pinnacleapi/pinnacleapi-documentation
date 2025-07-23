<img _ngcontent-c2="" src="https://avatars2.githubusercontent.com/u/31601407?s=70&amp;u=f3c6e1cfc8a26665e4a4df6d8da4a7ee527aeceb&amp;v=4" style="background-color: transparent;"> 


# Overview

Pinnacle API is a RESTful service for betting all bet types on all sports. 
```
api.pinnacle.com
``` 
Access to Pinnacle API suite has been closed for the general public since July 23rd, 2025. We offer bespoke data services for select high value bettors & commercial partnerships. We also support academics and pregame handicapping projects. To apply for access please write a short description of your use case to api@pinnacle.com.  Our team will get back to you with options.

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

 
 
### Rules 
 
1. Delta and snapshot calls are supported in `/fixtures`, `/fixtures/special` , `/odds` and `/odds/special`  endpoints.  Delta calls return changes since the provided  `since` value. For delta calls, `since` parameter must not be set to 0 or 1, it must always be the value of the  `last` property from the previous response. Snapshot calls return the current state,  `since` parameter must not be provided for snapshot calls.

2. Always issue a snapshot call first, then proceed with delta calls. This yields faster response times and smaller payloads, so your client will receive odds and fixture updates more quickly.

3. The client must not call the `/odds` or `/fixture` eendpoints in a loop for each sport, league, or fixture. If you’re interested in certain leagues only, include all their IDs in the `leagueIds` pparameter in a single call. Likewise, if you need specific events, include all their IDs in the  `eventIds` parameter together.

4. For the `/sports` call: requests must be limited to once every 60 minutes. The list of sports rarely changes, and the “active events” count is obsolete functionality that will eventually be removed.

5. The client must not call the `/line` endpoint in a loop. This endpoint exists solely to check a price prior to placing a bet.

6. IP Restrictions: Access to the entire API is restricted to a maximum of 2 distinct IP addresses per client.

### Rate Limiting

All API endpoints that expose odds data are subject to strict rate limiting:

/v1/odds

/v1/odds/special

/v1/odds/parlay

/v2/odds

/v1/line

/v1/line/special

/v1/line/parlay

 
**Request Rate Limit**: 1 request per 2 minutes, per endpoint, per sportId.

Requests exceeding the allowed rate will result in 429 HTTP error:


``` http

HTTP/1.1 429 Too Many Requests
Content-Type: application/json
{
  "code": "TOO_MANY_REQUESTS",
  "message": "Notice of Excessive Request Activity"
}
```


# More ...

[Getting Started](GettingStarted.md)

[API Change Log](APIChangelog.md) 

[FAQ](FAQ.md)

[Fair Use Policy](FairUsePolicy.md)


# Disclaimer

 Pinnacle is not liable for use of the API for any purpose. The API is provided on an “as is” and “as available” basis, without warranties of any kind, either expressed or implied, including, without limitation, implied warranties of merchantability and fitness for a particular purpose or non-infringement.

 
