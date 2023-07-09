
# Azure-Data-Factory-For-Data-Engineers---Project-on-Covid19

Our main objective here is to create a data platform from which our data scientists can create machine-learning models. We'll then populate the data warehouse with the subset of the data so that it can be used for reporting on trends. The data warehouse will include details about confirmed cases, unfortunate mortality rates, hospitalization and ICU cases from our weekly data lake counts, and the testing numbers. We'll then build a Power BI report from this data.


### Source Data :
- ECDC (https://www.ecdc.europa.eu/en/covid-19) 
- Population Data From Azure Blob Storage (eurostat_data)

### Destination: <br>
 Azure Data Lake Storage (GEN2) <br>
 
 ### Tools: <br> 
 - Data Integration/Ingestion : 
    - used ADF Data Flows within the Data Factory  
 
 - Transformation : 
   -  Data Flows within the Data Factory
   -  DataBricks 
 
 - Data warehouse solution : 
    -  we've used Azure's SQL database
 
 - visualization : 
    - Power BI Desktop and Power BI service  


<br> Note : <br>
- Data Factory will be used as the orchestration For the HDInsight and the data bricks  <br>
- All of the transformed data will then be stored in our Azure Data Lake storage (GEN2)


# Solution Architecture Overview : 
![image](https://github.com/AbdallahQoutbAli/Azure-Data-Factory-For-Data-Engineers---Project-on-Covid19/assets/47276503/fb200fd3-5381-4d03-8f6c-b4a464b8fb07)

 # Data Ingestion 
 ###  1- Population Data 
 
Ingest "population by age" for all EU Countries into the Data Lake to support the machine learning models to predict an increase in Covid-19 mortality rates

###  Overview
![image](https://github.com/AbdallahQoutbAli/Azure-Data-Factory-For-Data-Engineers---Project-on-Covid19/assets/47276503/50abaa2e-13aa-471c-9cfc-e36f78e4834d)


### Steps : 
#### 1. Create a Linked Server To Azure Blob Storage 
#### 2. Connect to Source Data Set
#### 3. Create a Linked Server To Azure Data Lake storage (GEN2)
#### 4. Slink Data set
#### 5. Create a Pipeline :
  <ol>
   <li> Execute Copy Activity when the file becomes available </li>
   <li> Check metadata counts before loading the Data using the IF Condition  </li>
   <li> Finally Load Data Into Our Destination </li>
  </ol>
  
#### 6. ScheduleTrigger <br>
 ### Pipeline Overview : 


![image](https://github.com/AbdallahQoutbAli/Azure-Data-Factory-For-Data-Engineers---Project-on-Covid19/assets/47276503/6c17c903-8d2f-406e-9b6c-bfac9300fba5)

 ### 2- ECDC Data 
 #### the ECDC Data Content Four File of CSV : 

##### 1. Case & Deaths Data.csv
##### 2. Hospital Admission Data.csv
##### 3. testing.csv
##### 4. country_response.csv
 
###  Overview
![image](https://github.com/AbdallahQoutbAli/Azure-Data-Factory-For-Data-Engineers---Project-on-Covid19/assets/47276503/628015ca-81ce-4495-8cdf-53e983c3625b)

### Steps : 
#### 1. Create a Linked Server using an HTTP connector
#### 2. Connect to Source Data Set
#### 3. Create a Linked Server To Azure Data Lake storage (GEN2)
#### 4. Slink Data set
#### 5. Create a Pipeline With Parameters & Variables 
#### 6. used Lookup to get all Parameters from Json File then pass it to  ForEach ECDC DATA as shown Below 
#### 7. ScheduleTrigger <br>

### Json File : 
![image](https://github.com/AbdallahQoutbAli/Azure-Data-Factory-For-Data-Engineers---Project-on-Covid19/assets/47276503/3334e5dd-b638-4f21-af29-7170f9f35eb0)


 ### Pipeline Overview : 
 ![image](https://github.com/AbdallahQoutbAli/Azure-Data-Factory-For-Data-Engineers---Project-on-Covid19/assets/47276503/0823f057-9f65-4c61-aed0-581a679a9d79)

### End Data Ingestion 
 # 2.Data Transformation 
 
 ## Data Flows (1)  Cases & Deaths Data

###  Overview : 
![image](https://github.com/AbdallahQoutbAli/Azure-Data-Factory-For-Data-Engineers---Project-on-Covid19/assets/47276503/9d1ef49b-d2da-4424-a735-aeda963cc98c)

### Steps : 
#### 1. Cases And DeathsSource (Azure Data Lake Storage Gen2 )
#### 2. Filter Europe-Only Data 
#### 3. Select Only Requirements Columns
#### 4. PiovtCounts using indicator Columns using (confirmed cases, deaths) and get the sum Daily Count
#### 5. Lookup Country to get country_code_2_digit,country_code_3_digit columns
#### 6. Select Only requirements For Sink
#### 7. Slink to Destination (Azure Data Lake Storage Gen2)

 ### Pipeline Overview : 

 ![image](https://github.com/AbdallahQoutbAli/Azure-Data-Factory-For-Data-Engineers---Project-on-Covid19/assets/47276503/aa9e1bcd-1dfa-4582-9f22-ac18c04f033a)

 ## Data Flows (2)  Cases & Deaths Data
 
 ###  Overview : 
![image](https://github.com/AbdallahQoutbAli/Azure-Data-Factory-For-Data-Engineers---Project-on-Covid19/assets/47276503/7b6b58dc-c381-4d15-89b3-afccec2e8e7a)

### Steps : 
#### 1. Hospital Admissions Source (Azure Data Lake Storage Gen2 )
#### 2. Select Only Requirements Columns 
#### 3. Lookup Country to get country_code_2_digit,country_code_3_digit columns
#### 4. Select Only Requirements Columns 
#### 5. Condition Split Weekly, Daily Split condition 
 <ol>
   <li> indicator=='Weekly new hospital admissions per 100k' || indicator=='Weekly new ICU admissions per 100k'</li>
   <li>  indicator== "Daily hospital occupancy" || indicator=="Daily ICU occupancy" </li>
 </ol>
  
#### 6. For Weekly Path 
 <ol>
    <li> Join With Date To Get ecdc_Year_week,week_start_date,week_End_date</li>
   <li> Piovt Counts using indicator Columns using (confirmed cases, deaths) and get the sum Daily Count </li>
   <li> Sort Data using reported_year_week ASC and Country DESC  </li>
   <li> Select Only requirements For Sink </li>
   <li> Slink to Destination (Azure Data Lake Storage Gen2) </li>
 </ol>

   
#### 7. For Daily Path 
 <ol>
   <li> Piovt Counts using indicator Columns using (confirmed cases, deaths) and get the sum Daily Count </li>
   <li> Sort Data using reported_year_week ASC and Country DESC  </li>
   <li> Select Only requirements For Sink </li>
   <li> Slink to Destination (Azure Data Lake Storage Gen2) </li>
 </ol>
 

 ### Pipeline Overview : 

![image](https://github.com/AbdallahQoutbAli/Azure-Data-Factory-For-Data-Engineers---Project-on-Covid19/assets/47276503/6e8008e1-5255-43d8-86b0-286826a50435)

 ## Databricks Activity (3) --Population File
 
 ###  Overview : 


 ![image](https://github.com/AbdallahQoutbAli/Azure-Data-Factory-For-Data-Engineers---Project-on-Covid19/assets/47276503/97068206-7da2-418e-9a36-ed5a49085db4)

Attached File : 
pyspark_notebooks/transform_population_data.py

 ### End Data Transformation 

 
