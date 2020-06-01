<img src=images/Hospital-Ward-image-2.jpg width="875" height="500">

## Predicting patients with poor outcomes (hospital readmissions) from Medical Insurance Claims Data (Readme - WIP)

In this project, I am trying to predict patients with poor outcomes by using the frequency and duration of patient visit, their usage of prescription drugs and other products & services. I do not have access to any medical information such as vitals, test results, scans or any other kind of diagnostic tests. <i> Challenge is to predict worsening of patient's health without the medical information.</i>


### Background
Overall 20% of the sickest patients consume 80% of the healthcare resources, be it cost or resource occupancy. Being able to predict the outcome (usually poor outcome) of a patient early-on can not only help in taking pre-emptive efforts to manage the condition but also help in managing the workload of the healthcare system thereby reducing cost and enhancing quality of life. 

### Can the insurer with only limited medical information such as disease diagnosis code, billing for the equipments, services and drugs used be able to predict the poor outcome of its clients. This project is an attempt to try this.

<img src=images/health_insurance.jpg width="265" height="200">


Steps:
1. Data Collection
2. Data Wrangling & Preparation
  2 a. Creating PostgreSQL database
3. Exploratory Data Analysis 
4. Feature Engineering
5. Machine Learning Models 
  5 a. Setting up and running the models in Tensorflow environment in Amazon Web Services (AWS)
6. Hyper parameter tuning (including dealing with class imbalance)
7. Comparing all the classification model's performance 
8. Conclusion and Key learning
9. Future work


### 1. Data Collection
Data was collected from Center for Medicare and Medicaid Services (CMS), USA. It contains data for around 7m patients, with 1.3m inpatient, 16m outpatient visit and 111m prescription drug events and other medical claims data. 

<img src=images/CMS.png width="220" height="100"> 

I started with around quarter million patients for exploratory data analysis. After seeing some trends between predictor  and the target variables, finally I used one-fifth of the available data. Prime reason for using the limited amount of data was because of limitation of RAM on my machine and to limit the expenditure on AWS.
	
### 2. Data Wrangling & Preparation

 <img src=images/size.png width="400" height="200">
 
1. Each patient can have multiple inpatient and outpatient visits
2. Each visit can have multiple ICD9 (diagnosis) assigned for each visit
3. There are 20,000 disease, 13,000 HCPCS and 4,000 procedure codes
 
  ### 2 a. Creating PostgreSQL database
  
  <img src=images/postgre_database.png width="500" height="300">
  
  ### 3. Exploratory Data Analysis 
  
   <img src=images/corelation_matrix.png width="600" height="450">
   
   <img src=images/feature_distribution.png width="600" height="450">
   
  
  ### 4. Feature Engineering
  
   <img src=images/num_inpt_admissions.png width="425" height="300"> <img src=images/los.png width="425" height="300">
   
   <img src=images/total_inpt_diagnosis.png width="425" height="300"> <img src=images/total_inpt_procedures.png width="425" height="300">
   
   
  <img src=images/summarized_by_patient.png width="900" height="350">
  
  
  ### 7. Comparing all the classification model's performance 
   <img src=images/scores.png width="700" height="500">
   
   <img src=images/feature_imp_random_forest.png width="700" height="500">
  
  ### 8. Conclusion and key learning
  1. Data wrangling is fast in SQL
2. Oversampling improves the accuracy (Logistic Regression from 0.75 to 0.86)
3. Polynomial features improved accuracy
4. PCA reduced my features from 14,000 to 500 with 82% cumulative variance
5. KNN was the slowest
6. Ensemble methods gave the best results
7. Gradient Boosting was the clear winner as it reduced bias. It had higher false positives hence lower precision for class 1 (preferred)
8. Random Forest seems to have a good balance between model accuracy and resource utilization (7mins vs 25 mins for Gradient Boosting)

  
  ### 9. Future work
  Since now the data is processed, I would like to do the following projects:
1. Cost prediction
2. Predicting Chronic Disease for a patient
3. Bundling procedures & payments (based on predicting future medical conditions) for preemptive meaasures 
4. Flag high cost hospitals and physicians with poor outcomes
