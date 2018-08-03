<img _ngcontent-c2="" src="https://avatars2.githubusercontent.com/u/31601407?s=70&amp;u=f3c6e1cfc8a26665e4a4df6d8da4a7ee527aeceb&amp;v=4" style="background-color: transparent;"> 

                   
 #  **API Changelog**

## July 17th , 2018 - Bets API 

##### 1# <span style="background-color:green">FEATURE</span>  - New properties `TeaserId` and `TeaserGroupId` for teaser bets  in the `/bets` response.

##### 2# <span style="background-color:green">FEATURE</span>  - Bet object added to the `bets/parlay` , `bets/teaser`  and `bets/special`  response.


## June 7th , 2018 - Bets API 

##### 1# <span style="background-color:green">FEATURE</span>  - New properties `price` and `finalPrice` for teaser bets  in the `/bets` response.
The `price` will be populated for all teaser bets and will be the original price on the time of placement.
The `finalPrice` will be populated only for `WON` bets and will indicate the price of bet resulting. It might be different from original price if one or more legs were pushed or canceled.

## June 6, 2018 - Lines API 

##### 1# <span style="background-color:green">FEATURE</span>  - New property `resultingUnit` in the `/fixtures` response.

`resultingUnit` specifies based on what unit the event will be resulted, e.g. corners, bookings 


#####  2# <span style="background-color:green">FEATURE</span>  - New property `status` in the `/odds` and `/odds/parlay/` response.

`status` specifies whether the period is online or offline for betting 

To determine if an event is open for betting , previously clients were supposed to check the event status  in /fixtures response.
Now you just need to check the `status` on the period.  
This would allow clients to speed up the decision process as there is now more need to frequently check the `/fixtures`. 

#####  3# <span style="background-color:green">FEATURE</span>  - New property `altHdp` in the `/odds/teaser` response.

`altHdp` specifies whether the spread is offered with the alternative handicap. Events with alternative teaser handicaps may vary from the teaser definition in `/teaser/groups`


 ## March 6th, 2018 - Lines API 

 #####  1# <span style="background-color:green">FEATURE</span>  - New property `parentId ` in the `/fixtures` response.


 `parentId` can be used to group associated events to the "parent" pre-game event, like in the example below:
 ``` json
 {
    "sportId": 29,
    "last": 148671597,
    "league": [
        {
            "id": 2331,
            "name": "Norway - 1st Division",
            "events": [
                {
                    "id": 837721686,
                    "starts": "2018-04-10T17:00:00Z",
                    "home": "Viking Fk",
                    "away": "Mjondalen",
                    "rotNum": "6751",
                    "liveStatus": 1,
                    "status": "O",
                    "parlayRestriction": 2,
                    "parentId": 834342247,
                    "altTeaser": false
                },
                {
                    "id": 834342247,
                    "starts": "2018-04-10T17:00:00Z",
                    "home": "Viking Fk",
                    "away": "Mjondalen",
                    "rotNum": "6751",
                    "liveStatus": 2,
                    "status": "I",
                    "parlayRestriction": 2,
                    "altTeaser": false
                }
            ]
        },
        {
            "id": 6816,
            "name": "Norway - 1st Division Corners",
            "events": [
                {
                    "id": 837721684,
                    "starts": "2018-04-10T17:00:00Z",
                    "home": "Viking Fk (Corners)",
                    "away": "Mjondalen (Corners)",
                    "rotNum": "6751",
                    "liveStatus": 1,
                    "status": "O",
                    "parlayRestriction": 1,
                    "parentId": 834342247,
                    "altTeaser": false
                },
                {
                    "id": 837721615,
                    "starts": "2018-04-10T17:00:00Z",
                    "home": "Viking Fk (Corners)",
                    "away": "Mjondalen (Corners)",
                    "rotNum": "6751",
                    "liveStatus": 2,
                    "status": "I",
                    "parlayRestriction": 1,
                    "parentId": 834342247,
                    "altTeaser": false
                }
            ]
        }
    ]
} 
```

There is a pre-game parent event id 834342247, that has associated live event id 837721686, but also 2 corner events in different league, one for live betting (
837721684), while the other one for pre-game (837721615)
Introduction of parentid eliminates a need for rotation numbers. 

Please note that in the next version of `/fixtures`, `rotNum` property will be decomissioned.

 
## January 4th, 2018 - Lines API 

##### <span style="background-color:red">BUGFIX</span> - 1# When contestant line is no longer offered, delta `/odds/special` calls  will return contestant line with null price
##### <span style="background-color:red">BUGFIX</span> - 2# `line/special` incorrectly returns successful response for offline events and when `cutoff` is in the past
##### <span style="background-color:red">BUGFIX</span> - 3# `line/special` returns {"status": "OFFLINE"} when a `price` is not set 
##### <span style="background-color:red">BUGFIX</span> - 4# `/fixtures/settled` for tennis sometimes returns negative value for `team1ScoreSets` and `team2ScoreSets` fields

 

## December 21st, 2017 - Lines API 
##### <span style="background-color:red">BUGFIX</span> - 1# `v1/fixtures/special`  eventId filtering not working


## October 11th, 2017 - Bets API 

 #####  1# <span style="background-color:green">FEATURE</span>  - New operation `/v2/bets/straight`.

 Most important changes:
 * New property `fillType` gives more flexibility to the client when specifying stake amount.   
 * When betting on events with live delay, `betid` is not in the response 
 * Client has to use uniqueRequestId to check if the bet was accepted or not, by calling v2/bets?uniqueRequestIds={,}. For danger zone live betting, we still return `betId` in the response. 
 In case of successful place bet call, we return bet object now. 
 * Status `NOT_ACCEPTED` is introduced as a replacement of `REJECTED`.  
 
 For more details see https://pinnacleapi.github.io/betsapi#operation/Bets_StraightV2

 #####  1# <span style="background-color:red">BUGFIX</span>  - Place bet operations return proper error in case of zero stake.

 #####  1# <span style="background-color:orange">DECOMMISSIONING</span>  - `/v1/bets/place` will be decommissioned January 15th 2018 , please migrate to /v2/bets/straight 
 #####   1# <span style="background-color:orange">DECOMMISSIONING</span>  - `/v1/bets` will be decommissioned January 15th 2018 , please migrate to /v2/bets

  
