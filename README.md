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

# Getting Started

##### Step 1 - Sign Up

To get started, you would need to create an account.

Please note that in order to access Pinnacle API, the account must be funded.


##### Step 2 - Get a List of Offered Sports and Leagues

You would need to get the list of sports from Get Sports operation. If you are interested in particular leagues, you can get all sport leagues by calling Get Leagues operation.

##### Step 3 - Place Bet 

To place a bet, please check the sections How to place a straight bet and How to place a parlay bet

##### Step 4 - Get Bets

To check the status of the placed bet, you need to call Get Bets operation. The recommended way is to use betId.



### How to Place a Straight Bet 

#####  Step 1 - Call Get Fixtures operation 

This will return the list of events that are currently offered. To get updates, use delta requests (with since parameter)


#####  Step 2 - Call Get Odds operation 

This will return the list of odds that are currently offered. To get updates, use delta requests (with since parameter)


##### Step 3 - Get Line (optional)

Call Get Line operation if you need exact limits or if you are interested in a specific line. Please note that the limits in the Get Odds response are general limits.


##### Step 4 - Place Bet

To place a bet, you need to call Place Bet operation.



Table shows how to do mapping of Get Odds operation response to Place Bet and Get Line request.


<table width="100%">
<tbody>
<tr><th width="30%"><strong>Parameter</strong></th><th width="70%"><strong>Get Odds response parameter</strong></th></tr>
<tr>
<td>sportId</td>
<td>sportId</td>
</tr>
<tr>
<td>leagueId</td>
<td>League Type -&gt; id</td>
</tr>
<tr>
<td>eventId</td>
<td>Event Type -&gt; id</td>
</tr>
<tr>
<td>periodNumber</td>
<td>Period Type -&gt; number</td>
</tr>
<tr>
<td>team</td>
<td>
<p>Depends on selected odds from:<br><br>· Spread Type<br>· Moneyline Type<br>· Team Total Points<br><br>check the value in the corresponding Get Leagues Response -&gt; League Type -&gt; homeTeamType and set the appropriate value.</p>
<p><strong>Example 1:</strong><br><br>Given:<br>&nbsp;&nbsp; &nbsp;homeTeamType="Team1"<br>When:<br>&nbsp;&nbsp; &nbsp;Selected odds is Spread Type -&gt; away<br>Then:<br>&nbsp;&nbsp; &nbsp;team=Team2<br><br><strong>Example 2:</strong></p>
<p>When:<br>&nbsp;&nbsp; &nbsp;Selected odds is Moneyline Type -&gt; draw<br>Then:<br>&nbsp;&nbsp; &nbsp;team=Draw<br><br><strong>Example 3:</strong><br><br>Given:<br>&nbsp;&nbsp; &nbsp;homeTeamType="Team2"<br>When:<br>&nbsp;&nbsp; &nbsp;Selected odds is Team Total Points Type -&gt; away<br>Then:<br>&nbsp;&nbsp; &nbsp;team=Team1</p>
</td>
</tr>
<tr>
<td>handicap</td>
<td>Spread Type -&gt; hdp<br>Total Points Type -&gt; points<br>Team Total Points Type -&gt; Total Points Type -&gt; points</td>
</tr>
<tr>
<td>lineId</td>
<td>Period Type -&gt; lineId</td>
</tr>
<tr>
<td>altLineId</td>
<td>Spread Type -&gt;altLineId<br>Total Points Type -&gt; altLineId <br><br></td>
</tr>
</tbody>
</table>

**IMPORTANT**: 
Maker sure you use both the `lineId` and `altLineId` from the Get Line or Get Odds response when placing a bet.
If you the price was for alternate line and you omit to set the `altLineId` parameter in the place bet request, the bet will be placed on the main line.


### How to Place a Parlay Bet 

##### Step 1 – Call Get Fixtures operation

This will return the list of events that are currently offered. To get updates use delta requests (with since parameter)

##### Step 2 – Call Get Odds operation

This will return the list of odds that are currently offered. To get updates use delta requests (with since parameter)

#####  Step 3 – Call Get Parlay Lines operation

For each event and bet type you want to bet on, construct a Leg object for Get Parlay Lines call and submit your request using: 
    POST /line/parlay
-> If response contains Invalid Legs – remove them and resubmit the request
-> If response has status = ‘VALID’ – place parlay bet request can be created

##### Step 4 – Call Place Parlay Bet

Construct a list of legs using lineId values from Get Parlay Lines response and specify roundRobbinOptions out of those retuned in Get Parlay Lines response.


### How to Place a Teaser Bet

##### Step 1 – Call Get Teaser Groups operation

This will return the list of teasers by group containing all the details for each teaser. For example; the minimum/maximum number of legs, payout combinations for the chosen teaser and leagues for each teaser.

##### Step 2 – Call Get Teaser Odds operation

This will return the list of adjusted points that are currently offered for the given teaser.
 
##### Step 3 – Optionally, call Get Teaser Lines operation

Prior to submitting a teaser bet you can call this endpoint to validate your proposed bet, calculate the effective minimum/maximum win/risk bet limits, as well as get the price you will receive for the bet without actually placing a bet.

