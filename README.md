
# Azure-Data-Factory-For-Data-Engineers---Project-on-Covid19

Our main objective here is to create a data platform from which our data scientists can create machine-learning models. We'll then populate the data warehouse with the subset of the data so that it can be used for reporting on trends. The data warehouse will include details about confirmed cases, unfortunate mortality rates, hospitalization and ICU cases from our weekly data lake counts, and the testing numbers. We'll then build a Power BI report from this data.


### Source Data :
- ECDC (https://www.ecdc.europa.eu/en/covid-19) 
- Population Data From Azure Blob Storage 

### Destination: <br>
 Azure Data Lake Storage (GEN2) <br>
 
 ### Tools: <br> 
 - Data Integration/Ingestion : 
 used ADF Data Flows within the Data Factory  
 
 - Transformation : 
 Data Flows within the Data Factory
 HDInsight
 The data bricks 
 
 - Data warehouse solution : 
  we've used Azure's SQL database for our 
 
 - visualization : 
 Power BI Desktop and Power BI service  


<br> Note :
Data Factory will be used as the orchestration For the HDInsight and the data bricks  <br>
All of the transformed data will then be stored in our Azure Data Lake storage (GEN2)


# Solution Architecture Overview : 
![image](https://github.com/AbdallahQoutbAli/Azure-Data-Factory-For-Data-Engineers---Project-on-Covid19/assets/47276503/fb200fd3-5381-4d03-8f6c-b4a464b8fb07)

 # Data Ingestion 
 ###  1- Population Data 
 
Ingest "population by age" for all EU Countries into the Data Lake to support the machine learning models to predict an increase in Covid-19 mortality rates

![image](https://github.com/AbdallahQoutbAli/Azure-Data-Factory-For-Data-Engineers---Project-on-Covid19/assets/47276503/50abaa2e-13aa-471c-9cfc-e36f78e4834d)


Steps : 
#### 1. Create a Linked Server To Azure Blob Storage 
#### 2. Connect to Source Data Set
#### 3. Create a Linked Server To Azure Data Lake storage (GEN2)
#### 4. Slink Data set
#### 5. Create a Pipeline
#### 6. Execute Copy Activity when the file becomes available
#### 7. ScheduleTrigger<br>

 ### Pipeline Overview : 


![image](https://github.com/AbdallahQoutbAli/Azure-Data-Factory-For-Data-Engineers---Project-on-Covid19/assets/47276503/6c17c903-8d2f-406e-9b6c-bfac9300fba5)

 ### 2- ECDC Data 
![image](https://github.com/AbdallahQoutbAli/Azure-Data-Factory-For-Data-Engineers---Project-on-Covid19/assets/47276503/d0acf9ab-a238-4eb2-90e2-b502f0e33e85)


(Connect using HTTP connector) 
 
