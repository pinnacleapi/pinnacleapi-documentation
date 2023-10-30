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

 
#### R Library
Please use the [pinnacle.API](https://cran.r-project.org/web/packages/pinnacle.API/index.html) package available on CRAN.  (install.packages(“pinnacle.API”))
The source code can be found [here](https://github.com/marcoblume/pinnacle.API).



# More ...

[Getting Started](GettingStarted.md)

[API Change Log](APIChangelog.md) 

[FAQ](FAQ.md)

[Fair Use Policy](FairUsePolicy.md)

# API Status
You can follow [pinnacle status page](https://status.pinnacle.com/) and subscribe to get the notifications on API status. Notifications will be sent from noreply@mg.pinnacle.com, make sure you check your junk inbox.

We are using Cloudflare as content delivery provider for the API, you can follow their status [here](https://www.cloudflarestatus.com/).


# Disclaimer

 Pinnacle is not liable for use of the API for any purpose. The API is provided on an “as is” and “as available” basis, without warranties of any kind, either expressed or implied, including, without limitation, implied warranties of merchantability and fitness for a particular purpose or non-infringement.

 
