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

4. Create a Data Refinery flow

 * Once the data set is added to the project
 * Click on ```Add to project``` on the top right
 * Select ```Data Refinery Flow```
 * Select the ```titanic.csv``` from the ```Data Assets``` section and click ```Add```

<p align="center">
<img src="https://github.com/fawazsiddiqi/DSPipeline/blob/master/images/ws5.png?raw=true"  width="800">
</p>

<p align="center">
<img src="https://github.com/fawazsiddiqi/DSPipeline/blob/master/images/df1.png?raw=true"  width="800">
</p>

## Data Manupulation (using Data Refinery)

The column types are already converted for you, but as you see we have a lot of missing data and unnormalized data which we need to fix (you can select the ```profile``` tab to see the profiling on the data)

<p align="center">
<img src="https://github.com/fawazsiddiqi/DSPipeline/blob/master/images/df2.png?raw=true"  width="800">
</p>

## Missing Values
The columns that have missing values in Titanic dataset are Age, Cabin and Embarked.
The methods to fulfill the missing values are different for each attribute depending on the purpose of the attribute.

### Embarked
Fill the missing values in **Embarked** attribute, we only fill it with 'S' knwong that the passengers actually embarked at Southampton.
* Select **Embarked** column, and click on Operations
* Select **Conditional Replace** under the _Organize_ Category

* Add one conditions in **Embarked** column, if value **empty** replace it with S. (Since only 2 missing values)

<p align="center">
<img src="https://github.com/fawazsiddiqi/DSPipeline/blob/master/images/embarked1.png?raw=true"  width="800">
</p>

* Click ```Apply```

### Cabin
For **Cabin** attribute, since tracing the actual cabin for each passenger is impossible. Handling this attribute by creating additional column that has 1 for a passenger who's cabin exists and 0 if it does not exist. Relating to the accident, known passenger's cabin indicate that they survived. To do that follow the below steps:

* Select the Cabin column, and click on Operations
* Select **Conditional Replace** under the _Organize_ Category

<p align="center">
<img src="https://github.com/fawazsiddiqi/DSPipeline/blob/master/images/cabin1.png?raw=true"  width="800">
</p>

* Add two conditions in Cabin's column, if value **empty** replace it with 0, if not empty replace with 1.

<p align="center">
<img src="https://github.com/fawazsiddiqi/DSPipeline/blob/master/images/cabin2.png?raw=true"  width="800">
</p>

* Choose Cabin column, in the option of __Replace__ put 1

<p align="center">
<img src="https://github.com/fawazsiddiqi/DSPipeline/blob/master/images/cabin3.png?raw=true"  width="800">
</p>

* Click ```Apply```

**Note**: Make sure you change the data type of the Cabin to ```Integer```

### Age

For **age** attribute, calculate the mean of the column values and placing it in the null values.
To replace missing values by the mean of the column, do the following:

* From the Operations menu choose **Filter condition**.

<p align="center">
<img src="https://github.com/fawazsiddiqi/DSPipeline/blob/master/images/age1.png?raw=true"  width="800">
</p>

* Select _column_ **Age** and **Is not empty** under _operator_ for the Filteration condition.

<p align="center">
<img src="https://github.com/fawazsiddiqi/DSPipeline/blob/master/images/age2.png?raw=true"  width="800">
</p>

* From the **Operation** Bar, select **Summarize** operator.

<p align="center">
<img src="https://github.com/fawazsiddiqi/DSPipeline/blob/master/images/age3.png?raw=true"  width="800">
</p>

* Fill in the operation command the required variables like this Summarize(newVarName=operator(column))
```summarize(NewAge = mean(`Age`))```

<p align="center">
<img src="https://github.com/fawazsiddiqi/DSPipeline/blob/master/images/age4.png?raw=true"  width="800">
</p>

<p align="center">
<img src="https://github.com/fawazsiddiqi/DSPipeline/blob/master/images/age5.png?raw=true"  width="800">
</p>

* Copy the geneated value to use after, and undo last two action from the backward arrow above.
Since the filteration and the new summerized value is now useless.

<p align="center">
<img src="https://github.com/fawazsiddiqi/DSPipeline/blob/master/images/age6.png?raw=true"  width="800">
</p>

* Select **Age** column again, from the Action menu choose **Replace missing values**

<p align="center">
<img src="https://github.com/fawazsiddiqi/DSPipeline/blob/master/images/age7.png?raw=true"  width="800">
</p>

* Insert the mean value to be replaced with and press _Apply_ button.

<p align="center">
<img src="https://github.com/fawazsiddiqi/DSPipeline/blob/master/images/age8.png?raw=true"  width="800">
</p>

## Duplicates 

* Titanic data set does not have sensitive information that should be unique except for the passenger ID. Simply select the Action menu in ```PassengerId``` column and choose Remove duplicates.

<p align="center">
<img src="https://github.com/fawazsiddiqi/DSPipeline/blob/master/images/dup1.png?raw=true"  width="800">
</p>

6. Saving and running your refinery flow

* Once completed with all the above steps click on ```Edit``` on the right pane 

<p align="center">
<img src="https://github.com/fawazsiddiqi/DSPipeline/blob/master/images/df3.png?raw=true"  width="800">
</p>

* Click on ```Edit Output``` and rename the output as ```titanic_shaped.csv```

7. Running your flow 

* Once completed editing the output, on your top right select ```Jobs```

<p align="center">
<img src="https://github.com/fawazsiddiqi/DSPipeline/blob/master/images/df4.png?raw=true"  width="800">
</p>

* Select ```Save and Create a Job```
* Give the Job a name and click ```Next``` to run the cleaning job

<p align="center">
<img src="https://github.com/fawazsiddiqi/DSPipeline/blob/master/images/df5.png?raw=true"  width="800">
</p>

Now you will see ```titanic_shaped.csv``` in your project assets

