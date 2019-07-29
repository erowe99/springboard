# Perceivant Student Engagement Data Report
***
***

### Overview

Proposal				2

Data Overview			3

Machine Learning Analysis		4

Results and Recommendations	6

Note: This report is a simplified version of the extended report that cuts down about 20 pages of information and detailed steps into this finalized report. 
More information can be found by reading the “Extended Report” or by looking through the python notebooks in the GitHub repository for this project.

The python notebooks will have the code and commentary for an Exploratory Data Analysis, Inferential Statistics Report, Machine Learning Cluster, and Data Cleaning. This information can also be found in the Extended Report.


# Perceivant Student Engagement Data
***

The client for my capstone project is Perceivant. Perceivant provides online courseware to universities and focuses on active learning. Active learning is tailored to the individual student and is meant to involve students in the learning process. The goal is that students can apply what they learn in these courses.

Perceivant wants to identify which factors of student engagement determine success in a course. They also want to see if there are other factors that predict failure. Perceivant will use the results to brainstorm potential ideas to boost student engagement based on the success factors and create risk assessments based on the predictive failure factors. These factors could be used to create new products and identify at risk students. This data could also explain add/drop rates for the course and put them in context.

The data for this project will be provided by Perceivant and is gathered through its online courseware. The data will focus on one course from one university. This is about 2000 entries containing various factors such as de-identified student grades, engagement, click history, and assessment responses.

For failing students, I want to look at how many "gave up" in the class which could be determined by their log-in times to the course. By checking how many students got below a 70 and also have not been active since about August and October. It could also be useful to look at specific course/sections/teachers/class times as factors that could have contributed to student success.

The end goal would be to predict and identify successful students and students at risk of failing before the semester ends ideally within the first four weeks of class. I will also add more context to the add/drop rates for the course in order to make them representative of the course.



# Data Overview
***

The dataset for this project is a collection of five files: Assessment Response Log, Assessment Page Views, Course Grades, Course Grades Final, and Click History. These files contain data for over 3000 students in Perceivant’s course. The data was pulled from Perceivants database and given to me in excel and csv formats. These names are how they are referenced in the data_dictionary, but these differ from the names of the csv’s in the springboard_data folder.

Course Grades is the file “grade_export_csv_08_Jan_2019_2220190108-19791-1e3ruy6 (1).csv” 
Course Grades Final is “KSU Student Final Grades 2018 Anonymous.csv” 
Assessment Page Views is “KSU Assessment Page Views Fall 2018 Clean.csv”

The problem is looking at factors of student engagement that predict success or failure in the course. This will mainly involve the Course Grades sheet and the Assessment Page Views csv. Course Grades is described above. Assessment Page views has a shape of  (6012777, 13). There were some missing values, but the relevant columns (page_id, duration, canvas_assignment_id, assessment_attempt_id, user_param_external_user_id, and assessment_type) had no missing values. I will only consider it a problem if there is more than 10% of a columns values are missing. 

The duration column for Assessment Page Views was one column of interest. It contains the time in milliseconds that a student spent on a page of an assessment. This column was checked for outliers using the interquartile range and the outliers were removed. The result is called “KSU Assessment Page Views Fall 2018 Clean.csv”. 

This data has been grouped in various ways into dataframes that make it easier to work with. One example is the Assessment Page Views after cleaning grouped by assessment_type and the average duration for each type was found. This was not saved as a csv, so examples like this will not be mentioned here. This information can be found in the section of the report where that calculation was made. 


# Machine Learning Analysis
***

### KNN:

K-Nearest Neighbors is a very basic, but practical classifying algorithm. Given a set of features, it will attempt to predict what class a data entry belongs to. In this case, the features are total duration, total attempts, class structure, or first project grade in the first four weeks of class. The target classifications were grade_bucket which was an attempt to place students into 4 buckets based off of percentiles, and pass/fail which as a binary classification of a 1 or a 0 for whether a student would pass or fail the class. 


Best Accuracy: 0.9683098591549296

Confusion Matrix:

[2715,   34]

[ 192,   39]

For both total attempts and total duration spent in guided learning, the accuracy of the model never rose above 40% using grade_bucket as the predictor. When the predictor was changed to pass/fail which is a binary variable, the accuracy was much higher, but the recall was not good. The accuracy was high, because the model predicted, almost randomly, that students would pass the class, and most students did pass the class (achieve a 60% or above).

The at-risk students in these models would be the negatives. False negatives are not a huge problem, since it is better to be safe and intervene with a student who might pass than ignore a student who might fail. The important sections to look at in the confusion matrices are the False Positives. These are the students who the model thinks will pass, but will really fail. Comparing the true negatives to false positives, the model does a terrible job of actually identifying students at risk even if the “accuracy” is high. These models will not be practically useful to Perceivant


