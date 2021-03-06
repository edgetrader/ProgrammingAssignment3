## Background
Data used in this assignment are downloaded from UCI Machine Learning Repository.  It is a Human Activity Recognition database built from the recordings of 30 subjects performing activities of daily living (ADL) while carrying a waist-mounted smartphone with embedded inertial sensors.
	
In summary, the experiments have been carried out with a group of 30 volunteers within an age bracket of 19-48 years. Each person performed six activities (WALKING, WALKING_UPSTAIRS, WALKING_DOWNSTAIRS, SITTING, STANDING, LAYING) wearing a smartphone (Samsung Galaxy S II) on the waist. 
Using its embedded accelerometer and gyroscope, 3-axial linear acceleration and 3-axial angular velocity at a constant rate of 50Hz are captured. The obtained dataset has been randomly partitioned into two sets, where 70% of the volunteers was selected for generating the training data and 30% the test data. 


## The Raw Data
The dataset is downloaded from the following URL:

[https://d396qusza40orc.cloudfront.net/getdata%2Fprojectfiles%2FUCI%20HAR%20Dataset.zip]

The downloaded files can be categorised as follows:
### 1) Explanatory
* <B>README.txt</B> : Background information on what kind of experiment is conducted and what kind of data are gathered
* <B>features_info.txt</B> : Summary with explanation on what kind and how the variables in the experiments are collected and calculated

### 2) Data Labels
* <B>activity_labels.txt</B> : Store the list of 6 activities performed by the volunteers
* <B>features.txt</B> : Store the list of 561 variables collected and calculated for further data analysis
* <B>train/y_train.txt</B> : Store the activity ids corresponding to each test record in the training data set 
* <B>test/y_test.txt</B> : Store the activity ids corresponding to each test record in the test data set 
* <B>train/subject_train.txt</B> : Store the subject ids corresponding to each test record in the training data set 
* <B>test/subject_test.txt</B> : Store the subject ids corresponding to each test record in the test data set 

### 3) Data
* <B>train/X_train.txt</B> : Store the data collected and calculated for 561 variables of each test record in the training data set
* <B>test/X_test.txt</B> : Store the data collected and calculated for 561 variables of each test record in the test data set

### 4) Additional Data - (Not used in this project)
* <B>train/Inertial Signals/total_acc_x_train.txt</B>
* <B>train/Inertial Signals/body_acc_x_train.txt</B>
* <B>train/Inertial Signals/body_gyro_x_train.txt</B>
* <B>test/Inertial Signals/total_acc_x_test.txt</B>
* <B>test/Inertial Signals/body_acc_x_test.txt</B>
* <B>test/Inertial Signals/body_gyro_x_test.txt</B>



## The Processed Data (using R Programming)
On studying the raw data set, a few observations are noted:<br><br>
1. Both the training and test variable data sets does not come with heading.  Each come with 561 columns corresponding to 561 variables for each test record in the training and test data set.<br>
2. The feature.txt stores the raw column names of the 561 variables.  For this assignment, we are only interested in the mean() and std() variables.  The required subset of variables will be filtered out from the 561 variables.<br>
3. The 30 volunteers also called 'subjects' are indexed and labelled 1 to 30<br>
4. The 6 activities are indexed 1 to 6 and given labels correspondingly as WALKING, WALKING_UPSTAIRS, WALKING_DOWNSTAIRS, SITTING, STANDING, LAYING<br><br>

To prepare tidy data, the following steps are done:<br><br>
1. Load in the features.txt into <B>feature</B>.<br>
2. Obtain the required variables mean() and std() from <B>feature</B> and store in <B>reqFeature</B>.  There are a total of 66 required variables.<br>
3. Clean up and format the variable names to be more descriptive to be used for column name in the training and test data set.  Read run_analysis.R lines 27 to 35 for column name format definition.<br>
4. Load the activity_labels.txt into <B>activity</B> and give it column names.<br>
5. Load the training and test data set into <B>Xtrain</B> and <B>Xtest</B> respectively.<br>
6. Load the activity ids corresponding to each test record of the training and test data set into <B>ytrain</B> and <B>ytest</B> respectively.<br>
7. Load the subject ids corresponding to each test record of the training and test data set into <B>subtrain</B> and <B>subtest</B>.<br>
8. Scope <B>Xtrain</B> and <B>Xtest</B> down by selecting only the required 66 variables using <B>reqFeature</B> as a filtering criteria.<br>
9. Update column names for <B>Xtrain</B>, <B>Xtest</B>, <B>ytrain</B>, <B>ytest</B>, <B>subtrain</B> and <B>subtest</B>.<br>
10. Column bind the training data set with subject ids and activity ids into <B>train</B>.<br>
11. Column bind the test data set with subject ids and activity ids into <B>test</B>.<br>
12. Row bind the training and test data set into <B>tidydata</B>.<br>
13. Set subject and activity in <B>tidydata</B> as factors.  Activity will be given factors labels.<br>
14. <B>tidydata</B> completed for further analysis.<br><br>


## tidydata Variables

The first 2 columns are 'subject' and 'activity'.<br>
<B>'subject'</B> is the id of volunteer performing the test.  Range from 1 to 30.<br>
<B>'activity'</B> is activity that the volunteer is performing during the test.  Namely, WALKING, WALKING_UPSTAIRS, WALKING_DOWNSTAIRS, SITTING, STANDING or LAYING<br>

All other variables are given more descriptive names formatted based on the following properties in order (left to right):<br>
* 't' or 'f' - (t for Time, f for Frequency)<br>
* 'Gravity' or 'Body'<br>
* 'Acc' or 'Gyro' - (Acc for Accelerometer, Gyro for Gyroscope)<br>
* 'Jerk' - (ignore if not required)<br>
* 'Mean' or 'Std' - (Mean or Standard Deviation)<br>
* 'X', 'Y', 'Z' or 'M' - (X, Y and Z for 3 dimensional signals.  M for Magnitude calculated based on X,Y,Z using the Euclidean form) <br>

### List
1. subject<br>
2. activity<br>
3. tBodyAccMeanX<br>
4. tBodyAccMeanY<br>
5. tBodyAccMeanZ<br>
6. tGravityAccMeanX<br>
7. tGravityAccMeanY<br>
8. tGravityAccMeanZ<br>
9. tBodyAccJerkMeanX<br>
10. tBodyAccJerkMeanY<br>
11. tBodyAccJerkMeanZ<br>
12. tBodyGyroMeanX<br>
13. tBodyGyroMeanY<br>
14. tBodyGyroMeanZ<br>
15. tBodyGyroJerkMeanX<br>
16. tBodyGyroJerkMeanY<br>
17. tBodyGyroJerkMeanZ<br>
18. tBodyAccMeanM<br>
19. tGravityAccMeanM<br>
20. tBodyAccJerkMeanM<br>
21. tBodyGyroMeanM<br>
22. tBodyGyroJerkMeanM<br>
23. fBodyAccMeanX<br>
24. fBodyAccMeanY<br>
25. fBodyAccMeanZ<br>
26. fBodyAccJerkMeanX<br>
27. fBodyAccJerkMeanY<br>
28. fBodyAccJerkMeanZ<br>
29. fBodyGyroMeanX<br>
30. fBodyGyroMeanY<br>
31. fBodyGyroMeanZ<br>
32. fBodyAccMeanM<br>
33. fBodyAccJerkMeanM<br>
34. fBodyGyroMeanM<br>
35. fBodyGyroJerkMeanM<br>
36. tBodyAccStdX<br>
37. tBodyAccStdY<br>
38. tBodyAccStdZ<br>
39. tGravityAccStdX<br>
40. tGravityAccStdY<br>
41. tGravityAccStdZ<br>
42. tBodyAccJerkStdX<br>
43. tBodyAccJerkStdY<br>
44. tBodyAccJerkStdZ<br>
45. tBodyGyroStdX<br>
46. tBodyGyroStdY<br>
47. tBodyGyroStdZ<br>
48. tBodyGyroJerkStdX<br>
49. tBodyGyroJerkStdY<br>
50. tBodyGyroJerkStdZ<br>
51. tBodyAccStdM<br>
52. tGravityAccStdM<br>
53. tBodyAccJerkStdM<br>
54. tBodyGyroStdM<br>
55. tBodyGyroJerkStdM<br>
56. fBodyAccStdX<br>
57. fBodyAccStdY<br>
58. fBodyAccStdZ<br>
59. fBodyAccJerkStdX<br>
60. fBodyAccJerkStdY<br>
61. fBodyAccJerkStdZ<br>
62. fBodyGyroStdX<br>
63. fBodyGyroStdY<br>
64. fBodyGyroStdZ<br>
65. fBodyAccStdM<br>
66. fBodyAccJerkStdM<br>
67. fBodyGyroStdM<br>
68. fBodyGyroJerkStdM<br>


## Performing analysis on tidydata and extracting the result
To prepare the final tidy data set with <U>the average of each variable for each activity and each subject</U>,<br><br>
1. Perform a group_by function on <B>tidydata</B> and store in <B>tidydataBySubAct</B><br>
2. Summarize the <B>tidydataBySubAct</B> with a mean function and store in <B>finaltidy</B><br>
3. Arrange <B>finaltidy</B> by subject and activity<br>
4. Extract <B>finaltidy</B> into tidy.txt<br><br>
