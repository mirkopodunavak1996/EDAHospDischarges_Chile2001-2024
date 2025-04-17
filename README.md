## Dataset Structure
The dataset is stored on Kaggle and consists of the following files:

- **Raw Data**  
  - [Egresos_Hospitalarios_2001.csv](https://www.kaggle.com/datasets/mirkopodunavak/egresos-hospitalarios-2001-2020)
  - [Egresos_Hospitalarios_2002.csv](https://www.kaggle.com/datasets/mirkopodunavak/egresos-hospitalarios-2001-2020)
  - [Egresos_Hospitalarios_2003.csv](https://www.kaggle.com/datasets/mirkopodunavak/egresos-hospitalarios-2001-2020)
  - [Egresos_Hospitalarios_2004.csv](https://www.kaggle.com/datasets/mirkopodunavak/egresos-hospitalarios-2001-2020)
  - [Egresos_Hospitalarios_2005.csv](https://www.kaggle.com/datasets/mirkopodunavak/egresos-hospitalarios-2001-2020)
  - [Egresos_Hospitalarios_2006.csv](https://www.kaggle.com/datasets/mirkopodunavak/egresos-hospitalarios-2001-2020)
  - [Egresos_Hospitalarios_2007.csv](https://www.kaggle.com/datasets/mirkopodunavak/egresos-hospitalarios-2001-2020)
  - [Egresos_Hospitalarios_2008.csv](https://www.kaggle.com/datasets/mirkopodunavak/egresos-hospitalarios-2001-2020)
  - [Egresos_Hospitalarios_2009.csv](https://www.kaggle.com/datasets/mirkopodunavak/egresos-hospitalarios-2001-2020)
  - [Egresos_Hospitalarios_2010.csv](https://www.kaggle.com/datasets/mirkopodunavak/egresos-hospitalarios-2001-2020)
  - [Egresos_Hospitalarios_2011.csv](https://www.kaggle.com/datasets/mirkopodunavak/egresos-hospitalarios-2001-2020)
  - [Egresos_Hospitalarios_2012.csv](https://www.kaggle.com/datasets/mirkopodunavak/egresos-hospitalarios-2001-2020)
  - [Egresos_Hospitalarios_2013.csv](https://www.kaggle.com/datasets/mirkopodunavak/egresos-hospitalarios-2001-2020)
  - [Egresos_Hospitalarios_2014.csv](https://www.kaggle.com/datasets/mirkopodunavak/egresos-hospitalarios-2001-2020)
  - [Egresos_Hospitalarios_2015.csv](https://www.kaggle.com/datasets/mirkopodunavak/egresos-hospitalarios-2001-2020)
  - [Egresos_Hospitalarios_2016.csv](https://www.kaggle.com/datasets/mirkopodunavak/egresos-hospitalarios-2001-2020)
  - [Egresos_Hospitalarios_2017.csv](https://www.kaggle.com/datasets/mirkopodunavak/egresos-hospitalarios-2001-2020)
  - [Egresos_Hospitalarios_2018.csv](https://www.kaggle.com/datasets/mirkopodunavak/egresos-hospitalarios-2001-2020)
  - [Egresos_Hospitalarios_2019.csv](https://www.kaggle.com/datasets/mirkopodunavak/egresos-hospitalarios-2001-2020)
  - [Egresos_Hospitalarios_2020.csv](https://www.kaggle.com/datasets/mirkopodunavak/egresos-hospitalarios-2001-2020)

- **Processed Data in CSV and parquet format with raw data cleaned and concatenated**  
  - [Egresos_2001-2020.parquet](https://www.kaggle.com/datasets/mirkopodunavak/egresos-hospitalarios-2001-2020)
  - [Egresos_2001-2020.csv](https://www.kaggle.com/datasets/mirkopodunavak/egresos-hospitalarios-2001-2020)

You can download the dataset files from: (https://www.kaggle.com/datasets/mirkopodunavak/egresos-hospitalarios-2001-2020).

Project overview (PENDIENTE):

This project focuses on cleaning and preparing the Egresos Hospitalarios dataset for analysis. The raw dataset contains hospital discharge data from 2001 to 2020, and this repository tracks the steps taken to clean, preprocess, and transform the data for analysis.

DATA_CLEANING NOTEBOOK (Cambiar a data importation)

Data Cleaning Overview
The data cleaning process was essential to join all the 20 datasets together, ensuring accuracy and completeness before starting the analysis. The main steps taken during this process are detailed in the Jupyter notebook located in the notebooks folder called "data_cleaning". Below is a summary of the key steps:

Data Inspection and importation

In this first step, I examined the glossary of definitions (TRACKEAR EXCEL FICHA EGRESOS HOSPITALARIOS) for the columns in the datasets (all them share the same columns) to decide which ones are useful for the project purpose. After making that decision I imported the datasets with the relevant columns, change some data types to simplify future analysis and applied transformatios over specific columns to improve the understanding of their values.

Handling Missing Data

Considering the datasets are large (at least 1.000.000 records each) and that the joint dataset consists on 26.340.655 rows that represent the total population that have been subject of a hospital discharge, it was chosen to just delete rows that at least contained one column with missing values except on "ID_PACIENTE" and "GLOSA_ESTABLECIMIENTO_SALUD", because around 7% of the data on that colum mas null and the data is not as relevant compared to the value that the other columns provide, respectively . Based on the Central Limit Teorem, deleting some values from a big sample it is not going to affect the measures of dispersion and central tendency that give a good understanding of the nature of the data and relations to be explored.

Various techniques were applied, including:

Removing rows with at least one value column with missing data.

Standardizing Value Columns and Data Types



NOTEBOOK ANALISIS_P1 (CAMBIAR NOMBRE A: DATA_CLEANING):

Inconsistent column names and data types can cause issues when performing analyses, so I standardized them throughout the dataset. This step includes:

Renaming columns for clarity and consistency.

Converting columns to appropriate data types (e.g., date columns to datetime).

For more information, check the specific transformations done in the notebook.

Exploring missing IDs:
Overall the percent of NaN Patient IDs is 7% which is not very high considering that most of them are for newborns or births. So the decision it is about how to handle the missing IDs depending of the nature of the missingness on each column and choose to delete the rows with NaN IDs or impute those values. Before deciding, lets analyze each result for the variables after grouping the missing IDs with them.

Age: Most of the NaN IDs are for newborns and then the trend is steady and slightly decreases after the age of 60. In this project it is going to be assumed that the correlation between age and being alive especially after 60 years old is negative, so the amount of people with that age is less and consequently the number of NaN IDs.
Type of Missingness: MAR

Healthcare facility: The number of NaN IDs is remarkably higher in "Hospital Clinico Universidad Catolica", but there was not found information about personal data management polices on the website nor via e-mail with the institution.
Type of Missingness: MAR

Discharge condition, Health insurance and Sex: As expected mainly alive people have NaN IDs more than death because less people die in a hospital discharge. So there is no evidence to think that there is a specific decision of having NaN IDs considering this variable. The same happens with sex and health insurance, the amount of men and women and Fonasa and Isapre that have NaN IDs is proportional to the valid values, respectively.
Type of Missingness: MCAR

Year: Over the time the amount of NaN IDs has been decreasing progressively and probably it is beacuse of improvements in patient data recording and changes in policies that allow better tracing or follow-up of the health history of the patients. To analyze revisits it is going to be considered only rows from the year 2008 onwards beacuse between 2007 and 2008 there was a big decrease on missing NaN IDs, so the revisits before 2008 could be underestimated.
Type of Missingness: MAR

Diagnosis: The amount of NaN Patient IDs considering the diagnosis do not show a clear relation with specific diseases or health conditions. In the first place only very rare diagnosis have 100% NaN Patient IDs. Secondly the most frequents and with higher percent of NaN Patient IDs and mainly births and a diagnosis denominated "other physical therapies". However, for the most common births (in general the ones without issues during the procedure) the frequency is high, but the percent of NaN is low and the "score" column created out of the max/min normalization shows that there are not diagnosis with high frequency AND high percent of NaN IDs.
This shows that there are not diagnosis with an unexpectedly high number AND percent of NaN patient IDs that could highlight an issue related to the diagnosis variable.
Type of Missingness: MAR

Lenght of stay:



General conclusion about missing data: 
The decision about the missing data is to delete it in all the variables (Sex, Age, Health insurance, Healthcare facility type, Length of stay, Discharge condition, Primary diagnosis code, Primary diagnosis name, Year) except on "Patient ID" and "Healthcare facility name". All the variables except of these 2 are related to each other considering the purpose of the project and the core questions, so having missing data in at least one of those variables can lead to bias in the analysis; the amount of rows left is still very high (around 26 millions) so the data size is still representative of the population. The "Patient ID" missing data is not going to be deleted because is not related to the rest of the variables consdiering the guiding questions of this project, except of the analysis of readmissions and patient journeys. In that sense, a separated dataframe was created to analyze this considering the year 2008 onwards. The "Healthcare facility name" is not a meaningfull variable for the project compared to the data that would be lost if the rows with missing data in this column are deleted, so the value NaN values was imputed to "Desconocido".

Removing Duplicates

Duplicate rows were identified and removed to ensure that the dataset reflects unique records only.

The exact criteria for identifying duplicates can be found in the notebook.

Handling Outliers

Some extreme values were detected during the exploratory analysis.

These outliers were reviewed, and decisions were made on whether to keep, adjust, or remove them based on their impact on the analysis.

Detailed code and visualizations of outlier detection are available in the notebook.

Final Dataset Format and Export

After the cleaning process, I ensured the dataset was in a format suitable for analysis.

The cleaned dataset was exported as both a CSV file and a Parquet file for use in future analysis.

Notebook Link
All detailed steps, code, and explanations are available in the Jupyter notebook here:
Data Cleaning Notebook

The notebook provides a step-by-step breakdown of the actions taken, including code snippets, visualizations, and reasoning behind the decisions made during the cleaning process.

Why This Process Was Important
The data cleaning steps were critical in preparing the dataset for meaningful analysis. A clean, well-organized dataset is essential to avoid biased results, improve model performance, and ensure that insights derived from the data are valid and actionable. (HACER RESTO MIO Y ORIGINAL)

By following these steps, I have ensured that the data is:

Free from inconsistencies.

Ready for exploratory data analysis and further modeling.

Easily interpretable and usable for stakeholders.

Conclusion
The README serves as a high-level guide to the data cleaning process, and all the detailed steps, including the code used, can be found in the notebooks folder. Feel free to refer to the notebook for a deeper understanding of the cleaning process and how each decision was made.


