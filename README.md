# Wine_selection_for_newbies
This repository contains my final project for  Data Analytics Bootcamp.  I explored a Wine Reviews dataset and built an interactive Tableau dashboard to recommend wines for a novice based on price, rating, variety, and country. I also built a machine learning model to train it to rate wine like an experienced sommelier.
## Table of Contents
* [Presentation](#Presentation)<br>
    * [Predictive Wine Ratings](#Predictive-Wine-Ratings)<br>
    * [Technologies Used](#Technologies-Used)<br>
          *  [Data Cleaning and Analysis](#Data-Cleaning-And-Analysis)<br>
          *  [Database Storage](#Database-Storage)<br>
          *  [Machine Learning](#Machine-Learning)<br>
          *  [Dashboard](#Dashboard)<br>
          *  [Final Project Website](#Final-Project-Website)<br>
* [Database](#Database)<br>    
    * [Dataset](#Dataset)<br>         
* [Machine Learning Model](#Machine-Learning-Model)<br>
    * [Question we would like to answer with our machine learning model](#Question-we-would-like-to-answer-with-our-machine-learning-model)<br>
    * [Machine Learning Model](#Machine-Learning-Model)<br>
    * [Output Label](#Output-Label)<br>
    * [Model Accuracy](#Model-Accuracy)<br>
    * [Data Preprocessing](#Data-Preprocessing)<br>
    * [How the model works](#How-the-model-works)<br>
* [Looking Ahead](#Looking-Ahead)<br>
    * [What are some possible improvements we could make?](#What-are-some-possible-improvements-we-could-make?)<br>
    * [Ideas for further development](#Ideas-for-further-development)<br>


## Presentation

#### <ins><b>Predictive Wine Ratings</ins></b><br> ####
For this repository I chose to explore a Wine Reviews dataset compiled from Wine Enthusiast magazine. I selected this topic because I am part of a group of wine enthusiasts but  certainly no sommeliers. Since wine can be complicated and overwhelming, I wanted to create a fun and interactive way for beginners to discover new wines. With this idea in mind, I built a dashboard to recommend wines for a novice based on such things as price, rating, variety, country and province. I also built a machine learning model to see if we could train it to rate wine like an experienced sommelier. For an in-depth look at my project, see my [Wine for Newbies presentation](https://docs.google.com/presentationxxxxx) on Google Slides.<br><br>

<div align="center">
  
  ![wine_row](Images/wine_row.png)
  
</div>

#### <ins><b>Technologies Used</ins></b><br> ####

* ##### <b>Data Cleaning and Analysis</b><br> #####
  I performed our data transformation and analysis with Python and Pandas using Jupyter Notebook.   See [Wine_Ratings.ipynb](https://github.com/-----.ipynb) for the code that transformed and analyzed our data.<br>
* ##### <b>Database Storage</b><br> #####
  I used PostgresSQL for database storage. Connections to the SQL database were created in our machine learning and data analysis notebooks. Again, this decision was made due to familiarity.<br>
* ##### <b>Machine Learning</b><br> #####
  For the machine learning portion, I chose to use a SciKitLearn Random Forest model due to the algorithm's high degree of accuracy, the reduced chance of overfitting, and the need to use a supervised model.<br>
* ##### <b>Dashboard</b><br> #####
  I used Tableau to build our [Dashboard](https://public.tableau.com/a xxxxxxx2) and [Story](https://public.tableau.com/app/profilexxxxxory). Interact with the dashboard by selecting a desired country from our dropdown feature or maybe you are looking for a specific price point - we have that covered in a slide scale in the upper left-hand corner.<br>
 
</div>

<div align="center">
  
  ![wine_communication](Images/wine_communication.png)

</div>

## Database<br><br>

#### <ins><b>Dataset</ins></b><br> ####
My raw dataset contained almost 130,000 rows of information that included the wine's title, grape variety, winery, country and region of origin, as well as the price per bottle, wine rating, taster name, and a description about the wine.  The original data was created by [Wine Enthusiast](https://www.winemag.com/ratings/?utm_source=wineenthusiast.com&utm_medium=affiliate&utm_content=topnav) and the [Wine Reviews dataset](https://www.kaggle.com/zynicide/wine-reviews) was posted on Kaggle.  I used a SQL database - see  [Entity Relationship Diagram (ERD)](https://github.comxxxxxQuickDBD-Winemag_data.png) with relationships. After we finished cleaning and transforming the data, our final [dataset](https://github.com/xxxxxxx/clean_wine_data.csv) contained almost 115,000 rows and 12 columns.<br><br>

<div align="center">
  
![wine_database](Images/wine_database.png)

</div>

## Machine Learning Model

#### <ins><b>Question I would like to answer with our machine learning model</ins></b><br> ####
Can a machine learning model be trained to rate wine like an experienced sommelier? <br><br>
#### <ins><b>Machine Learning Model</ins></b><br> ####
I chose a random forest model since we needed a supervised learning model. Random forest algorithms are great to use for classification or regression problems and typically produce a higher degree of accuracy. The model does a good job to avoid overfitting and it can efficiently handle large datasets like ours. The biggest downside to using this type of model is computing time. The model can take hours to fit to the training data making it very time consuming to optimize.<br><br>
#### <ins><b>Output Label</ins></b><br> ####
My machine learning model's output label is a wine rating -- a continuous value between 80 and 100 -- otherwise known as "points" in the dataset.<br><br> 
#### <ins><b>Data Preprocessing</ins></b><br> ####
Our initial dataset was fairly robust with lots of data (almost 130,000 rows and 13 columns) but offered a limited number of valuable features to analyze and explore. Therefore, I engineered the following features: 
* I extracted the year the wine was made by searching the title column for a regular expression then added it as an extra feature to our dataset, focusing on wines made starting in 2000 since this made up most of our dataset.
* I used dictionary keys to look in the description, variety and title columns and assigned a red or white designation. I added this feature as an additional column called wine type.
* I added a column to group ratings into 5 categories -- below average, average, good, very good and excellent. The idea was we could use these categories to add context and value to our consumer-friendly dashboard. However, I did not use this feature to train our machine learning model since it was derived from the feature I were trying to predict.<br><br>
To clean and transform our dataset further:<br>
* I replaced null values in the region_1 column with province name and in the taster_name column with "unknown"
* I reluctantly dropped the description, designation, title and winery columns since they presented computational challenges for our machine learning model
* I dropped the region_2 and taster_twitter_handle columns since they didn’t add value to our model or dashboard.<br><br>
#### <ins><b>How the model works</ins></b><br> ####
See a [flowchart](https://github.com/XXXXXX/MLModel_flowchart.png) for a broad overview of the process for my [machine learning model](https://github.com/xxxxx/MLModel.ipynb).  First, the model made a connection to our SQL database and read the dataset into a Pandas dataframe. Then, the data was cleaned and transformed. Once the data was ready, the categorical columns were split into binary data using scitkit-learn’s One Hot Encoder. This tool created a new column for each unique value in the previous columns which made the dataset quite larger than before. The data was then split using scikit-learn’s Train Test Split method into 75% training data and 25% testing data. Finally, the model was fit to the data. This was the most time-consuming part of the process. At 100 estimators, the model took about an hour to fit to the data.<br><br>
#### <ins><b>Model Accuracy</ins></b><br> ####
Since my target is continuous and not discrete, i could not use a confusion matrix and the traditional accuracy score to rate the performance of our model. Instead, i use the coefficient of determination (r²) as well as the mean squared error (mse). Both of these are simply just ways of measuring how far away each data point is from the line of regression. A perfect model has an r² value of 1 and a mse of 0.

When i trained the model to predict wine ratings, it scored an r² value of 0.478 and an mse value of 4.78. When i trained it to predict categories of wine ratings, it scored an r² value of 0.149 and an mse value of 0.109. In the end, due to my computational limitations and the abundance of categorical features in our dataset, several of which i had to omit, my model performed mediocrely.<br><br>

<div align="center">
  
![wine_cellar](Images/wine_cellar.png)<br><br>

</div>

## Looking Ahead

#### <ins><b>What are some possible improvements i could make?</ins></b><br> ####
If i had a very large amount of computing power (over 100GB RAM) then i could go back and include the title and winery columns to improve my model's results. Also, all features other than price proved to be weak learners. Clearly there are other factors not contained in our dataset that have a huge impact on the rating of a wine, such as climate and weather data for instance. Given more time, i could bring in additional features like these and improve our model. Finally, i had a few outliers in our datset that i should consider addressing.<br><br>
#### <ins><b>Ideas for further development</ins></b><br> ####
Ideally, natural language processing techniques would be used to predict score based on text found in the description column. This was simply out of reach for us given our skill sets and time constraints.<br><br>

<div align="center">
  
![wine_toast_sunset](Images/wine_toast_sunset.jpg)<br><br>

</div>