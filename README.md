# IBM Data Analyst Capstone

## Background Information
This project was undertaken as a part of the IBM Data Analyst Professional Certificate Capstone course on Coursera.

For this project, we assume that we are a Data Analyst at a Global IT and Business Consulting Firm. In order to keep pace with changing technologies, the organization regularly analyzes data and trends to identify future skill requirements.

As a Data Analyst, we have been tasked with collecting data from various sources and identifying trends for this year's report on emerging technology skills. The purpose of the results are to aid developers and employers in staying relevant in the job market and guide employer training and upskilling support. 

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
## Dashboard
The following are screenshots of the Cognos Dashboard. The live dashboard can be found [here](https://dataplatform.cloud.ibm.com/dashboards/92117510-5e9e-4605-8f99-bb4f6e80756a/view/5e64a7606f9e10c467b5c0e407cd2b0428322758b7bbd602d1d47b4907687097a96d1498c8791e5adc190c66a5b915519d)

### Current Technology Dashboard
![image](https://github.com/nkiesz39/IBM_Data_Analyst_Capstone/blob/main/Screenshots/Current_Tech_dash.png)

### Future Technology Dashboard
![image](https://github.com/nkiesz39/IBM_Data_Analyst_Capstone/blob/main/Screenshots/Futue_Tech_dash.png)

### Demographics Dashboard
![image](https://github.com/nkiesz39/IBM_Data_Analyst_Capstone/blob/main/Screenshots/Demo_dash.png)


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
SQL queries were used in a Jupyter Notebook to access the RDBMS and visualize the data.

### Visualizing Data Distribution
A boxplot was used to visualize the distribution of the respondent's Age. The Median Age falls around 30 years old with outliers being older than 50-55 years old. 

![image](https://github.com/nkiesz39/IBM_Data_Analyst_Capstone/assets/73789208/87aed585-2ffc-4302-89bf-e4a69d8af556)

A hisotgram was used to visualize the distribution of the ConvertedComp column.

### Visualizing Relationships Between Features
The relationship between Age and Work Week Hours was visualized using a scatter plot. 

![image](https://github.com/nkiesz39/IBM_Data_Analyst_Capstone/assets/73789208/a8d1625f-08de-4718-a851-6b15ae4c5e9d)

A bubble plot was used to compare Work Week Hours on the X-axis, Code Review Hours on the Y-axis, and Age as the size of the bubbles. Code Review Hours is the amount of time spent per week reviewing documentation to aid in coding and understanding.

![image](https://github.com/nkiesz39/IBM_Data_Analyst_Capstone/assets/73789208/cc92aae8-0ea3-4c4f-b80e-c687524002ff)

### Visualizing Data Composition
Using a Pie chart, a the Top 5 Databases to learn were graphed. These are the Database Systems that developers have expressed interest in learning in the next year. 

![image](https://github.com/nkiesz39/IBM_Data_Analyst_Capstone/assets/73789208/ebfd6135-c1c3-4165-a690-3d2b0cde6f3e)

Using a Stacked chart, the median Work Week Hours and Code Review Hours were graphed for the age group of 30 - 35 years old. Overall, the age group works 40 hour Work Weeks and spends about 5 hours on Code Review in the week.

![image](https://github.com/nkiesz39/IBM_Data_Analyst_Capstone/assets/73789208/e4b0b306-458f-4937-b347-00f3563632a0)

### Visualizing Data Comparison
A line chart was used to graph the Median salary for the respondent's Age between 45 - 60 years old. While 60 year olds have the highest median salary overall, there are other peaks at 48, 54 and 57 years old. With the lowest median salary going to 49 year olds. 

![image](https://github.com/nkiesz39/IBM_Data_Analyst_Capstone/assets/73789208/a7915f2a-196b-4d90-a5e6-45f9fbcae325)

Finally, a horizontal bar chart was used to visualize the counts of whether respondents are Developers as a job or not. 
![image](https://github.com/nkiesz39/IBM_Data_Analyst_Capstone/assets/73789208/d50e7fec-65f3-46de-a98f-1b722837b580)

## Conclusions
