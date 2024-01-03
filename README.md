# IBM Data Analyst Capstone

## Background Information
This project was undertaken as a part of the IBM Data Analyst Professional Certificate Capstone course on Coursera.

For this project, we assume that we are a Data Analyst at a Global IT and Business Consulting Firm. In order to keep pace with changing technologies, the organization regularly analyzes data and trends to identify future skill requirements.

As a Data Analyst, we have been tasked with collecting data from various sources and identifying trends for this year's report on emerging technology skills. The purpose of the results are to aid developers and employers in staying relevant in the job market and guide amployer traing and upskilling support. 

Each step of the data analysis process is shown in different notebook of this repository and some aditional files needed for their understanding.

## Repo Structure
- [Data Folder](https://github.com/nkiesz39/IBM_Data_Analyst_Capstone/tree/main/Data)
  - This folder contains csv files of survey data used in this project.
    - Includes technology use survey and Demographics survey
- [Collecting Job Data with APIs](https://github.com/nkiesz39/IBM_Data_Analyst_Capstone/blob/main/Collecting_Jobs_data_Using_API.ipynb)
  - Collecting_Jobs_data_Using_API.ipynb
  - A Python file that contains the code used to collect jobs data from a subset of Kaggle data.
  - API objectives:
    - Collect the number of job openings for various locations
    - Collect the number of job openings for various technologies
- [Web Scraping](https://github.com/nkiesz39/IBM_Data_Analyst_Capstone/blob/main/Web_Scraping_Capstone.ipynb)
    - Web_Scraping.ipynb
    - A Python file used to gather data by web scraping from an IBM website, specifically used for the course
    - Using BeautifulSoup to gather data about Promgramming Languages, the Average Salary Associated, and Learning Difficulty
- [Data Wrangling](https://github.com/nkiesz39/IBM_Data_Analyst_Capstone/blob/main/DataWrangling_Capstone.ipynb)
    - DataWrangling_Capstone.ipynb
    - Objectives:
      - Identify and remove duplicate values
      - Identify missing values
      - Impute missing values, if appropriate
      - Normalize data
  - [Exploratory Data Analysis](https://github.com/nkiesz39/IBM_Data_Analyst_Capstone/blob/main/ExploratoryDataAnalysis_Capstone.ipynb)
    - EDA_Capstone.ipynb
    - A Python file used to perform EDA
    - Objectives:
      - Identify the distribution of the data
      - Identify outliers present in the data
      - Identify correlation in features of the dataset
  - [Data Visualization](https://github.com/nkiesz39/IBM_Data_Analyst_Capstone/blob/main/DataVisualization_Capstone.ipynb)
    - DataVisualization_capstone.ipynb
    - A Python notebook used to query a RDBMS with SQL and visualize the data.
    - Visualization Objectives:
      - Visualize the data distribution
        - Utilizing:
          - Histograms
          - Box Plots
      - Visualize relationships between features
        - Utilizing:
          - Scatter Plots
          - Bubble Plots
      - Visualize the composition of the data
        - Utilizing:
          - Pie Charts
          - Stacked Charts
      - Visualize comparison of the data
        - Utilizing:
          - Line Charts
          - Horizontal Bar Charts
  - [Capstone Presentation Slide Deck](https://github.com/nkiesz39/IBM_Data_Analyst_Capstone/blob/main/capstone_presentation.pdf)
    - The PowerPoint presentation of the project findings in a pdf format

## Guiding Questions
The aim of the project was to answer the questions:
  - What are the top programming languages in demand?
  - What are the top databases that are desired?
  - What are the most popular platforms?
  - Developer demographics

## Data
The job posting data comes from the Kaggles dataset [Jobs on Naukri.com](https://www.kaggle.com/datasets/promptcloud/jobs-on-naukricom). The dataset contains information on job listings. The data also comes from Stackoverflow's Annual Developer Survey. It is a comprehensive survey for developers that gathers information about the technologies and database systems currently in use. As well as the technologies and database systems developers want to learn. This data was gathered using web scraping and API calls.

*It should be noted that a random subset of the survey data is used for this analysis. Survey results and conclusions may vary with the use of the entire dataset.
  
## Exploratory Data Analysis
### Data Wrangling and Cleaning
#### Duplicates
During this step, the duplicated values were located. The duplicated Respondent rows were dropped.
#### Missing values
Missing values in the DataFrame were found using:

```df.isna().sum() ```

The code block results in the number of missing values from each column. 
The WorkLoc column had 32 missing entries. In order to not lose those rows of data, it was decided to impute the data. Using ```df['WorkLoc'].value_counts()``` results in the following:

![image](https://github.com/nkiesz39/IBM_Data_Analyst_Capstone/assets/73789208/79187384-c7c7-441f-8a35-4b61a848eac6)

With this information the missing values were replaced with the mode of the column, 'Office'.
#### Data Normalization
The dataset contains two columns about compensation, the pay and the frequency that it is recieved. The frequency is either, weekly, monthly, or yearly. In order to compare, a normalized column was added using the following code snippet and making a column that was the compensation for the entire year. 
```
annual_comp = []

def norm_AC():
    for x,y in zip(df['CompFreq'], df['CompTotal']):
        if x == 'Monthly':
            annual_comp.append(y*12)
        elif x== 'Weekly':
            annual_comp.append(y*52)
        else:
            annual_comp.append(y)
            
norm_AC()

df['NormalizedAnnualCompensation'] = annual_comp

df.head()
```
### EDA
#### Data Distribution
##### Compensation Distribution
The median of the compensation is 57745.0

##### Age Distribution
The age distribution is highest between 25-35 years old 

![image](https://github.com/nkiesz39/IBM_Data_Analyst_Capstone/assets/73789208/df01d68f-df71-4287-aef4-51aaea6aa214)

#### Outliers
Using a boxplot, the outliers for compensation were found. The IQR of the columns was calculated and used to identify the outliers using the fisrt and third quartiles: Q1 - (1.5 * IQR) and Q3 + (1.5 * IQR). 879 points fell outside this range and a new DataFrame was created where the outliers were removed.

#### Correlations 
The following is the correlation between the numerical columns:
![image](https://github.com/nkiesz39/IBM_Data_Analyst_Capstone/assets/73789208/a8579483-ed7c-47af-8a71-24d9a909e580)

Comensation is highly correlated with Age. 
## Data Visualizations

## Dashboard

## Conclusions
