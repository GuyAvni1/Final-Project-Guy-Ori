# Preproccesing Steps:
### 1. DataPreparation
  In this part, we take the raw data given by ADNI and preprocess it to give a line for each patient's visit.<br> 
  The reads **ADNIMERGE.csv** (from ADNI) and return **df_prepared.csv**.
### 2. ParticipantSelection
  In this part we remove unwanted patients.<br> 
  Such as patients transforming from CN to MCI and back to CN, patients transforming from CN to AD, and so on.<br>
  The code creates for each patient a single line.<br> 
  The code reads **df_prepared.csv** and return **df_ps.csv**.
### 3. Data_after_ps
  In this part we combine both DataPreparation and ParticipantSelection.<br>
  We remove all the patients from df_prepared.csv who don't appear in df_ps.<br>
  We are left with a copy of df_prepared.csv but only with the patients appearing in df_ps.csv.<br>
  The code reads **df_prepared and df_ps.csv** and returns **df_prepared_after_ps.csv**.
### 4. Null_Filling
  In this part, we are filling in missing data in the df_prepared_after_ps.csv file. <br>
  We are using HistGradientBoostingRegressor to fill in missing data.<br>
  The code reads **df_prepared_after_ps.csv** and return **df_imputed.csv**.
### 5. Preparation_for_Prediction
  In this part, we create a separate .csv file for prediction.<br>
  Each file is created with a time-space of 'month' (a changeable variable in the code) months.<br>
  The code creates future_of_12m.csv file which contains the same features in df_imputed.csv,<br>
  but adds a column called 'Transition' which will be the transition label of each patient in the specific time-space.<br>
  Assume month = 12 (1 year) and we get the label CNtoMCI in the Transition column. <br>
  The label means the patient changed his state from CN to MCI in one year.
