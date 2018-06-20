<img _ngcontent-c2="" src="https://avatars2.githubusercontent.com/u/31601407?s=70&amp;u=f3c6e1cfc8a26665e4a4df6d8da4a7ee527aeceb&amp;v=4" style="background-color: transparent;"> 


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
