![image](https://github.com/AbdallahQoutbAli/Azure-Data-Factory-For-Data-Engineers---Project-on-Covid19/assets/47276503/6c17c903-8d2f-406e-9b6c-bfac9300fba5)![image](https://github.com/AbdallahQoutbAli/Azure-Data-Factory-For-Data-Engineers---Project-on-Covid19/assets/47276503/1733005b-719d-4331-884a-67cf8708e3af)# Azure-Data-Factory-For-Data-Engineers---Project-on-Covid19



In this project we help your data scines team to make a predaciton 


 create a data platform from which our data science team can run machine learning models to predict the spread of the virus, and find other insights from the data., we wanna create a data platform from which our data analysts can easily report on the COVID-19 trends using a reporting tool. o, those are the two main objectives of our project. he solution that we are building will be limited o reporting on the data related to EU countries and UK only. I did this mainly because I was familiar with these data sets from working on my pet project.

Our main objective here is to create a data platform from which our data scientists can create machine learning models. We'll then populate the data warehouse with the subset of the data so that it can be used for reporting on trends. The data warehouse will include details about confirmed cases, unfortunate mortality rates, hospitalization and ICU cases from our weekly counts in the data lake, as well as the testing numbers. We'll then build a Power BI report from this data.


Source Data :
ECDC (https://www.ecdc.europa.eu/en/covid-19) Connect using HTTP connector  
Population Data From Azure Blob Storage 
(Azure Blob storage is a solution for storing large amount of text or binary data.)
DESC : Azure Data Lake storage (GEN2)

Tools : 
used ADF Data Flows within the Data Factory for the couple of data sets. 
Data Factory will be used as the orchestration For the HDInsight and the data bricks 
All of the transformed data will then be stored in our Azure Data Lake storage (GEN2)

ADF For Data Integration 
Transformation : 
Data Flows within the Data Factory
HDInsight
The data bricks 

And finally, we've used Azure's SQL database

for our data warehouse solution.

![image](https://github.com/AbdallahQoutbAli/Azure-Data-Factory-For-Data-Engineers---Project-on-Covid19/assets/47276503/fb200fd3-5381-4d03-8f6c-b4a464b8fb07)


Data Ingestion – Population Data
Ingest ”population by age” for all EU Countries into the Data Lake to support the machine learning models to predict increase in Covid-19 mortality rates

![image](https://github.com/AbdallahQoutbAli/Azure-Data-Factory-For-Data-Engineers---Project-on-Covid19/assets/47276503/50abaa2e-13aa-471c-9cfc-e36f78e4834d)


Steps : 
1- Create Linked Server To Azure Blob Storage 
2-Connect to Source Data Set 
3- Create Linked Server To Azure Data Lake storage (GEN2) 
4-Slink Data set 
5-Create Pipeline
6-Execute Copy Activity when the file becomes available
7-ScheduleTrigger


![image](https://github.com/AbdallahQoutbAli/Azure-Data-Factory-For-Data-Engineers---Project-on-Covid19/assets/47276503/d0acf9ab-a238-4eb2-90e2-b502f0e33e85)



 
