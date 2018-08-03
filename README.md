<img _ngcontent-c2="" src="https://avatars2.githubusercontent.com/u/31601407?s=70&amp;u=f3c6e1cfc8a26665e4a4df6d8da4a7ee527aeceb&amp;v=4" style="background-color: transparent;"> 


# Overview

Pinnacle API is a RESTful service for betting all bet types on all sports. 

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


# API Reference

**[Pinnacle API Open API Specification](https://github.com/pinnacleapi/OpenAPI-Specification)** is hosted on GitHub.

The API reference documentation:

**[Lines API](https://pinnacleapi.github.io/linesapi)**

**[Bets API](https://pinnacleapi.github.io/betsapi)**

**[Customer API](https://pinnacleapi.github.io/customerapi)**




# More ...

[Getting Started](GettingStarted.md)

[API Change Log](APIChangelog.md) 

[FAQ](FAQ.md)

[Fair Use Policy](FairUsePolicy.md)

# API Status
You can follow [pinnacle status page](https://status.pinnacle.com/) and subscribe to get the notifications on API status.  

# Libraries 
#### R
Please use the [pinnacle.API](https://cran.r-project.org/web/packages/pinnacle.API/index.html) package available on CRAN.  (install.packages(“pinnacle.API”))
The source code can be found [here](https://github.com/marcoblume/pinnacle.API).

# Disclaimer

 Pinnacle is not liable for use of the API for any purpose. The API is provided on an “as is” and “as available” basis, without warranties of any kind, either expressed or implied, including, without limitation, implied warranties of merchantability and fitness for a particular purpose or non-infringement.

 
