**Index**

* Description of the Original Data
* Description of the Manipulated Data
* Description of the Variables
* Steps to clean up and summarize the data

**Original Data**

From the Original Data documentation:
"The experiments have been carried out with a group of 30 volunteers within an age bracket of 19-48 years. Each person performed six activities (WALKING, WALKING-UPSTAIRS, WALKING-DOWNSTAIRS, SITTING, STANDING, LAYING) wearing a smartphone (Samsung Galaxy S II) on the waist. Using its embedded accelerometer and gyroscope, we captured 3-axial linear acceleration and 3-axial angular velocity at a constant rate of 50Hz. The experiments have been video-recorded to label the data manually. The obtained dataset has been randomly partitioned into two sets, where 70% of the volunteers was selected for generating the training data and 30% the test data."

For more information about the original data, see the `study_readme.txt` file.

**Submitted Data**

From the original data, only the variables that measured the means and standard deviations of the various features were retained. This values were then averaged for each subject and activity.

The first column is called ``subject``. The values are integers representing the volunteer whose data is being shown.
The second column is called ``activity``. These are the same six activities described in the Original Data description. The possible values for this column are WALKING, WALKING-UPSTAIRS, WALKING-DOWNSTAIRS, SITTING, STANDING, LAYING.

For each of the 30 subjects and each of the 6 activities, the data contains the average of the following measures:

 1 .  fBodyAcc.mean.X   
 2 .  fBodyAcc.mean.Y   
 3 .  fBodyAcc.mean.Z   
 4 .  fBodyAcc.std.X   
 5 .  fBodyAcc.std.Y   
 6 .  fBodyAcc.std.Z   
 7 .  fBodyAccJerk.mean.X    
 8 .  fBodyAccJerk.mean.Y   
 9 .  fBodyAccJerk.mean.Z   
 10 .  fBodyAccJerk.std.X   
 11 .  fBodyAccJerk.std.Y   
 12 .  fBodyAccJerk.std.Z   
 13 .  fBodyGyro.mean.X   
 14 .  fBodyGyro.mean.Y  
 15 .  fBodyGyro.mean.Z  
 16 .  fBodyGyro.std.X  
 17 .  fBodyGyro.std.Y  
 18 .  fBodyGyro.std.Z  
 19 .  tBodyAcc.mean.X  
 20 .  tBodyAcc.mean.Y  
 21 .  tBodyAcc.mean.Z  
 22 .  tBodyAcc.std.X  
 23 .  tBodyAcc.std.Y  
 24 .  tBodyAcc.std.Z  
 25 .  tBodyAccJerk.mean.X  
 26 .  tBodyAccJerk.mean.Y  
 27 .  tBodyAccJerk.mean.Z  
 28 .  tBodyAccJerk.std.X  
 29 .  tBodyAccJerk.std.Y  
 30 .  tBodyAccJerk.std.Z  
 31 .  tBodyGyro.mean.X  
 32 .  tBodyGyro.mean.Y  
 33 .  tBodyGyro.mean.Z  
 34 .  tBodyGyro.std.X  
 35 .  tBodyGyro.std.Y  
 36 .  tBodyGyro.std.Z  
 37 .  tBodyGyroJerk.mean.X   
 38 .  tBodyGyroJerk.mean.Y   
 39 .  tBodyGyroJerk.mean.Z   
 40 .  tBodyGyroJerk.std.X   
 41 .  tBodyGyroJerk.std.Y  
 42 .  tBodyGyroJerk.std.Z  
 43 .  tGravityAcc.mean.X  
 44 .  tGravityAcc.mean.Y  
 45 .  tGravityAcc.mean.Z  
 46 .  tGravityAcc.std.X  
 47 .  tGravityAcc.std.Y  
 48 .  tGravityAcc.std.Z 
 
For detailed information about these measures, please see ``features_info.txt``.


**Steps to clean up the data**

1. A total of 8 data files were read into R. They contained the following data:  
   *  X_test: test set containing the measurements for each of the original variables  
   *  y_test: test set containing the activity value, stored separately    
   *  subject_test: test set containing the subject indicator, stored separately   
   *  X_train: train set containing the measurements for each of the original variables  
   *  y_train: train set containing the activity value, stored separately  
   *  subject_train: train set containing the subject indicator, stored separately  
   *  features: set containing the names of the columns for X_test and X_train  
   *  labels: table containing the descriptions corresponding to the activity values  

2. Combined each train data with its corresponding test data (e.g. X_test with X_train)

3. Used the values in the features file to rename the columns in the dataset containing the measurements of the features

4. Combined all the data - measurements, activity values, subject values

5. Changed the names of the columns using make.names to allow for melting

6. Melted the data into a long form

7. Renamed the activity values according to the labels table for clarity

8. Grouped the long data by subject and activity, then summarized it by its mean.

9. Used `cast` to transform this data into a wide format, having a single row for each subject-activity combination, and a column for each measurement for that observation.
