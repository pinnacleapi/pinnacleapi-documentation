<img _ngcontent-c2="" src="https://avatars2.githubusercontent.com/u/31601407?s=70&amp;u=f3c6e1cfc8a26665e4a4df6d8da4a7ee527aeceb&amp;v=4" style="background-color: transparent;"> 


# FAQ

### When is event's period open for betting? 

A period in an event is open for betting if in [Get Odds](https://pinnacleapi.github.io/linesapi#tag/Odds) response:
1. Period `status` = 1
2. Period has odds 
3. Period has `cutoff` is in the future.

Please note that for live events, odds change quite frequently as well as the period `status`, 
Due to these frequent changes, it’s possible that you will be getting status NOT_EXISTS in the Get Line response more often than for the pre-game events.



### How to place a bet on live events?

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







### How often can I refresh your odds?

Please check our fair use policy

### How do I make sure my links to www.pinnacle.com are tracking correctly?

Please ensure that any links back to www.pinnacle.com are tagged with your tracking link. 
Your tracking links are available from your affiliate account accessed at http://affiliates.pinnacle.com
A correct tracking link will have the format:   http://affiliates.pinnacle.com/processing/clickthrgh.asp?btag=a_numbersb_numbers

### Do you cache responses? For how long?

Get Odds and Get Fixtures snapshot calls are cached for 60 seconds. Get Odds and Get Fixtures delta calls are not cached.

### Can I link directly to the relevant odds pages on www.pinnacle.com (deep linking)?

Yes. To link directly to our odds pages, please contact customerservice@pinnacle.com

### How can I return only those sports and leagues which have data?

Get Sports and Get Leagues operations have the `hasOfferings` property that indicates availability of the markets.

### How do you calculate maximum bet amounts for currencies other than USD?

We follow oanda.com, and update our exchange rates every 24 hours. Please note that for non-USD currencies, we round them to the largest integer less-than or equal-to the specified decimal number resulting from currency conversion. For example, a maximum bet amount of £345.23 would be rounded down to £345.

### What time zone is used for the API?

All times are GMT.

### How can I know if an event is deleted or settled?

Please use Get Settled Fixtures to find out if the event's period was settled or if the event was deleted.

### How to get odds changes?

1) Call the snapshot /odds (without the since parameter) - this would return cached odds snapshot
2) Call the delta /odds (with the since parameter from the snapshot response) - to get all the changes since the snapshot.

  Delta response has only changed periods, with all the markets that are currently offered. For example, if we offer period 0 and period 1 odds on an event and there was a change in one of the markets in period 1, the delta call will have only period 1 with all the markets that we currently offer, not just the changed markets, and the period 0 will not be in the delta response.

Example:
    1) Snapshot has period 1 and period 0, and both of them have moneyline and spreads odds.
    2) Delta call returns just period 1 with the same moneyline and totals
 => This means that the period 0 did not have any changes, and on the period, 1 the spread is not offered anymore while the totals are offered now.
