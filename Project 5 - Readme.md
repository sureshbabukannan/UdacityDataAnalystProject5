# Airlines On-time Performance Data 
----------------------------------- 

### by Sureshbabu K


## Flight On-time Performance data

> The US Department of Transport Bureau of Statistics publishes Flight on-time data monthly. The dataset primary shows the timeliness of flights, their origin and destination details. Further details about the dataset can be found at https://www.transtats.bts.gov/Fields.asp The data is available at https://www.transtats.bts.gov/DL_SelectFields.asp for public to download.  

> For this Analysis the latest data available from the above sites is considered, Jan to Jun 2019 data has been downloaded in 6 different monthly comma separated files are used for analysis. 

> The dataset is has main sections of data with data fields related to the section 
     >>* Time Period  
     >>>    * Year 
     >>>    * Quarter 
     >>>    * Month 
    >>>    * Day of the Month 
    >>>    * Day of the Week 
    >>>    * Flight Date 
     >>* Airline 
     >>> * Detailed Airlines company and Flight  
     >>> * Origin 
     >>> * Details of originating City and Airport  
     >>> * Destination 
     >>> * Details of Destination City and Airport  
     >>*Departure Performance 
     >>> * departure time  
     >>> * Planned departure time 
     >>*Arrival Performance 
     >>> * Arrival time delay  
     >>> * Planned Arrival time 
     >>* Cancellation and Diversions  
     >>> * Indicators of cancelled and Diverted flights 
     >>* Flight Details 
     >>> * Planned departure time 
     >>> * Planned Arrival time 
     >>> * Distance 
     >>> * Taxi In time 
     >>> * Taxi Out time 
     >>* Cause of delay Categories 
     >>* Gate return to origin Airport details 
     >>* Diverted flight details  

> Further to the data fields are categorical field like 
     >> * Delay Time block - The hour duration of the day like 1900-1959  
     >> * Delay Time Group - Blocks of every 15 min , 0-15 is 0 and 0-30 is 1 and so on, to indicate the severity of the delay.  
     >> * Distant Group - The blocks of 250 kms is indicated as distant group. First 250 kms is 1 and upto 500 kms is 2 and so on.  
     >> * Delay in minutes due to each Categories of delay is shown separately to show all causes of delay, like NAS, SECURITY, LATE AIRCRAFT, CARRIER DELAY, WEATHER DELAY. 
The focus of the analysis is to find out what are the primary cause of delay. At the onset some variables like day of the week, time of the day, routes, Destination, Routes, Flight Number and Individual Aircraft could be cause of the delays. On this basis I set to analyse the cause of the delay.  

By Common sense we could also say weather could cause the most delay and NAS technical reasons. We could see by further doing the analysis. 


## Summary of Findings

> The delay due to cancellations and Diversions is quite evident and the data could skew the findings of delay of other cancelled and Diverted flights. So the cancelled and diverted flights are not considered for analysis. 

> The data is consolidated from 6 seperate monthly file into 1 dataset and loaded to a padas dataframe df_H12019 for analysis.  
>> * The Univariate analysis and Bivariate analysis is done on  
>>> * Arrival and Departure delay minutes 
>>> * Time of the day blocks for Arrival and Departures delay minutes. 
>>> * Day of the week for Arrival and Departures delay minutes. 
>>> * Cause of the delay categories 

> Findings from the analysis 
>> * **Departure and Arrival Delays** Most of the flights take of early or on-time but we are more interested in delays.  
>> * The Departure delays and arrival delay seems to closely related. This could be due to departure delay causes arrival delay. 45 mins, 1 hour, 1.5 hours and more than 2.5 hours delays seems to be quite common.  
>> * Arrival Delay and Departure delays are plotted. On Analysing the Minute wise delays, It is found that spike at -3 minutes which means most flights depart earlier. But also a spike at 12 minutes delay. 
>> * On analysis of **Day of the week**, Interestingly it is found that 15 minutes are more delays are on Wednesday and Thursdays followed by Saturdays and Sundays and on Fridays have least delays.   
>> * The Time of the day blocks of Departure delays of 15 minutes are more shows left skewed peaking at 5.00 pm to 7.00 pm. Arrival departures similarly seem late in the day peaking at 9.00 pm.  
>> * The arrival delays on distribution is different from departure distribution, more delay are see towards end of the day between 4 pm to 10 pm. The least delay observed in morning arrival flights. There is difference in departure and arrival delay patterns. 
>> * **Cause of Delay** Each flight data has minutes of attributable to each category of delay. The analysis of is done for  
>>> * when 15 minutes or more Arrival delay with no Departue delays  Prominent reason is NAS delay .i.e is due to Air traffic congestion at airport. 
>>> * When there is 15 minutes or more delay in both Departure and Arrival the primary cause is due to late arrival of airport and followed by Carrier Delays. 
>> * Both arrival and departure delay minutes are fairly normally distributed and does not require any transformations. 

