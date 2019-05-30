# Capstone Project - Data Wrangling

The dataset for this project is a collection of five files: Assessment Response Log, Assessment Page Views, Course Grades, Course Grades Final, and Click History. These files contain data for over 3000 students in Perceivant’s course. The data was pulled from Perceivants database and given to me in excel and csv formats. 

The first problem Perceivant wants to look at is the drop rates for the course. There is a sizeable chunk of students that miss the drop date and then give up on the course. This affects the failure rate for Perceivant even though these were students that should not have been counted since they had effectively “dropped” the course. 

This problem will use the Course Grades excel document. The step to clean this file included checking for missing values, adding a new column that recorded the last time they submitted work, and removing duplicate student id’s that were a result of a student switching course sections, not failing. This new sheet is called “student_login_times_clean.” 

Then, I created a new sheet, “Dropped”, that contains all the students who have not been active since August 19, 2018. Another sheet named “active students.” The latter contains all the students who legitimately failed the course and were actively participating for most of the semester. 

The next problem on the table is whether or not more assignment attempts or page duration is correlated with higher grades in the course. This will mainly involve the Course Grades sheet and the Assessment Page Views csv. Course Grades is described above. Assessment Page views has a shape of  (6012777, 13). There were some missing values, but the relevant columns (page_id, duration, canvas_assignment_id, assessment_attempt_id, and user_param_external_user_id) had no missing values. I will only consider it a problem if there is more than 20% of a columns values missing. 

The duration column for Assessment Page Views was one column of interest. It contains the time in milliseconds that a student spent on a page of an assessment. This column was checked for outliers using the interquartile range and the outliers were removed. The result is called Assessment Page Views Clean.

