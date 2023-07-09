
# Azure-Data-Factory-For-Data-Engineers---Project-on-Covid19

Our main objective here is to create a data platform from which our data scientists can create machine-learning models. We'll then populate the data warehouse with the subset of the data so that it can be used for reporting on trends. The data warehouse will include details about confirmed cases, unfortunate mortality rates, hospitalization and ICU cases from our weekly data lake counts, and the testing numbers. We'll then build a Power BI report from this data.


### Source Data :
- ECDC (https://www.ecdc.europa.eu/en/covid-19) 
- Population Data From Azure Blob Storage 

### Destination: <br>
 Azure Data Lake Storage (GEN2) <br>
 
 ### Tools: <br> 
 - Data Integration/Ingestion : 
    - used ADF Data Flows within the Data Factory  
 
 - Transformation : 
   -  Data Flows within the Data Factory
    - HDInsight
   -  The data bricks 
 
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
 # 2.Transformion  
 #### Cases & Deaths Data using Data Flow 