>> * A scatter plot of created with numeric variables of the dataset. On closer examination of picture of the scatterplot there are no surprising relationships emerge, only common sense natural relationship are seen.  
>>> * Heat map is plotted understand the correlations. We could only see all natural co-relations. 
>>>> 1. Actual Elapsed Time vs Airtime   
>>>> 2. Acutal Elapsed Time vs CRS Elapsed Time 
>>>> 3. Acutal Elapsed Time vs Distance 
>>>> 4. Air-Time vs Distance 
>>>> 5. Air-Time vs CRS-elapsed-time 
>>>> 6. Arr-delay vs Departure-Delay 
>>>> 7. CRS Elapsed Time vs distance 
>>>> 8. Departure time vs Wheels off 
>>>> 9. Departure time vs Wheels on 
>>>> 10.  Wheels on vs Wheels off   

>> * Heat map is plotted for other pairwise relationships of Arrival delay minutes by airports to understand if there are any relationship. Again only  
natural relationships are observed. 
>>> * It is observed that departure and Arrival delays are highly related. Co-relation coefficient at **~0.97** 
>>> * Carrier delay and Late Aircraft delays and are fairly related to Arrival and Departure delays , correlation coefficient at **0.63** 

>> * Next Arrival Delay minutes by Airport is plotted as bar plot. As there were more than 3000 airports to make better sense only airports with **total delay minutes greater than 10000** is plotted.  
>>> * ORD - Chicago  and DFW - Dallas Aiport has total Arrival delay top 2 delay  
minutes. 
>> * Another strip plot is created to General distribution of delay minutes for US Airports causing total delay over 100k minutes in H1 2019.   
>>> * It is observed that there high numbers of delays below 60 minutes,  But there are some outlier seen where delays are more than 2000 minutes. 
>> * A violin plot is confirms that that the mean and quartiles lies with in 60 minutes time but there are many out-liers making the total delay minutes extremely high. 
>> * To further narrow down, a point plot of Arrival Delay in US airport within 60 minutes is created.  It is observed that the **mean arrival delay minutes are 5 minutes and standard deviation is around 15 minutes**.  
>> * A point plot is created to for more then 60 arrival minutes total arrival delay, It is observed that mean arrival **delay minutes is 180 minutes** and standard deviation is around **150 minutes**.   

>> * The major cause of departure delay are due to Carrier and Late Arrival Delays departure delay which is attributable to Airline carrier.  On analysis of delays based on Carrier following is analysed 
>>> * **Southwest Airlines (WN)** has cause the most cumulative departure delays. **Hawaiian airlines (HA) **  has best track record of lowest cumulative delay minutes.  
>>> * **Eva Airline (EV)** and **Jetblue (B6)** are worst peforming in terms of average departure delay times with still Hawillian Airlines stands out ib best performance. 

>> * A new field called route with ORIGIN and DEST together is created. The total departure delay and total Arrival Delay more than 50000 total minutes are plotted. 
>>> * The ORD to LGD and reverse direction route are most delayed flights, followed by SFO to LAX and reverse direction. This could be because of large number of flights between these airports.  
>>> * Mean delay minutes are plotted to give more than 1 hours clearer picture,  
The Mean delay minutes shows a different picture. When there a high mean shows consistent delays in **VSP to SRQ** route has huge delays for both arrival and Departure minutes. Followed by **AZA-MEM** route.  
>>> * **Fort Wilton beach to Sarasota-Bradenton international Airport** is cause of most delays.  Both these airports are in Florida on south cost, Both these airports are not major airports and major routes.   
>>> * **AZA-Phonix Mesa Gateway airport to MEM-Memphis airport** are showing next most average delays. 

>>* Further to this analysis Departure and Arrival delay by Flight numbers and flight tail Numbers are done. 
>>>* It is observed that Notoriously fight number G45814 is causing maximum delay. But it seems to be private jet so we may not omit this. **Flight number OO4711** is next greatest delay causing flight just under **300 minutes** of Arrival and Departure delays. 

>>* Further Analysing on Flight number there are some specific Aircrafts found to be causing delays. 
>>>* Only 4 flights have mean delays more than 100 minutes. **N684RW, N656YX, N2341U, N728AN**.  

