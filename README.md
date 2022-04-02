# modeling-streaming-data-with-spark
#### what is steaming data 
<br> urgent to prcess + continous coming
#### challenges 
<br> new + late data
<br> solutions -> microbatches + intermediate state eg. avg of each microbatch abd append new data (windowing with time.) + watermarking 
#### lambda architecture 
<br> to mix streaing data with batches.
<br> ex when we meature suger in blood of person its streaming as if measure excceeed specific limit must tell us 
<br> also we wanna make some analyses on hist data to get avg/day and many other analyses.
#### drawbacks of lambda 
<br> duplication of work -> doing code for batches and online 
<br> different technologies to handle 
<br> difficult to maintain
#### drawbacks of core spark steaming 
<br> no read once grauntee
<br> dont support late data 
#### spark structured streaming 
<br> reaad once and only once gruanteed
<br> support late coming data.
<br> window (timecolumn,duration of window,window frequency)
<br> ex. window(eventTime,2,4)
<br> so ther will be agg on 2 window on time ex 1,2 - 2,3 - 3,4 
<br> if both sec and third arg are same so no window overlapping.
#### note 
<br> we can only sort by window or sort asln except on complete mode -> as it has all data 
#### using approperiate mode 
<br> no changes on data so its batches -> complete mode 
<br> new data are coming and dont handle late -> append mode 
<br> new data + late data -> update mode. 
#### using approperiate mode in case of grouping data 
<br> no grouping -> complete mode is not supported asln 
<br> as it will show whole data with each new line appended whitch dont make any sence 
<br> if we group by key -> append is not supported as append requirees that there is change must happens 
#### Trigger -> when to show output of data 
<br> immediate -> once MicroBatch is processed it will be outputed
<br> fixed time -> show result on specific timeframe eg. each 30 min 
<br> one shot -> manual so its on demand 
#### handling late data 
<br> we can just ignore it for very fast optimized pipleline
<br> process is for read once and consistency of the steam(recommended )
<br> we use waremark to handle it.
#### watermark 
<br> its max time to process late data 
#### limitation of waremark 
<br> one way gruantee : only gurantee that it will not ignore current data(note late) but may process late data too.
#### how to overcome limitation 
<br> 1- use update/append mode
<br> 2-use column of waremarking in grouping too (must be the same column.)
<br> what will happend --> once time goes on will not process late data (except first batch may have late data.)

#### handling failure
<br> write ahead log (default)
<br> check points (add it in code)
<br> query recovery (default.)