##### Step 4 – Call Place Teaser Bet operation

Using the information obtained from the previous steps, build and place your bet.

### How to Place a Special Bet

##### Step 1 – Call Get Special Fixtures operation

This will return the list of specials that are currently offered. To get updates use delta requests (with since parameter)

##### Step 2 – Call Get Special Odds operation

This will return the list of special odds that are currently offered. To get updates use delta requests (with since parameter)
 
##### Step 3 – Optionally; call Get Special Lines operation

Prior to submitting a special bet, you can call this endpoint to validate your proposed bet, calculate the effective minimum/maximum win/risk bet limits, as well as get the price you will receive for the bet without actually placing a bet.

##### Step 4 – Call Place Special Bet operation

Using the information obtained from the previous steps, build and place your bet.

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




# Fair Use Policy


This API is protected by copyright laws and is provided free of charge only to our players, partners and affiliates.

The use of this free resource is subject to our "Fair Use Policy" which is set out below.

Use of the API constitutes your agreement to this policy. You understand and agree that at our sole discretion, and without prior notice, we may block access to our site if we believe that your use of our site has violated or is inconsistent with this Fair Use Policy. 

We may at any time, and at our sole discretion, modify this Fair Use Policy, with or without prior notice. Any such modification will be effective immediately upon public posting. Your continued use of our APIs and this site following such modification constitutes your acceptance of the modified terms in this Fair Use Policy.

 

### Fair usage

The API is provided to players to facilitate wagering and may not be used for data gathering, scraping or for any other purpose. The API usage must be proportionate to wagering activities as determined on a case-by-case basis by Pinnacle.


Unless explicitly agreed in writing by Pinnacle, the commercial usage of the API will lead to the permanent suspension of your access.


You will not attempt, nor encourage others to:
- interfere with, disrupt, or disable any API features;
- use the API for commercial purposes without a written agreement with Pinnacle;
- sell, rent, lease, sublicense, redistribute, or syndicate the API to any third party without prior written approval from Pinnacle.

The following limitations must be observed per sport:

- Requests made for the /fixtures and /odds operation without the since parameter must be restricted to once every 60 seconds;
- Requests made for the /fixtures and /odds operation with the since parameter must be restricted to once every 5 seconds.

 

### Best practice

Please use a delta /fixtures and /odds calls (with the since parameter) instead of a snapshot /fixtures and /odds calls (without since parameter).



# FAQ



##### How often can I refresh your odds?

Please check our fair use policy

##### How do I make sure my links to www.pinnacle.com are tracking correctly?

                   Please ensure that any links back to www.pinnacle.com are tagged with your tracking link. 
                   Your tracking links are available from your affiliate account accessed at http://affiliates.pinnacle.com
                   A correct tracking link will have the format:   http://affiliates.pinnacle.com/processing/clickthrgh.asp?btag=a_numbersb_numbers

##### Do you cache responses? For how long?

All feed command requests that have the same parameters (e.g. same client ID/API key/sport ID) are cached for 60 seconds.

##### Can I link directly to the relevant odds pages on www.pinnacle.com (deep linking)?

Yes. To link directly to our odds pages, please contact customerservice@pinnacle.com

##### How can I return only those sports and leagues which have data?

Get Sports and Get Leagues operations have the hasOfferings property that indicates availability of the markets.

##### How do you calculate maximum bet amounts for currencies other than USD?

We follow oanda.com, and update our exchange rates every 24 hours. Please note that for non-USD currencies, we round them to the largest integer less-than or equal-to the specified decimal number resulting from currency conversion. For example, a maximum bet amount of £345.23 would be rounded down to £345.

##### What time zone is used for the API?

In the feed, all times displayed are GMT.

##### How can I know if an event is deleted or settled?

Please use Get Settled Fixtures to find out if the event's period was settled or if the event was deleted.

##### How to get odds changes?

             1) Call the snapshot /odds (without the since parameter) - this would return cached odds snapshot
             2) Call the delta /odds (with the since parameter from the snapshot response) - to get all the changes since the snapshot.

  Delta response has only changed periods, with all the markets that are currently offered. For example, if we offer period 0 and period 1 odds on an event and there was a change in one of the markets in period 1, the delta call will have only period 1 with all the markets that we currently offer, not just the changed markets, and the period 0 will not be in the delta response.


Example:
    1) Snapshot has period 1 and period 0, and both of them have moneyline and spreads odds.
    2) Delta call returns just period 1 with the same moneyline and totals
 => This means that the period 0 did not have any changes, and on the period, 1 the spread is not offered anymore while the totals are offered now.

 # Disclaimer

 Pinnacle is not liable for use of the API for any purpose. The API is provided on an “as is” and “as available” basis, without warranties of any kind, either expressed or implied, including, without limitation, implied warranties of merchantability and fitness for a particular purpose or non-infringement.



 # Affiliates


##### How do I get access to the API as an affiliate?

In order to access the API as an affiliate, you are required to send 5 new funded signups from the previous 3 months. If you are unable to refer 5 new funded signups from the previous 3-month period, access to the API may be rescinded.