### Logistic Regression:

Logistic Regression will also be useful as a classifier for a binary target variable pass. It will also be combined with GridsearchCV. GridsearchCV is a way of optimizing hyperparameters such as slack variables. That could mean, how far can a point stray from the cluster and still be considered part of the cluster. Optimizing parameters like this could provide more accuracy and a more useful model. 

Tuned Logistic Regression Parameters: {'C': 1e-05}

Best score is 0.9250559284116331

Confusion matrix:

[2749,    0]

[ 231,    0]

This model did not perform as well as the k-means classifier in terms of accuracy or recall. This model has the similar problem of having a terrible ratio of false positives to true negatives. In fact, this model just said that everyone passed the class which is by coincidence, a 92.5% accuracy score. This model will not be useful to Perceivant. 

It is also likely that we can rule out total time spent and total attempts in guided learning in the first four weeks as predictors of success/failure in the course, but we will use Random Forest to support this further.

### Random Forest:
 
This section will use the Random Forest Classifier and Regressor to create a model and identify important features. It will create a decision tree diagram with weights that will help classify data points and identify which features held the most weight. This will be the last attempt to create a model or determine if total duration, total attempts, first project grades, and class structure are useful features to examine.

Mean Absolute Error: 0.06 degrees

Score: 0.9405405405405406

Features:

Variable: duration_4           Importance: 0.15

Variable: attempts_4          Importance: 0.15

Variable: duration_2           Importance: 0.13

Variable: duration_1           Importance: 0.12

Variable: attempts_1           Importance: 0.11

Variable: attempts_2           Importance: 0.11

Variable: duration_3            Importance: 0.09

Variable: attempts_3           Importance: 0.09

Variable: online                   Importance: 0.02

Variable: quiz                      Importance: 0.02

Variable: midterm                Importance: 0.01

While the accuracy and mean absolute error make this model seem very precise, it does not fulfill Perceivants main goal of correctly identifying at risk students. The test data for this model had 33 students that were at-risk. The model signaled that there were only 4 and only 2 of those 4 were actually at-risk students, the other two would have passed. This means that the model only identified 2/33 correctly which is a recall of about 6%. The best model so far was in the KNN section with a score of 17%. The caveat being that it also had several false negatives, so non-at-risk students were also signaled.

Several other attempts were made using the Random Forest Regressor along with varying the number of factors, such as just using the top five from above, but none performed any better. 

### Results and Recommendations
***

The goal of this project was to identify factors that could predict success or failure. This section was trying to identify at-risk students in the first four weeks of the semester before it is too late to intervene.

Along with the models created above, I also created KNN models that were fit to both total time spent and total attempts, I created versions that included the class structure (quiz, midterm, and online), and I also created a model based off of the first project grade. None of these models did significantly better in any way than the models in Section 2, 3, or 4.

It seems every model had good accuracy, but had terrible recall. The model that did the best with True Negatives and False positives was the project grades model, but it also misidentified about half the students as False Negatives. If I blindly say that half the class will fail, and the half I pick does in fact contain most of the students who will fail, it is still not a great model, since the work it would take to actually identify those students who will fail (about 150 in this example) from the misidentified students (about 1500) would take too many resources. This model effectively does eliminate about 1000 students from the “might fail” group, but there are still too many students to sift through for this to be a practically useful model. 

It analogous to just using a larger net, so it makes sense that you would catch more of your target fish, but it is too much work and near impossible to identify them further from the rest of the batch.

After using Random Forest as the last effort, it is likely that using the features I chose, there is not a way to classify students so early in the semester. The other option that was unexplored was the relationships in the Assessment Responses and Click History datasets. These might be able to improve the models above or create new ones, but I did not have enough time in the scope of this project to explore every possible avenue.

Other options to consider would be targeting specific sections, courses, teachers, class times etc. to see if those have a distinct effect. Putting more weight on students that are in 8am might improve the model. 

For now, I would use the above sections as a platform for continued experimentation. The most definitive statement I can make is that the combination of total duration, total attempts, class structure, and first project grade in the first four weeks is not sufficient for a model to predict whether that student will pass or fail. Looking through the other datasets or computing new fields might help.

The class structures also did not have practically significant differences in their mean final grades, which was concluded by a hypothesis test in the inferential statistics sections. Average duration and average attempts also had little to no effect on the students' grades. Even last login time was a weak predictor for students that scored below a 70% in the class which was explored in the EDA section of ipython notebooks.

For Perceivant, the information in this report could also be used for marketing purposes or for a blog. This report cannot be used to answer the problem of predicting whether a student will pass or fail the class early on in the semester.




