<img _ngcontent-c2="" src="https://avatars2.githubusercontent.com/u/31601407?s=70&amp;u=f3c6e1cfc8a26665e4a4df6d8da4a7ee527aeceb&amp;v=4" style="background-color: transparent;"> 

                   
 #  **API Changelog**



## October 13, 2025 
1.  FEATURE: Introduced the /v2/odds endpoint with support for team total alternate lines.
Only the team total data mode has changed; all other aspects of the response model remain unchanged.

2.  DEPRECATED: /v1/odds endpoint. End of Life: January 1, 2026.

3. FEATURE: Released Bets API v4. The main change: place-bet responses no longer include full bet details.

4. DEPRECATED: Bets API v3. End of Life: January 1, 2026.

## July 23, 2025 
1.  Rate limiting rules are updated.

## November 4, 2024 - Customer API 
1. DEPRECATED -`/v1/translations` endpoint has been deprecated and this feature no longer supported.

## October 7, 2024 - Lines API 
1. DEPRECATED -`/v1/inrunning` endpoint has been deprecated and this feature no longer supported.

## April 19, 2024 - Lines API 

1. FEATURE - Documented property `max` in the /odds/special  response. This property exposes contestant specific limits.
   
## November 18, 2022 - Lines API 

Historically we have offered Soccer Extra Time markets as distinct events with names like: “France (To Advance)”, “England (ET ONLY)”, “Brazil (PEN)”, “China (1st TEN PEN)”, “Spain (To Win Final)”. All of these markets are now offered as Periods of the [parent event live event](FAQ.md#how-to-find-associated-events). 

Special Note: Goals and Red Cards occurring in Extra Time are only returned in Period 3!

- Period 3 is Extra Time
- Period 6 is Penalty Shootout
- Period 7 1st Ten Shootout Pen
- Period 8 is To Qualify 
- Period 39 is To Win Final 

Consumers can expect to see Spread, Moneyline, Total and Team Totals priced in Period 3. Only Moneyline in Periods 6, 8, 39. Only Total in Period 7.


Sample Responses:
<details>
    <summary> Get Fixtures </summary>

```json	
{
    "sportId": 29,
    "last": 442452738,
    "league": [
        {
            "id": 218153,
            "name": "Zanzibar - Mapinduzi Cup",
            "events": [
                {
                    "id": 1563271322,
                    "starts": "2022-11-17T13:30:00Z",
                    "home": "TeamA",
                    "away": "TeamB",
                    "rotNum": "99552",
                    "liveStatus": 2,
                    "status": "O",
                    "parlayRestriction": 2,
                    "altTeaser": false,
                    "resultingUnit": "Regular",
                    "version": 442452541
                },
                {
                    "id": 1563271334,
                    "starts": "2022-11-17T13:30:00Z",
                    "home": "TeamA",
                    "away": "TeamB",
                    "rotNum": "99556",
                    "liveStatus": 1,
                    "status": "O",
                    "parlayRestriction": 1,
                    "parentId": 1563271322,
                    "altTeaser": false,
                    "resultingUnit": "Regular",
                    "version": 442452738
                }
            ]
        }
    ]
}
	
```
	
</details>
<details>
<summary>  Get In-Running </summary>
	
```json 
{
    "sports": [
        {
            "id": 29,
            "leagues": [
                    {
                    "id": 218153,
                    "events": [
                        {
                            "id": 1563271334,
                            "state": 3,
                            "elapsed": 23
                        }
                                ]
                    }
                        ]
        }
            ]
}
	
```
	
</details>
<details>
<summary>  Get Odds</summary>
	
```json 	
{
    "sportId": 29,
    "last": 1912670245,
    "leagues": [
        {
            "id": 218153,
            "events": [
                {
                    "id": 1563271334,
                    "awayScore": 1.0,
                    "homeScore": 1.0,
                    "awayRedCards": 1,
                    "homeRedCards": 0,
                    "periods": [
                        {
                            "lineId": 1912670188,
                            "number": 8,
                            "cutoff": "2022-11-17T17:45:51.367Z",
                            "maxMoneyline": 100.0,
                            "status": 1,
                            "moneylineUpdatedAt": "2022-11-17T14:34:49.527Z",
                            "moneyline": {
                                "home": -322.0,
                                "away": 212.0
                            }
                        },
                        {
                            "lineId": 1912670213,
                            "number": 3,
                            "cutoff": "2022-11-17T17:46:01.913Z",
                            "maxSpread": 100.0,
                            "maxMoneyline": 100.0,
                            "maxTotal": 100.0,
                            "status": 1,
                            "spreadUpdatedAt": "2022-11-17T14:34:51.603Z",
                            "moneylineUpdatedAt": "2022-11-17T14:34:51.603Z",
                            "totalUpdatedAt": "2022-11-17T14:34:51.603Z",
                            "spreads": [
                                {
                                    "hdp": -0.25,
                                    "home": -127.0,
                                    "away": -109.0
                                },
                                {
                                    "altLineId": 30710204111,
                                    "hdp": -1.0,
                                    "home": 404.0,
                                    "away": -823.0,
                                    "max": 100.0
                                },
                                {
                                    "altLineId": 30710204112,
                                    "hdp": -0.75,
                                    "home": 195.0,
                                    "away": -306.0,
                                    "max": 100.0
                                },
                                {
                                    "altLineId": 30710204113,
                                    "hdp": -0.5,
                                    "home": 129.0,
                                    "away": -185.0,
                                    "max": 100.0
                                },
                                {
                                    "altLineId": 30710204114,
                                    "hdp": 0.0,
                                    "home": -407.0,
                                    "away": 250.0,
                                    "max": 100.0
                                },
                                {
                                    "altLineId": 30710204115,
                                    "hdp": 0.25,
                                    "home": -724.0,
                                    "away": 371.0,
                                    "max": 100.0
                                }
                            ],
                            "moneyline": {
                                "home": 130.0,
                                "away": 497.0,
                                "draw": -109.0
                            },
                            "totals": [
                                {
                                    "points": 0.75,
                                    "over": -115.0,
                                    "under": -121.0
                                },
                                {
                                    "altLineId": 30710204123,
                                    "points": 0.5,
                                    "over": -170.0,
                                    "under": 119.0,
                                    "max": 100.0
                                },
                                {
                                    "altLineId": 30710204124,
                                    "points": 1.0,
                                    "over": 157.0,
                                    "under": -231.0,
                                    "max": 100.0
                                },
                                {
                                    "altLineId": 30710204125,
                                    "points": 1.25,
                                    "over": 218.0,
                                    "under": -350.0,
                                    "max": 100.0
                                },
                                {
                                    "altLineId": 30710204126,
                                    "points": 1.5,
                                    "over": 276.0,
                                    "under": -477.0,
                                    "max": 100.0
                                }
                            ],
                            "homeScore": 0.0,
                            "awayScore": 0.0,
                            "awayRedCards": 1,
                            "homeRedCards": 0
                        },
                        {
                            "lineId": 1912670245,
                            "number": 0,
                            "cutoff": "2022-11-17T17:45:41.93Z",
                            "maxSpread": 250.0,
                            "maxMoneyline": 125.0,
                            "maxTotal": 250.0,
                            "maxTeamTotal": 100.0,
                            "status": 1,
                            "spreadUpdatedAt": "2022-11-17T14:34:53.463Z",
                            "moneylineUpdatedAt": "2022-11-17T14:34:53.463Z",
                            "totalUpdatedAt": "2022-11-17T14:34:53.463Z",
                            "teamTotalUpdatedAt": "2022-11-17T14:34:53.463Z",
                            "spreads": [
                                {
                                    "hdp": -0.25,
                                    "home": 106.0,
                                    "away": -145.0
                                },
                                {
                                    "altLineId": 30710204552,
                                    "hdp": -0.75,
                                    "home": 287.0,
                                    "away": -487.0,
                                    "max": 250.0
                                },
                                {
                                    "altLineId": 30710204553,
                                    "hdp": -0.5,
                                    "home": 183.0,
                                    "away": -271.0,
                                    "max": 250.0
                                },
                                {
                                    "altLineId": 30710204554,
                                    "hdp": 0.0,
                                    "home": -488.0,
                                    "away": 294.0,
                                    "max": 250.0
                                }
                            ],
                            "moneyline": {
                                "home": 185.0,
                                "away": 725.0,
                                "draw": -181.0
                            },
                            "totals": [
                                {
                                    "points": 2.5,
                                    "over": 113.0,
                                    "under": -155.0
                                },
                                {
                                    "altLineId": 30710204564,
                                    "points": 2.75,
                                    "over": 173.0,
                                    "under": -254.0,
                                    "max": 250.0
                                },
                                {
                                    "altLineId": 30710204565,
                                    "points": 3.0,
                                    "over": 369.0,
                                    "under": -693.0,
                                    "max": 250.0
                                }
                            ],
                            "teamTotal": {
                                "home": {
                                    "points": 1.5,
                                    "over": 157.0,
                                    "under": -222.0
                                },
                                "away": {
                                    "points": 1.5,
                                    "over": 494.0,
                                    "under": -973.0
                                }
                            },
                            "homeScore": 1.0,
                            "awayScore": 1.0,
                            "awayRedCards": 1,
                            "homeRedCards": 0
                        }
                    ]
                }
            ]
        }
    ]
}
	
```
	
</details>

## October 7, 2022  - Lines API 

#### 1. <span style="background-color:green">DEPRECATED</span> -  Properties team1ScoreSets/team2ScoreSets are deprecated.

As a part of the tennis changes from September 12, 2022, properties `team1ScoreSets` and`team2ScoreSets` in `/fixtures/settled` endpoint are deprecated. 

The score for tennis matches works the same as for other sports, properties `team1Score` and`team2Score` show the score depending on the `resultingUnit` (`Games` or `Sets`) coming from the `/fixtures` endpoint.


## September  12, 2022  - Lines API 

#### 1. <span style="background-color:green">IMPROVEMENT</span> -  Tennis events trading.

Old Tennis markets are offered with the `Regular` `resultingUnit`, except for the Set Handicaps markets which have `Sets` `resultingUnit`. The Set Handicaps markets events had the resulting unit and the handicap points in the team names and are offered as Moneylines. 
The rest of the markets are not explicit as to whether or not they use the number of Sets or Games won by each player to determine their result.
New tennis events will start using proper `resultingUnit` and the Sets Handicaps markets will have handicap points removed from the team names and offered as spread markets.


In addition to the above changes to convey the 'resultingUnit' for each market, in Live we have historically offered all markets in Period 0 with the description of the Period in the Team Names. 
This has changed to use the period `number` of two events (one for each `resultingUnit`), see Example 2. 
The descriptions for Tennis Periods can be found with this call `/v1/periods?sportId=33`.


##### Example 1. Prematch Fixtures 

<details>
    <summary>Old fixtures snippet</summary>

 ```json
  
{
                    "id": 1504081918,
                    "starts": "2022-02-28T19:45:00Z",
                    "home": "Ana Konjuh",
                    "away": "Katie Boulter",
                    "rotNum": "8909",
                    "liveStatus": 0,
                    "status": "O",
                    "parlayRestriction": 2,
                    "altTeaser": false,
                    "resultingUnit": "Regular",
                    "version": 400671698
                },
                {
                    "id": 1504082301,
                    "starts": "2022-02-28T19:45:00Z",
                    "home": "Ana Konjuh (-1.5 Sets)",
                    "away": "Katie Boulter (+1.5 Sets)",
                    "rotNum": "8909",
                    "liveStatus": 0,
                    "status": "O",
                    "parlayRestriction": 2,
                    "parentId": 1504081918,
                    "altTeaser": false,
                    "resultingUnit": "Sets",
                    "version": 400671702
                },
                {
                    "id": 1504082299,
                    "starts": "2022-02-28T20:00:00Z",
                    "home": "Ana Konjuh (+1.5 Sets)",
                    "away": "Katie Boulter (-1.5 Sets)",
                    "rotNum": "8909",
                    "liveStatus": 0,
                    "status": "O",
                    "parlayRestriction": 2,
                    "parentId": 1504081918,
                    "altTeaser": false,
                    "resultingUnit": "Sets",
                    "version": 400675277
                }
  ```

</details>
 
<details>
    <summary>Old odds snippet</summary>

 ```json
 {
                    "id": 1504081918,
                    "periods": [
                        {
                            "lineId": 1601650790,
                            "number": 0,
                            "cutoff": "2022-02-28T19:45:00Z",
                            "maxSpread": 2500.0,
                            "maxMoneyline": 2500.0,
                            "maxTotal": 1250.0,
                            "maxTeamTotal": 500.0,
                            "status": 1,
                            "spreadUpdatedAt": "2022-02-28T18:07:50.317Z",
                            "moneylineUpdatedAt": "2022-02-28T18:33:07.623Z",
                            "totalUpdatedAt": "2022-02-28T18:03:52.817Z",
                            "teamTotalUpdatedAt": "2022-02-28T18:03:52.877Z",
                            "spreads": [
                                {
                                    "hdp": -3.5,
                                    "home": -113.0,
                                    "away": -105.0
                                },
                                {
                                    "altLineId": 24528340045,
                                    "hdp": -2.5,
                                    "home": -144.0,
                                    "away": 121.0,
                                    "max": 2500.0
                                },
                                {
                                    "altLineId": 24528340047,
                                    "hdp": -3.0,
                                    "home": -130.0,
                                    "away": 109.0,
                                    "max": 2500.0
                                },
                                {
                                    "altLineId": 24528340049,
                                    "hdp": -4.0,
                                    "home": 108.0,
                                    "away": -128.0,
                                    "max": 2500.0
                                },
                                {
                                    "altLineId": 24528340051,
                                    "hdp": -4.5,
                                    "home": 128.0,
                                    "away": -153.0,
                                    "max": 2500.0
                                }
                            ],
                            "moneyline": {
                                "home": -210.0,
                                "away": 184.0
                            },
                            "totals": [
                                {
                                    "points": 20.5,
                                    "over": -118.0,
                                    "under": -101.0
                                },
                                {
                                    "altLineId": 24528340044,
                                    "points": 21.5,
                                    "over": 105.0,
                                    "under": -125.0,
                                    "max": 1250.0
                                },
                                {
                                    "altLineId": 24528340046,
                                    "points": 21.0,
                                    "over": -104.0,
                                    "under": -114.0,
                                    "max": 1250.0
                                },
                                {
                                    "altLineId": 24528340048,
                                    "points": 20.0,
                                    "over": -138.0,
                                    "under": 116.0,
                                    "max": 1250.0
                                },
                                {
                                    "altLineId": 24528340050,
                                    "points": 19.5,
                                    "over": -153.0,
                                    "under": 128.0,
                                    "max": 1250.0
                                }
                            ],
                            "teamTotal": {
                                "home": {
                                    "points": 12.5,
                                    "over": 116.0,
                                    "under": -138.0
                                },
                                "away": {
                                    "points": 10.5,
                                    "over": -121.0,
                                    "under": 102.0
                                }
                            }
                        },
                        {
                            "lineId": 1601670164,
                            "number": 1,
                            "cutoff": "2022-02-28T19:45:00Z",
                            "maxMoneyline": 500.0,
                            "status": 1,
                            "moneylineUpdatedAt": "2022-02-28T18:58:10.25Z",
                            "moneyline": {
                                "home": -182.0,
                                "away": 155.0
                            }
                        }
                    ]
                },
                {
                    "id": 1504082301,
                    "periods": [
                        {
                            "lineId": 1601619622,
                            "number": 0,
                            "cutoff": "2022-02-28T19:45:00Z",
                            "maxMoneyline": 1250.0,
                            "status": 1,
                            "moneylineUpdatedAt": "2022-02-28T17:35:58.32Z",
                            "moneyline": {
                                "home": 107.0,
                                "away": -122.0
                            }
                        }
                    ]
                } 
 ```

</details>

New way shows the match using the new structure where the `resultingUnit` are explicit:

<details>
    <summary>New fixtures snippet</summary>

 ```json
{
    "sportId": 33,
    "last": 440033657,
    "league": [
        {
            "id": 2957,
            "name": "ATP Paris - R1",
            "events": [
                {
                    "id": 1562180480,
                    "starts": "2022-10-31T20:30:00Z",
                    "home": "Sebastian Korda",
                    "away": "Alex De Minaur",
                    "rotNum": "8325",
                    "liveStatus": 0,
                    "status": "O",
                    "parlayRestriction": 2,
                    "altTeaser": false,
                    "resultingUnit": "Sets", 
                    "version": 440033645
                },
                {
                    "id": 1562180497,
                    "starts": "2022-10-31T20:30:00Z",
                    "home": "Sebastian Korda (Games)",
                    "away": "Alex De Minaur (Games)",
                    "rotNum": "8325",
                    "liveStatus": 0,
                    "status": "O",
                    "parlayRestriction": 2,
                    "parentId": 1562180480,
                    "altTeaser": false,
                    "resultingUnit": "Games", 
                    "version": 440033657
                }
            ]
        }
    ]
}
 ```

</details>

<details>
    <summary>New odds snippet</summary>

 ```json
 {
	"sportId": 33,
	"last": 1894932080,
	"leagues": [
		{
			"id": 2957,
			"events": [
				{
					"id": 1562180480,
					"periods": [
						{
							"lineId": 1894801784,
							"number": 1,
							"cutoff": "2022-10-31T20:30:00Z",
							"maxMoneyline": 3000.0,
							"status": 1,
							"moneylineUpdatedAt": "2022-10-31T17:03:51.87Z",
							"moneyline": {
								"home": -130.0,
								"away": 109.0
							}
						},
						{
							"lineId": 1894801790,
							"number": 2,
							"cutoff": "2022-10-31T20:30:00Z",
							"maxMoneyline": 3000.0,
							"status": 1,
							"moneylineUpdatedAt": "2022-10-31T17:03:51.933Z",
							"moneyline": {
								"home": -131.0,
								"away": 110.0
							}
						},
						{
							"lineId": 1894932080,
							"number": 0,
							"cutoff": "2022-10-31T20:30:00Z",
							"maxSpread": 3000.0,
							"maxMoneyline": 4000.0,
							"maxTotal": 3000.0,
							"status": 1,
							"spreadUpdatedAt": "2022-10-31T19:33:13.17Z",
							"moneylineUpdatedAt": "2022-10-31T19:33:13.17Z",
							"totalUpdatedAt": "2022-10-31T19:33:13.17Z",
							"spreads": [
								{
									"hdp": -1.5,
									"home": 185.0,
									"away": -215.0
								},
								{
									"altLineId": 30378223926,
									"hdp": 1.5,
									"home": -342.0,
									"away": 284.0,
									"max": 3000.0
								}
							],
							"moneyline": {
								"home": -138.0,
								"away": 122.0
							},
							"totals": [
								{
									"points": 2.5,
									"over": 125.0,
									"under": -149.0
								}
							]
						}
					]
				},
				{
					"id": 1562180497,
					"periods": [
						{
							"lineId": 1894801794,
							"number": 1,
							"cutoff": "2022-10-31T20:30:00Z",
							"maxMoneyline": 3000.0,
							"status": 1,
							"moneylineUpdatedAt": "2022-10-31T17:03:52.12Z",
							"moneyline": {
								"home": -130.0,
								"away": 109.0
							}
						},
						{
							"lineId": 1894801795,
							"number": 2,
							"cutoff": "2022-10-31T20:30:00Z",
							"maxMoneyline": 3000.0,
							"status": 1,
							"moneylineUpdatedAt": "2022-10-31T17:03:52.153Z",
							"moneyline": {
								"home": -131.0,
								"away": 110.0
							}
						},
						{
							"lineId": 1894801797,
							"number": 0,
							"cutoff": "2022-10-31T20:30:00Z",
							"maxSpread": 3000.0,
							"maxTotal": 3000.0,
							"status": 1,
							"spreadUpdatedAt": "2022-10-31T17:03:52.183Z",
							"totalUpdatedAt": "2022-10-31T17:03:52.26Z",
							"spreads": [
								{
									"hdp": -1.5,
									"home": -111.0,
									"away": -103.0
								},
								{
									"altLineId": 30375816407,
									"hdp": -2.5,
									"home": 110.0,
									"away": -126.0,
									"max": 3000.0
								},
								{
									"altLineId": 30375816409,
									"hdp": -2.0,
									"home": -100.0,
									"away": -114.0,
									"max": 3000.0
								},
								{
									"altLineId": 30375816411,
									"hdp": -1.0,
									"home": -120.0,
									"away": 105.0,
									"max": 3000.0
								},
								{
									"altLineId": 30375816413,
									"hdp": -0.5,
									"home": -130.0,
									"away": 113.0,
									"max": 3000.0
								}
							],
							"totals": [
								{
									"points": 22.5,
									"over": -106.0,
									"under": -112.0
								},
								{
									"altLineId": 30375816408,
									"points": 21.5,
									"over": -139.0,
									"under": 116.0,
									"max": 3000.0
								},
								{
									"altLineId": 30375816410,
									"points": 22.0,
									"over": -122.0,
									"under": 102.0,
									"max": 3000.0
								},
								{
									"altLineId": 30375816412,
									"points": 23.0,
									"over": 105.0,
									"under": -125.0,
									"max": 3000.0
								},
								{
									"altLineId": 30375816414,
									"points": 23.5,
									"over": 116.0,
									"under": -138.0,
									"max": 3000.0
								}
							]
						}
					]
				}
			]
		}
	]
}
```
</details>

 

##### Example 2. Live Fixtures  


<details>
    <summary>Old fixtures snipet (with `Regular` `resultingUnit` and period descriptions in `home" and `away`)</summary>

 ```json
{
                    "id": 1504322998,
                    "starts": "2022-02-28T21:30:00Z",
                    "home": "Ana Konjuh",
                    "away": "Katie Boulter",
                    "rotNum": "10909",
                    "liveStatus": 1,
                    "status": "O",
                    "parlayRestriction": 1,
                    "parentId": 1504081918,
                    "altTeaser": false,
                    "resultingUnit": "Regular",
                    "version": 400699030
                },
                {
                    "id": 1504325436,
                    "starts": "2022-02-28T21:30:00Z",
                    "home": "Ana Konjuh To Win Set 1",
                    "away": "Katie Boulter To Win Set 1",
                    "rotNum": "10909",
                    "liveStatus": 1,
                    "status": "O",
                    "parlayRestriction": 1,
                    "parentId": 1504081918,
                    "altTeaser": false,
                    "resultingUnit": "Regular",
                    "version": 400699034
                },
                {
                    "id": 1504325437,
                    "starts": "2022-02-28T21:30:00Z",
                    "home": "Ana Konjuh To Win Set 2",
                    "away": "Katie Boulter To Win Set 2",
                    "rotNum": "10909",
                    "liveStatus": 1,
                    "status": "O",
                    "parlayRestriction": 1,
                    "parentId": 1504081918,
                    "altTeaser": false,
                    "resultingUnit": "Regular",
                    "version": 400699035
                },
                {
                    "id": 1504328314,
                    "starts": "2022-02-28T21:30:00Z",
                    "home": "Ana Konjuh Game 4 of Set 1",
                    "away": "Katie Boulter Game 4 of Set 1",
                    "rotNum": "10909",
                    "liveStatus": 1,
                    "status": "O",
                    "parlayRestriction": 1,
                    "parentId": 1504081918,
                    "altTeaser": false,
                    "resultingUnit": "Regular",
                    "version": 400699036
                },
                {
                    "id": 1504329654,
                    "starts": "2022-02-28T21:30:00Z",
                    "home": "Ana Konjuh Game 5 of Set 1",
                    "away": "Katie Boulter Game 5 of Set 1",
                    "rotNum": "10909",
                    "liveStatus": 1,
                    "status": "O",
                    "parlayRestriction": 1,
                    "parentId": 1504081918,
                    "altTeaser": false,
                    "resultingUnit": "Regular",
                    "version": 400699188
                },
                {
                    "id": 1504330259,
                    "starts": "2022-02-28T21:30:00Z",
                    "home": "Ana Konjuh Game 6 of Set 1",
                    "away": "Katie Boulter Game 6 of Set 1",
                    "rotNum": "10909",
                    "liveStatus": 1,
                    "status": "O",
                    "parlayRestriction": 1,
                    "parentId": 1504081918,
                    "altTeaser": false,
                    "resultingUnit": "Regular",
                    "version": 400699733
                },
                {
                    "id": 1504334716,
                    "starts": "2022-02-28T21:30:00Z",
                    "home": "Ana Konjuh Game 7 of Set 1",
                    "away": "Katie Boulter Game 7 of Set 1",
                    "rotNum": "10909",
                    "liveStatus": 1,
                    "status": "O",
                    "parlayRestriction": 1,
                    "parentId": 1504081918,
                    "altTeaser": false,
                    "resultingUnit": "Regular",
                    "version": 400700547
                },
                {
                    "id": 1504340108,
                    "starts": "2022-02-28T21:30:00Z",
                    "home": "Ana Konjuh Game 8 of Set 1",
                    "away": "Katie Boulter Game 8 of Set 1",
                    "rotNum": "10909",
                    "liveStatus": 1,
                    "status": "O",
                    "parlayRestriction": 1,
                    "parentId": 1504081918,
                    "altTeaser": false,
                    "resultingUnit": "Regular",
                    "version": 400700999
                }
            ]
        }
