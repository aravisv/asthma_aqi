Does monthly AQI correlate with hospital admissions for asthma in Indian cities?

I had started on a project with the motivation of exploration on common respiratory illnesses and several parameters that affect it. It was too broad and was lagging behind a lot. 

Hence picking this small qn.

Asthma / health related sources

some pdf regarding asthma data of CDC 
https://cdn.ymaws.com/www.cste.org/resource/resmgr/EnvironmentalHealth/Asthmacomplete2.pdf

US - CDC
https://stacks.cdc.gov/gsearch?terms=asthma

https://www.cdc.gov/asthma-data/about/most-recent-asthma-data.html

dataful is paid!!
https://dataful.in/datasets/6182/

Seems like Good resource - Indian
https://hmis.mohfw.gov.in/#!/
publications → RHS → rural health stats (number of health centres, doctors, rural & urban population etc)

data gov in

NFHS

### **Data Usage Notice**

The data and content provided are intended solely for personal, educational, or research purposes. Users agree not to use, reproduce, distribute, or exploit any data or content for commercial gain, including but not limited to selling, licensing, or redistributing for profit. All rights, ownership, and intellectual property rights to the data remain with NFHS, IIPS. Users acknowledge that the data is provided "as is", without any warranties regarding accuracy, completeness, or suitability for specific purposes.

Not for datasets, but good reports - Indian
https://www.icmr.gov.in/reports

Global summary data

https://vizhub.healthdata.org/gbd-compare/

Data sources

https://ghdx.healthdata.org/data-sites-we-love

https://ghdx.healthdata.org/

AQI related sources

real time, by state, good days vs bad days

https://www.data.gov.in/search?title=aqi&type=resources&sortby=_score
need to filter as needed

zenodo aqi dataset and model
[https://zenodo.org/records/13694585](https://zenodo.org/records/13694585?utm_source=chatgpt.com)
but the data is of .nc4 format

kaggle
https://www.kaggle.com/datasets/rohanrao/air-quality-data-in-india/data
https://www.kaggle.com/datasets/neomatrix369/air-quality-data-in-india-extended

2013 - 2023
citywise
https://cpcb.nic.in/manual-monitoring/

https://cpcb.nic.in/

the way to proceed would be to finalise on the asthma dataset
see whether the data is state / city wise, frequency is monthly or yearly
based on that, choose the AQI dataset
we have data for India itself regarding the diseases / asthma. need to clean and transform the data for that


Got 3 csv files
29 states, percentage of people suffering from asthma -  women, men in rural & urban
years - 2005-06, 2015, 2017
https://www.data.gov.in/search?title=asthma&type=resources&sortby=_score

Now I need AQI data - yearly, statewise
Statewise and yearly AQI is a very broad level summary
But given I dont have the monthly and a much granular region level data on Asthma patients, this is the only option to move forward

For 2005, the datasets are state specific. Need to download around 25 csv files and then combine
https://www.data.gov.in/catalog/historical-daily-ambient-air-quality-data?page=1

Can be done later. 
From 2015 to 2020, I can use the kaggle dataset 

https://www.kaggle.com/datasets/rohanrao/air-quality-data-in-india/data

info about AQI calculation
https://www.kaggle.com/code/rohanrao/calculating-aqi-air-quality-index-tutorial?scriptVersionId=41199538

But we need to inspect whether the AQI dataset has all the state’s cities

It has only 21 states. There are duplicate cities in the same state. 
We can either find new dataset. Or use the existing one. 
Average the cities in the same state and go forward. 
Is that the best approach? No. Because the cities’ population, number of industries, vehicles etc will differ. But we are averaging it out and proceeding anyhow. Compromises.

I think its better to move to Python now than doing in excel

Coming to the exploratory experiment, I can do below
1 - see the pattern of particular year patients and the AQI
2 - Year wise comparisons
3 - gender specific patients
4 - prediction of number of patients, based on the found patterns above

After getting the AQI data for particular years, there seems to be large number of NA values.
I dont know how to handle it except deletion, which is not a good idea.
Hence proceeding to explore handling of missing values.


Coming back to this project after doing a detailed basic study of missingness,

Accroding to CPCB, 
How is AQI calculated? 
1. The Sub-indices for individual pollutants at a monitoring location are calculated using its 24-hourly average concentration value (8-hourly in case of CO and O3) and health breakpoint concentration range. The worst sub-index is the AQI for that location. 
2. All the eight pollutants may not be monitored at all the locations. Overall AQI is calculated only if data are available for minimum three pollutants out of which one should necessarily be either PM2.5 or PM10. Else, data are considered insufficient for calculating AQI. Similarly, a minimum of 16 hours’ data is considered necessary for calculating subindex.  
3. The sub-indices for monitored pollutants are calculated and disseminated, even if data are inadequate for determining AQI. The Individual pollutant-wise sub-index will provide air quality status for that pollutant.  
4. The web-based system is designed to provide AQI on real time basis. It is an automated system that captures data from continuous monitoring stations without human intervention, and displays AQI based on running average values (e.g. AQI at 6am on a day will incorporate data from 6am on previous day to the current day). 
5. For manual monitoring stations, an AQI calculator is developed wherein data can be fed manually to get AQI value. 

AQI Calculator (Excel) → https://cpcb.nic.in/upload/national-air-quality-index/AQI-Calculator.xls

Started exploring missing data in the AQI dataset
Dropped some of the columns and cities which are not relevant to calculate the AQI, and with huge number of missing values

Reflection : 
How could I have sped up the exploratory analysis of data?
Since i dont know python and pandas much, I keep asking claude for the code
It gives code, I execute after checking it
If the results are not what I expect, I reframe the prompt one more time and get the right answer
Further upon executing a command and seeing a pattern, I have to deep dive and go in a more granular level
This cannot be foreseen before, unless I have domain expertise or have done similar projects before


Recalculated AQI and the bucket using the formula. Because for some rows the AQI was not calculated. 
And I wanted the AQI score and formula used to be consistent.
It was a good decision, since the AQI scores differed for some rows hugely.

we can impute the missing values. but given that the health data of asthma patients is only for 2 years, imputation efforts would be not worth it
because finally we will just have 2 yearly data points, so any statistical test and inference we do will not be significant
hence continuing with some aggregations of the yearly indicators' data

first lets create function to calculate AQI, then replace the AQI score and AQI bucket columns, since we dont know which formula was used in calculating
to maintain consistency, its better to recalculate all, although it seems expensive and redundant
we need to first calculate per day AQI, and then average it over months, seasons, and year

then we can derive new columns such as bad pollution days, winter and summer AQIs etc...

https://www.lung.org/blog/asthma-and-air-pollution
PM2.5, NO2 - child asthma

https://pmc.ncbi.nlm.nih.gov/articles/PMC7503605/ 
summary table by NotebookLM

| **NO2**  | Causes new-onset asthma. | Children. |
| --- | --- | --- |
| **PM2.5** | Causes new-onset and exacerbations. | Children and Elderly. |
| **Ozone** | Triggers severe exacerbations and hospital visits. | Children and active outdoor adults. |
| SO2 | Asthma prevalence | Children, especially with atopy |

https://www.sciencedirect.com/science/article/pii/S2659663625000529
Abstract of the study has the same matching info

We can focus on deriving some aggregates on NO2, PM2.5, Ozone (O3)

Calculated the aggregates - City, Month, Season, Yearly.
There are lot of combinations of data.
I think its better to use some visualisation tools rather than the table outputs in jupyter notebook


