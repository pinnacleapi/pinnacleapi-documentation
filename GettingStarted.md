<img _ngcontent-c2="" src="https://avatars2.githubusercontent.com/u/31601407?s=70&amp;u=f3c6e1cfc8a26665e4a4df6d8da4a7ee527aeceb&amp;v=4" style="background-color: transparent;"> 

# Getting Started

##### Step 1 - Get Approval to Access the API

Please note that Pinnacle API is not available to all customers. To request the access please contact [Pinnacle Solution](
https://www.pinnaclesolution.com/en/contact-us).


##### Step 2 - Get a List of Offered Sports and Leagues

You would need to get the list of sports from the Get Sports operation. If you are interested in particular leagues, you can get all sports leagues by calling the  Get Leagues operation.

##### Step 3 - Place Bet 

To place a bet, please check the below section [How to place a bet](#How_to_Place_a_Bet).

##### Step 4 - Get Bets

To check the status of the placed bet, you need to call Get Bets operation. The recommended way is to use `betIds` query parameter.



## How to Place a Bet

#### Straight Bet 

#####  Step 1 - Call Get Fixtures operation 

This will return the list of events that are currently offered. To get updates, use delta requests (with since parameter)


#####  Step 2 - Call Get Odds operation 

This will return the list of odds that are currently offered. To get updates, use delta requests (with since parameter)


##### Step 3 (Optional) - Get Line 

Call Get Line operation if you need exact limits or if you are interested in a specific line. Please note that the limits in the Get Odds response are general.

##### Step 4 - Place Bet

To place a bet you need to call Place Bet operation.



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
Make sure you use both the `lineId` and `altLineId` from the Get Line or Get Odds response when placing a bet.
If you the price was for alternate line and you omit to set the `altLineId` parameter in the place bet request, the bet will be placed on the main line.



#### Parlay Bet 

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

Construct a list of legs using lineId values from Get Parlay Lines response and specify roundRobbinOptions out of those returned in Get Parlay Lines response.


#### Teaser Bet

##### Step 1 – Call Get Teaser Groups operation

This will return the list of teasers by group containing all the details for each teaser. For example; the minimum/maximum number of legs, payout combinations for the chosen teaser and leagues for each teaser.

##### Step 2 – Call Get Teaser Odds operation

This will return the list of adjusted points that are currently offered for the given teaser.
 
##### Step 3 (Optional) – Call Get Teaser Lines operation

Prior to submitting a teaser bet you can call this endpoint to validate your proposed bet, calculate the effective minimum/maximum win/risk bet limits, as well as get the price you will receive for the bet without actually placing a bet.

##### Step 4 – Call Place Teaser Bet operation

Using the information obtained from the previous steps, build and place your bet.

#### Special Bet

##### Step 1 – Call Get Special Fixtures operation

This will return the list of specials that are currently offered. To get updates use delta requests (with since parameter)

##### Step 2 – Call Get Special Odds operation

This will return the list of special odds that are currently offered. To get updates use delta requests (with since parameter)
 
##### Step 3 (Optional) - Call Get Special Lines operation

Prior to submitting a special bet, you can call this endpoint to validate your proposed bet, calculate the effective minimum/maximum win/risk bet limits, as well as get the price you will receive for the bet without actually placing a bet.

##### Step 4 – Call Place Special Bet operation

Using the information obtained from the previous steps, build and place your bet.


