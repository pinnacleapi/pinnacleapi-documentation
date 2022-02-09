<img _ngcontent-c2="" src="https://avatars2.githubusercontent.com/u/31601407?s=70&amp;u=f3c6e1cfc8a26665e4a4df6d8da4a7ee527aeceb&amp;v=4" style="background-color: transparent;"> 

                   
 #  **API Changelog**
 
## February  9, 2022  - Lines API 
##### 1. <span style="background-color:green">FEATURE</span>  - New properties `moneylineUpdatedAt`, `spreadUpdatedAt`, `totalUpdatedAt` and `teamTotalUpdatedAt`  in the `/v1/odds` response.
 
## February  18, 2021 
##### 1. <span style="background-color:green">FEATURE</span>  - Added new property `max` in the `/v1/odds` response, to return alternate market specific limits. 
##### 2. <span style="background-color:green">FEATURE</span>  - Added new endpoint `/v2/line/parlay`  to support round robin limits.
##### 3. <span style="background-color:red"> DEPRECATED</span>  -  `/v1/line/parlay`  and  `/v1/bets/parlay`  are deprecated, please switch to `/v2/line/parlay`  and `/v2/bets/parlay`  by March 18th 2021. Transition to `/v2/bets/parlay` version  is seamless, there are no data contract changes. Transition to `/v2/line/parlay` version requires small changes for parlay bets and a bit more for round robin bets .


 
## November 16, 2020 

##### 1. <span style="background-color:green">FEATURE</span>  - New property `contestants` in the `/v1/fixtures/special/settled` response, to return individual contestant outcomes.
 
## November 2, 2020 

##### 1. <span style="background-color:green">FEATURE</span>  - New properties `betStatus2` and `legBetStatus2` in the `/v3/bets` response. 
New properties are added to the straight and the parlay bets to support Asian handicap half won and half lost settlement.

## March 25, 2019 

`api.pinnaclesports.com` will not be supported after April 15, 2019. Please use `api.pinnacle.com` instead. 


 
## December 18, 2018 - Lines API 

##### 1. <span style="background-color:green">FEATURE</span>  - New property `liveStatus` in the `/v1/fixtures/special` response. 
Pinnacle will start offering live betting on specials soon, firstly on Esports. This property was introduce so that clients can differentiate live from pregame specials. Please note that live delay will be applied to betting on live specials. 

#### 2. <span style="background-color:green">IMPROVEMENT</span> -  All live events must have `parentId`.
When `parentId` was introduced we could not guarantee that all live events would have `parentId` set. In time we were able to consolidate the data and be able to guarantee that.

 
## December 5, 2018 - Bets API 

##### 1. <span style="background-color:green">FEATURE</span>  - New property `eventStartTime` for straight and special bets in the `/v3/bets` response.

 
## October 17, 2018 - Lines API 

##### 1. <span style="background-color:green">FEATURE</span>  - Added `handicap` parameter to  `line/special`.
As contestant's handicap is a mutable property,  it may happened that `line/special` returns `status`:`SUCCESS`, but with the different `handicap` from the one that client had at the moment of calling the  `line/special`. Now one can specify `handicap` parameter in the request and if the contestant's handicap changed, it would return `status`:`NOT_EXISTS`. This way  `line/special` is more aligned to how `/line` works.


## July 17, 2018 - Bets API 

##### 1. <span style="background-color:green">FEATURE</span>  - New properties `TeaserId` and `TeaserGroupId` for teaser bets in the `/bets` response.

##### 2. <span style="background-color:green">FEATURE</span>  - Bet object added to the `bets/parlay` , `bets/teaser` and `bets/special` response.

## June 7, 2018 - Bets API 

##### 1# <span style="background-color:green">FEATURE</span>  - New properties `price` and `finalPrice` for teaser bets  in the `/bets` response.
The `price` will be populated for all teaser bets and will be the original price on the time of placement.

The `finalPrice` will be populated only for `WON` bets and will indicate the price of bet resulting. It might be different from original price if one or more legs were pushed or canceled.


## June 6, 2018 - Lines API 

##### 1. <span style="background-color:green">FEATURE</span>  - New property `resultingUnit` in the `/fixtures` response.

`resultingUnit` specifies based on what unit the event will be resulted, e.g. corners, bookings 

##### 2. <span style="background-color:green">FEATURE</span>  - New property `status` in the `/odds` and `/odds/parlay/` response.

`status` specifies whether the period is online or offline for betting 

To determine if an event is open for betting, previously, clients were supposed to check the event status in /fixtures response.
Now you just need to check the `status` on the period.  
This would allow clients to speed up the decision-making process as there is no more need to frequently check the `/fixtures`. 

##### 3. <span style="background-color:green">FEATURE</span>  - New property `altHdp` in the `/odds/teaser` response.

`altHdp` specifies whether the spread is offered with the alternative handicap. Events with alternative teaser handicaps may vary from the teaser definition in `/teaser/groups`


 ## March 6, 2018 - Lines API 

 ##### 1. <span style="background-color:green">FEATURE</span>  - New property `parentId ` in the `/fixtures` response.

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

There is a pre-game parent event id 834342247, that has associated live event id 837721686, but also 2 corner events in different leagues, one for live betting (837721684), while the other one is for pre-game (837721615)

Introduction of parentid eliminates the need for rotation numbers. 

Please note that in the next version of `/fixtures`, the `rotNum` property will be decomissioned.


## January 4, 2018 - Lines API 

##### 1. <span style="background-color:red">BUGFIX</span>  When contestant line is no longer offered, delta `/odds/special` calls  will return contestant line with null price
##### 2. <span style="background-color:red">BUGFIX</span> `line/special` incorrectly returns successful response for offline events and when `cutoff` is in the past
##### 3. <span style="background-color:red">BUGFIX</span>  `line/special` returns {"status": "OFFLINE"} when a `price` is not set 
##### 4. <span style="background-color:red">BUGFIX</span> `/fixtures/settled` for tennis sometimes returns negative value for `team1ScoreSets` and `team2ScoreSets` fields


## December 21, 2017 - Lines API 
##### <span style="background-color:red">BUGFIX</span> - 1. `v1/fixtures/special`  eventId filtering not working


## October 11, 2017 - Bets API

Most important changes:
 * New property `fillType` gives more flexibility to the client when specifying stake amount.   
 * When betting on events with live delay, `betid` is not in the response 
 * Client has to use uniqueRequestId to check if the bet was accepted or not, by calling v2/bets?uniqueRequestIds={,}. 
 * For danger zone live betting, we still return `betId` in the response. 
 * In the case of a successful place bet call, we now return bet object. 
 * Status `NOT_ACCEPTED` is introduced as a replacement of `REJECTED`.  
 
 For more details, see https://pinnacleapi.github.io/betsapi#operation/Bets_StraightV2

 ##### 1. <span style="background-color:green">FEATURE</span>  - New operation `/v2/bets/straight`

 ##### 2. <span style="background-color:red">BUGFIX</span>  - Place bet operations return proper error in case of zero stake.

 ##### 3. <span style="background-color:orange">DECOMMISSIONING</span>  - `/v1/bets/place` will be decommissioned January 15, 2018. Please migrate to /v2/bets/straight 
 
 ##### 4. <span style="background-color:orange">DECOMMISSIONING</span>  - `/v1/bets` will be decommissioned January 15, 2018. Please migrate to /v2/bets 

  
