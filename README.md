# Collect, clean, predict and deploy your Data Science Pipeline 

Lets collect, clean, predict and deploy your data science pipeline on IBM Cloud. As we all know a data science pipeline consists of various steps, which certainly starts with collecting your data from different data sources, then we come to understanding the data making sure that we are able to get meaning out of it and we clean it by managing missing values and normalizing it and then we train and deploy our machine learning model which is followed by getting feedback from the models result and re-evaluating it. 

## Services Used

We will use various IBM Services which will aid us to complete our data science pipeline

* **IBM Watson Studio:** Analyze data using RStudio, Jupyter and Machine Learning Flow in a configured, collaborative environment that includes IBM value-adds, such as managed Spark.

* **IBM Cloud Object Storage:** An IBM Cloud service that provides an unstructured cloud data store to build and deliver cost effective apps and services with high reliability and fast speed to market. This code pattern uses Cloud Object Storage.

* **IBM Data Refinery:** A part of the Watson Data Platform integrated environment and is a self-service data preparation client for data scientists, data engineers, and business analysts. It can transform large amounts of raw data into consumable, quality information that’s ready for analytics. IBM Data Refinery makes it easy to explore, prepare, and deliver data.

* **SPSS Modeler:** With SPSS Modeler flows in Watson Studio, you can quickly develop predictive models using business expertise and deploy them into business operations to improve decision making. Designed around the long-established SPSS Modeler client software and the industry-standard CRISP-DM model it uses, the flows interface in supports the entire data mining process, from data to better business results. 

## Pre-requisites

* **IBM Cloud account:**  An account must exist to use the platform.

* **Watson Studio service instance:** A service instance must exist to be able to use **Data Refinery** & **SPSS Modeler**.

## Steps

* If you do not have an IBM Cloud account please create one or login into your existing account by clicking [here](https://ibm.biz/pathto-ai)

* Please make sure that you have cloned/downloaded this repository

1. Create a Watson Studio service 

* Once logged in, search for Watson Studio and create a lite instance 

<p align="center">
<img src="https://github.com/fawazsiddiqi/DSPipeline/blob/master/images/ws1.png?raw=true"  width="800">
</p>

<p align="center">
<img src="https://github.com/fawazsiddiqi/DSPipeline/blob/master/images/ws2.png?raw=true"  width="800">
</p>

2. Create an empty project

Once your Watson Studio service is created, head over to creating a new project 

 * Access the serivce and click either **Create a project** or **New project**.
 * Select **Create an empty project**.
 * Give the project a name.
 * Choose an existing Object Storage service instance or create a new one.
 * Click **Create**.

<p align="center">
<img src="https://github.com/fawazsiddiqi/DSPipeline/blob/master/images/ws3.png?raw=true"  width="800">
</p>

3. Add your data

 * Once in your project, click on the Assets tab
 * On the pane to the left, either drag and drop your data set or click browse and locate your dataset and add it to the project 
 
<p align="center">
<img src="https://github.com/fawazsiddiqi/DSPipeline/blob/master/images/ws4.png?raw=true"  width="800">
</p>