```
</details>


<details>
    <summary>Old odds snipet</summary>

 ```json
 {
                    "id": 1504322998,
                    "periods": [
                        {
                            "lineId": 1601797796,
                            "number": 0,
                            "cutoff": "2022-03-01T03:30:00Z",
                            "maxSpread": 3600.0,
                            "maxMoneyline": 3000.0,
                            "maxTotal": 3600.0,
                            "status": 1,
                            "spreadUpdatedAt": "2022-02-28T21:35:38.637Z",
                            "moneylineUpdatedAt": "2022-02-28T21:35:38.623Z",
                            "totalUpdatedAt": "2022-02-28T21:35:38.67Z",
                            "spreads": [
                                {
                                    "hdp": -4.5,
                                    "home": -115.0,
                                    "away": -104.0
                                },
                                {
                                    "altLineId": 24531258705,
                                    "hdp": -5.5,
                                    "home": 141.0,
                                    "away": -171.0,
                                    "max": 3600.0
                                },
                                {
                                    "altLineId": 24531258711,
                                    "hdp": -3.5,
                                    "home": -185.0,
                                    "away": 153.0,
                                    "max": 3600.0
                                }
                            ],
                            "moneyline": {
                                "home": -346.0,
                                "away": 297.0
                            },
                            "totals": [
                                {
                                    "points": 20.5,
                                    "over": -110.0,
                                    "under": -109.0
                                },
                                {
                                    "altLineId": 24531258704,
                                    "points": 19.5,
                                    "over": -154.0,
                                    "under": 127.0,
                                    "max": 3600.0
                                },
                                {
                                    "altLineId": 24531258710,
                                    "points": 21.5,
                                    "over": 110.0,
                                    "under": -134.0,
                                    "max": 3600.0
                                }
                            ]
                        }
                    ]
                },
                {
                    "id": 1504334716,
                    "periods": [
                        {
                            "lineId": 1601795550,
                            "number": 0,
                            "cutoff": "2022-03-01T03:30:00Z",
                            "status": 1,
                            "moneylineUpdatedAt": "2022-02-28T21:31:54.81Z"
			                 "moneyline": {
                            "home": -275.0,
                            "away":  240.0
                        }
                    ]
                },
                {
                    "id": 1504334716,
                    "periods": [
                        {
                            "lineId": 1504340108,
                            "number": 0,
                            "cutoff": "2022-03-01T03:30:00Z",
                            "status": 1,
                            "moneylineUpdatedAt": "2022-02-28T21:28:28.387Z"
			                 "moneyline": { 
                            "home": -125.0,
                            "away":  102.0
                        }
                    ]
                },
                {
                    "id": 1504325436,
                    "periods": [
                        {
                            "lineId": 1601797789,
                            "number": 0,
                            "cutoff": "2022-03-01T03:30:00Z",
                            "maxMoneyline": 1800.0,
                            "status": 1,
                            "moneylineUpdatedAt": "2022-02-28T21:35:38.59Z",
                            "moneyline": {
                                "home": -431.0,
                                "away": 369.0
                            }
                        }
                    ]
                },
                {
                    "id": 1504325437,
                    "periods": [
                        {
                            "lineId": 1601797791,
                            "number": 0,
                            "cutoff": "2022-03-01T03:30:00Z",
                            "maxMoneyline": 2700.0,
                            "status": 1,
                            "moneylineUpdatedAt": "2022-02-28T21:35:38.607Z",
                            "moneyline": {
                                "home": -218.0,
                                "away": 187.0
                            }
                        }
                    ]
                }
```
</details>


New way shows the match using the new structure where the `resultingUnit` are explicit and odds are offered on multiple periods ( not just period 0):
<details>
    <summary>New fixtures snipet</summary>

```json
{
    "sportId": 33,
    "last": 440033657,
    "league": [
        {
            "id": 2957,
            "name": "ATP Paris - R1",
            "events": [
                {
                    "id": 1562180480,
                    "starts": "2022-10-31T20:30:00Z",
                    "home": "Sebastian Korda",
                    "away": "Alex De Minaur",
                    "rotNum": "8325",
                    "liveStatus": 0,
                    "status": "O",
                    "parlayRestriction": 2,
                    "altTeaser": false,
                    "resultingUnit": "Sets", 
                    "version": 440033645
                },
                {
                    "id": 1562180497,
                    "starts": "2022-10-31T20:30:00Z",
                    "home": "Sebastian Korda (Games)",
                    "away": "Alex De Minaur (Games)",
                    "rotNum": "8325",
                    "liveStatus": 0,
                    "status": "O",
                    "parlayRestriction": 2,
                    "parentId": 1562180480,
                    "altTeaser": false,
                    "resultingUnit": "Games", 
                    "version": 440033657
                }
            ]
        }
    ]
}
```
</details>


<details>
    <summary>New odds snipet</summary>

```json
{
	"sportId": 33,
	"last": 1894932080,
	"leagues": [
		{
			"id": 2957,
			"events": [
				{
					"id": 1562180480,
					"periods": [
						{
							"lineId": 1894801784,
							"number": 1,
							"cutoff": "2022-10-31T20:30:00Z",
							"maxMoneyline": 3000.0,
							"status": 1,
							"moneylineUpdatedAt": "2022-10-31T17:03:51.87Z",
							"moneyline": {
								"home": -130.0,
								"away": 109.0
							}
						},
						{
							"lineId": 1894801790,
							"number": 2,
							"cutoff": "2022-10-31T20:30:00Z",
							"maxMoneyline": 3000.0,
							"status": 1,
							"moneylineUpdatedAt": "2022-10-31T17:03:51.933Z",
							"moneyline": {
								"home": -131.0,
								"away": 110.0
							}
						},
						{
							"lineId": 1894932080,
							"number": 0,
							"cutoff": "2022-10-31T20:30:00Z",
							"maxSpread": 3000.0,
							"maxMoneyline": 4000.0,
							"maxTotal": 3000.0,
							"status": 1,
							"spreadUpdatedAt": "2022-10-31T19:33:13.17Z",
							"moneylineUpdatedAt": "2022-10-31T19:33:13.17Z",
							"totalUpdatedAt": "2022-10-31T19:33:13.17Z",
							"spreads": [
								{
									"hdp": -1.5,
									"home": 185.0,
									"away": -215.0
								},
								{
									"altLineId": 30378223926,
									"hdp": 1.5,
									"home": -342.0,
									"away": 284.0,
									"max": 3000.0
								}
							],
							"moneyline": {
								"home": -138.0,
								"away": 122.0
							},
							"totals": [
								{
									"points": 2.5,
									"over": 125.0,
									"under": -149.0
								}
							]
						}
					]
				},
				{
					"id": 1562180497,
					"periods": [
						{
							"lineId": 1894801794,
							"number": 1,
							"cutoff": "2022-10-31T20:30:00Z",
							"maxMoneyline": 3000.0,
							"status": 1,
							"moneylineUpdatedAt": "2022-10-31T17:03:52.12Z",
							"moneyline": {
								"home": -130.0,
								"away": 109.0
							}
						},
						{
							"lineId": 1894801795,
							"number": 2,
							"cutoff": "2022-10-31T20:30:00Z",
							"maxMoneyline": 3000.0,
							"status": 1,
							"moneylineUpdatedAt": "2022-10-31T17:03:52.153Z",
							"moneyline": {
								"home": -131.0,
								"away": 110.0
							}
						},
						{
							"lineId": 1894801797,
							"number": 0,
							"cutoff": "2022-10-31T20:30:00Z",
							"maxSpread": 3000.0,
							"maxTotal": 3000.0,
							"status": 1,
							"spreadUpdatedAt": "2022-10-31T17:03:52.183Z",
							"totalUpdatedAt": "2022-10-31T17:03:52.26Z",
							"spreads": [
								{
									"hdp": -1.5,
									"home": -111.0,
									"away": -103.0
								},
								{
									"altLineId": 30375816407,
									"hdp": -2.5,
									"home": 110.0,
									"away": -126.0,
									"max": 3000.0
								},
								{
									"altLineId": 30375816409,
									"hdp": -2.0,
									"home": -100.0,
									"away": -114.0,
									"max": 3000.0
								},
								{
									"altLineId": 30375816411,
									"hdp": -1.0,
									"home": -120.0,
									"away": 105.0,
									"max": 3000.0
								},
								{
									"altLineId": 30375816413,
									"hdp": -0.5,
									"home": -130.0,
									"away": 113.0,
									"max": 3000.0
								}
							],
							"totals": [
								{
									"points": 22.5,
									"over": -106.0,
									"under": -112.0
								},
								{
									"altLineId": 30375816408,
									"points": 21.5,
									"over": -139.0,
									"under": 116.0,
									"max": 3000.0
								},
								{
									"altLineId": 30375816410,
									"points": 22.0,
									"over": -122.0,
									"under": 102.0,
									"max": 3000.0
								},
								{
									"altLineId": 30375816412,
									"points": 23.0,
									"over": 105.0,
									"under": -125.0,
									"max": 3000.0
								},
								{
									"altLineId": 30375816414,
									"points": 23.5,
									"over": 116.0,
									"under": -138.0,
									"max": 3000.0
								}
							]
						}
					]
				}
			]
		}
	]
}
```
</details>



## August  16, 2022  - Lines API 
##### 1. <span style="background-color:green">FEATURE</span>  - New period level properties for score and red cards  in  `/odds` response.  Supported only for Match (number=0) and Extra Time (number=3). 
  
 
## May  31, 2022  - Bets API 
##### 1. <span style="background-color:green">FEATURE</span>  - New property `resultingUnit`  in   `/bets` response.
  
## April  18, 2022  
   

New  call [rate limit](https://github.com/pinnacleapi/pinnacleapi-documentation#rate-limits) logic. 

 
## February  9, 2022  - Lines API 
##### 1. <span style="background-color:green">FEATURE</span>  - New properties `moneylineUpdatedAt`, `spreadUpdatedAt`, `totalUpdatedAt` and `teamTotalUpdatedAt`  in the `/v1/odds` and `/v1/odds/teaser` response.
 
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

  