>>* Further Multivariate analysis is done to understand combination of factor The Week of the day,  Time of the day, Specific routes, Airports and even specific aircraft are seen to be causing delay. For each combination of delay categories is used to find the cause of delay. 
>>* Delay by Week days, time  of the day vs Cause of delay is plotted. 
>>>* As the most delay is observed on SUN, WED THU SAT and time of the day between 1500 to 2159 for Depature dealy and 1600 to 2359 for Arrival Delay datasets are created from base datasets 
>>>* A facetgrid plot created shows most of the Departure delay are caused by late Aircraft catergory. It is Further drilled down to understand which of the Airlines by day of he week delay  
>>>* It is clearly seen by day wise drill down, **YU- EuroAtalintic** is least punctual followed by **United Airlines** are worst performers in punctuality. It is also observed that average delay of **80 minutes** for these airline during **Saturdays**. 

>>* The further plotting the drill down on most delay causing Top 50 Aircraft from the top top 2 delay causing airline , it is seen that 600 minutes is the average Departure and Arrival Delays.  
>>>* **5 Airlines from UA and 3 from YU are causing more than 1000 minutes delays**.  

>>>* Further the Flight number and routes these flights are operated is plot to understand the distribution of Late Aircraft delay and Departure delay 
>>>* It is observed that **YU** flights departure delay is commensurate to the **Late arrival delay**. But we could see **UA** airlines has further added to already late arrived flights to departure time. 
>>>* We could clearly see **UA** is worst performing in flights **UA2500- Houston,TX to Settle.WA & UA5000 Newyork to Clevland**. 
>>>* **YV flight ASH 7500** is the next worst performing next to UA flights. 

>>* Further the Analysis of Arrival Delays and the major reason for Arrival delays are analysed. 
>>>* A Facetegrid plots is creates which shows the single most prominent cause of Late Arrivals is NAS delays attributable air traffic cognition at airport.  
>>>* Top 50 Mean NAS Delay Minutes of Aiports with Top 50 NAS Delay Minutes is plotted and it is seen that  IAG - Niagra falls international Airport has extremely high delay due to NAS delay followed by IMT, ALO, BFM, ATY all have above 40 mins average NAS delay. 
>>>* Top 5 Airports Causing most Arrival delays due to NAS delay by Week day is plotted and it is seen that  
>>>>* IAG and ALO airports have evenly distributed Arrival Delays. This could be because of these airports are operating beyond its capacity to handle currently see high traffic. IMT has spick on Saturday and Wednesdays, These day could have high number of flights landing on specific days. 


   
## Key Insights for Presentation 

> **Airport vs Arrival Delay** On average 5 minutes delay for airports with more than 100k mnutes total delay and delay is less that 1 hours. When the delay is more than 1 hour the average delay is 180 minutes. 

> **Airlines vs Departure delay** EVA airlines, and Jetblue airlines are worse performing airlines in term of average delay .They are at **17.5 minutes** delay on average.  

> **Airport Routes** - Total delays is shown in Chiago to Newyork and LA to SFO routes because of relatively large number of flighys, The large mean delay is seen in minor airports and Minor routes in Florida and Phenix    

> **Flight Number** - There are few flight numbers especially flight **OO4711** is greatest delay causing flights other than other private jets 

> **Tail Numbers** - There are specific Air crafts causing good amount of delays are **N684RW, N656YX, N2341U, N728AN** 

>* The ***Departure delays are primary caused by Late Aircraft Arrival delay and Carrier Delays**. This is attributable to the Airlines.  
>* **YU and UA** are worst performing Airline for departure delays.  
>* It could be narrowed down to **3 flight numbers** which have consistent delayed arrival. One of the **routes is Houston to Settle and other is Newyork to Clevland**. 
>* The Arrival delays are more to do with **NAS delays** which are due to Airports ATS congestion. 
>* **IAG ,IMT, ALO, BFM, ATY are 5 most arrival delay causing airports**. 
>* Further breaking down by Day of the week **IAG- Niagra falls Airport is congested only on Saturdays. IMT ford airports only on Thursdays. ALO Waterloo airport on Sundays, Wednesday, Thursday and Sundays, but mostly on Wednesdays. BMF airport on Sundays only and ATY airport on Saturdays**. 
>* There should be reason for Air traffic congestion on these specific day for specific airport. These have to be further investigated to understand the root cause. 
>* **IAG and ALO airports are looks to have fairly congested air traffic**, **IMT is worst performing with Arrival delays peaking at 350 minutes on Saturdays**, This will certainly need closer examination.  

I have plotted multivariate on the based of Arrival delays by Airport due to NAS delay.  Departure delay is due to Late Arrival of Airport Delay and have to be conveyed as story on this basis.
I had feedback from my wife on the multivariate plots. Based on the feedback I have made titles and labels more meaningful. I have also included Peak Delay causing day plots. The feedback has shaped the story for the presentation. 
