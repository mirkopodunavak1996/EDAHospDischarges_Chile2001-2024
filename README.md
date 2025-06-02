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

- **Processed Data in parquet format with column names and data types updated, ready for a deeper cleaning**  
  - [Egresos_cleaned.parquet](https://www.kaggle.com/datasets/mirkopodunavak/egresos-hospitalarios-2001-2020)

- **Processed and cleaned Data in parquet format, ready to use in the EDA phase of the project for the general analysis**  
  - [General_analysis_data.parquet](https://www.kaggle.com/datasets/mirkopodunavak/egresos-hospitalarios-2001-2020)

- **Processed and cleaned Data in parquet format, ready to use in the EDA phase of the project for the readmission analysis**  
  - [Readmissions.parquet](https://www.kaggle.com/datasets/mirkopodunavak/egresos-hospitalarios-2001-2020)

You can download the dataset files from: (https://www.kaggle.com/datasets/mirkopodunavak/egresos-hospitalarios-2001-2020).

Project overview (PENDIENTE):

This project focuses on cleaning and preparing the Egresos Hospitalarios dataset for analysis. The raw dataset contains hospital discharge data from 2001 to 2020, and this repository tracks the steps taken to clean, preprocess, and transform the data for analysis.

DATA IMPORTATION NOTEBOOK

1.	Data Cleaning Overview
The data cleaning process was essential to join all the 20 datasets together, ensuring accuracy and completeness before starting the analysis. The main steps taken during this process are detailed in the Jupyter notebook located in the notebooks folder called "data_importation". Below is a summary of the key steps:

2.	Data Inspection and importation

In this first step, I examined the glossary of definitions (TRACKEAR EN GIT EXCEL FICHA EGRESOS HOSPITALARIOS) for the columns in the datasets (all them share the same columns) to decide which ones are useful for the project purpose. After making that decision I imported the datasets with the relevant columns, change some data types to simplify future analysis and applied transformatios over specific columns to improve the understanding of their values.

3.	Handling Missing Data

Considering the datasets are large (at least 1.000.000 records each) and that the joint dataset consists on 26.340.655 rows that represent the total population that have been subject of a hospital discharge, it was chosen to just delete rows that at least contained one column with missing values except on "Patient ID" and "Healthcare facility name”. Around 7% of the IDs were null and in the “data_cleaning” notebook the missingness of the IDs was analyzed in relation to the rest of the columns before making decision about handling those null values. The null “Healthcare facility names” values were imputed to “unknown” instead of deleting them to avoid losing valuable data from the rest of the columns. Based on the Central Limit Teorem, deleting a relatively small proportion of rows that at least had 1 missing value column from a big sample it is not going to affect the measures of dispersion and central tendency that give a good understanding of the nature of the data and relations to be explored.

Various techniques were applied, including:
-	Removing rows with at least one value column with missing data.
-	Standardizing Value Columns and Data Types



DATA_CLEANING NOTEBOOK:
1.	Customizing data types and column names
Inconsistent column names and data types can cause issues when performing analyses, so I standardized them throughout the dataset. This step includes:
-	Renaming columns for clarity and consistency.
-	Converting columns to appropriate data types (e.g., date columns to datetime).
For more information, check the specific transformations done in the notebook.

2.	Exploring missing Patient IDs:
Overall, the percent of NaN Patient IDs is 7% which is not very high considering that most of them are for newborns or births. So, the decision is about how to handle the missing IDs depending on the nature of the missingness on each column and choose to delete the rows with NaN IDs or impute those values. Before deciding, it was necessary to analyze each result for the variables after grouping the missing IDs with them.

Age: Most of the NaN IDs are for newborns and then the trend is steady and slightly decreases after the age of 60. In this project it is going to be assumed that the correlation between age and being alive especially after 60 years old is negative, so the amount of people with that age is less and consequently the number of NaN IDs.
Type of Missingness: MAR

Healthcare facility name: The proportion of NaN IDs is remarkably higher in some healthcare facilities, but there was not found information about personal data management polices on the website nor via e-mail with the institutions. The NaN IDs in some hospitals were 100% , so for them was not possible to analyze readmissions.
Type of Missingness: MAR

Discharge condition, Health insurance and Sex: As expected mainly alive people have NaN IDs more than death because less people die in a hospital discharge. So there is no evidence to think that there is a specific decision of having NaN IDs considering this variable. The same happens with sex and health insurance: the amount of men and women and Fonasa and Isapre that have NaN IDs is proportional to the valid values, respectively.
Type of Missingness: MCAR

Year: Over time the amount of NaN IDs has been decreasing progressively and probably it is because of improvements in patient data recording and changes in policies that allow better tracing or follow-up of the health history of the patients. To analyze readmissions, it is going to be considered only rows from the year 2008 onwards because between 2007 and 2008 there was a big decrease on missing NaN IDs, so the revisits before 2008 could be underestimated.
Type of Missingness: MAR

Diagnosis: The amount of NaN Patient IDs considering the diagnosis do not show a clear relation with specific diseases or health conditions. In the first place only very rare (not frequent) diagnosis have 100% NaN Patient IDs. Secondly the most frequent and with higher percent of NaN Patient IDs were mainly births and a diagnosis denominated "other physical therapies". However, for the most common births (in general the ones without issues during the procedure) the frequency is high, but the percent of NaN is low. Lastly, the "score" column created out of the max/min normalization shows that there are no diagnoses with an unexpectedly high number AND percent of NaN patient IDs that could highlight an issue related to the diagnosis variable.
Type of Missingness: MAR

Length of stay: central tendency measures for length of stay is similar between NaN and valid IDs; 5,15% of NaN IDs are outliers(long stays) whereas 5,56% of valid ID are anomalies, which is similar for both of the distributions and not unusual to an alarming point; mental health and nutrition issues are consistently associated with both NaN and valid IDs; and the distribution of outliers for NaN and valid IDs is similar. All this shows that the missigness of patient IDs related to the length of the stay is at random (MAR).
Type of Missigness: MAR


General conclusion about missing data

The decision about the missing data is to delete it in all the variables (Sex, Age, Health insurance, Healthcare facility type, Length of stay, Discharge condition, Primary diagnosis code, Primary diagnosis name, Year) without analyzing the missigness of them (which was done in the notebook “data_importation”) except on "Patient ID" for which the nature of their null values was analyzed, and "Healthcare facility name". 
All the variables except of these 2 are related to each other considering the purpose of the project and the core questions, so having missing data in at least one of those variables can lead to bias in the analysis; even after deleting some rows, the dataset still contains a large number of observations (around 26 million), which ensures that the data remains representative of the population. According to the central limit theorem, a sufficiently large sample size allows for reliable statistical inference.

The "Patient ID" missing data was not deleted in the main dataframe (called “df_final” in the jupyter notebook) because the IDs are not related to the rest of the variables considering the guiding questions of this project in a way that bias could be introduced, as it is shown in an analysis of the NaN values in relation to the rest of the columns. The missingness of the IDs in relation to the other variables was completely at random (MCAR) or at random (MAR) as it was shown above. That, including other aspects that are explained in the jupyter notebook file, contribute to the decision of keeping the rows with NaN ID values in the “df_cleaned” dataframe, but deleting the column itself to make the file lighter.

However, the NaN IDs were deleted in the dataframe to be used to analyze readmissions (“df_readmissions”) and just the valid IDs were kept for the analysis of readmissions and patient journeys, that only considers from the year 2008 onwards, due to possible underestimations of readmissions in the previous years because the decrease of NaN IDs is progressive over the years, reaching a steady trend from that year, as stated in the jupyter notebook file.
Aside from this, the "Healthcare facility name" is not a meaningful variable for the project compared to the data that would be lost if the rows with missing data in this column were deleted, but it is useful to identify each hospital to analyze efficiency and other important issues, so the NaN values were imputed to "Unknown".

Various techniques were applied to handle missing data, including:
-	Group by each column to analyze missingness of the data in relation to Patient IDs
-	Impute missing values in “Healthcare facility name” with a constant “Unknown” to avoid losing valuable data from other columns
-	Deleting rows with missing values in “Patient ID” column before exporting readmission analysis dataframe
-	Outliers’ detection techniques for variables related to missing Patient IDs, such as interquartile range method (IQR).
-	Apply logarithmic transformations to normalize length of stay outliers for missing Patient IDs and visualize them with histograms
For more information, check the specific process done in the notebook.



3.	Handling Duplicates
Duplicated rows were identified and removed, except the first occurrence, but all the duplicates were kept if the Patient ID was missing for the general analysis (these were deleted for readmissions analysis) as it is impossible to know if the rows represent a real duplicated (data entry error) or repeated events (different patient but same value columns) with the information available. It was chosen to acknowledge this uncertainty and keep the rows with missing IDs because the data that would be lost from the rest of the columns apart of it is important at an aggregate level of analysis, however the rows were deleted for readmission analysis, because it is necessary to identify the patient. This strategy allows us to keep the data when the goal is to analyze it at an aggregate level (general analysis) and delete it when the focus is on individual patients (readmissions analysis).

Various techniques were applied to handle duplicates, including:
-	Keep the first occurrence of a full duplicated value and deleting the rest
-	Splitting the data to then concatenate it based on the decision previously explained
The exact steps for identifying and handling duplicates can be found in the notebook.

4.	Final Dataset Format and Export
After the cleaning process, 2 datasets were exported for further analysis as a parquet file to ensure more speed to import and process it.

Dataset “df_cleaned”: includes all the data from the year 2001 to 2020 with patients with and without ID. The data is ready to be analyzed at an aggregate level for the general analysis that explores the main questions in this project.

Dataset “df_readmissions”: includes the data from the year 2008 to 2020, because the number of patients without IDs was lower than previous years, allowing to make the estimation of readmissions more accurate. This dataset does not include patients with NaN IDs as this is necessary for the analysis.

5.	About the notebook and cleaning process

All detailed steps, code, and explanations are available in the Jupyter notebook here: Notebook Link
The notebooks provide a step-by-step breakdown of the actions taken, including code snippets, visualizations, and reasoning behind the decisions made during the cleaning process.

Why the cleaning process was important

The data cleaning steps were critical in preparing the dataset for meaningful analysis depending on the goal, but also to understand the original structure of the data to make every step contribute for a future analysis that is not biased and provides valid and actionable insights for a broad range of stakeholders.
By following these steps, I have ensured that the data is:
-	Free from inconsistencies: valid values, correct column names and data types and others
-	Ready for exploratory data analysis and further modeling.
-	Easily interpretable and usable for stakeholders.

Conclusion
The README serves as a high-level guide to the data cleaning process, and all the detailed steps, including the code used, can be found in the notebooks folder. Feel free to refer to the notebook for a deeper understanding of the cleaning process and how each decision was made.



