I need to add all of the visualizations to this thing after I have saved them. Then I need to add pseudo code that
shows some of the calculatations and actual results from hypothesis tests, linear regression, and descriptive statistics.
All of that should take about 1hr. Then I'll be done. I can do that tomorrow in the car.

# Introduction:

### Section 1: Effects of Guided Learning Duration and Attempts

This section analyzes the correlation between average duration and average attempts seperately on final grades, quiz grades, and midterm grades.

### Section 2: Effects of Class Structure

This section groups students by class structure (face to face with quiz, face to face with midterm, and online). The
students are also bucketed into letter grades that correspond to the numbers 0,1,2,3,4.

### Section 3: Looking at the "Dip"

This section will plot grades of students over the course of the semester. The grades of interest are project grades
and guided learning grades. Quiz grades will also be looked at for the face to face quiz group.





****
## Section 1: Effects of Guided Learning Duration and Attempts

This section will look at the correlation between average duration and attempts on guided learning and grade outcomes: final grades, quiz grades, and midterms.

I will use simple linear regressions to test for correlations and hypothesis tests to evaluate the difference between groups (Those above versus below the average for duration and attempts).

### Results:

The linear regressions and hypothesis tests performed are as follows:
 * Unposted Final score and Average Assessment Attempts
 * Unposted Final score and Average Assessment Duration
 * Difference of means for Students with above versus below average assessment durations
 * Average Quiz Grade by Average Assessment Duration
 * Average Quiz Grade by Average Assessment Attempts
 * Average Midterm Grade by Average Assessment Duration
 * Average Midterm Grade by Average Assessment Attempts
 * Guided Learning Grade by Average Assessment Duration
 * Guided Learning Grade by Average Assessment Attempts

None of these yielded any correlation or difference of means. The conclusion is that none of these factors were
a direct contributor or indicator of student success in the course.

****
## Section 2: Effects of Class Structure

This section will divide students based on their final scores in the class. They will be bucketed into 5 groups: 105-90, 90 - 80, 80 - 70, 70 - 60, 60-0. The last group is larger, but it charcterizes all the students that got failing grades. It is a grouping essentially of A,B,C,D, and F letter grades.

Then students will be divided based on the class structure they took: face to face with quizzes (which includes the hybrid group), face to face with a midterm, and online.

Using these grouping, I will calculate descriptive statistics and perform hypothesis test to see if their are statisitaclly significant difference between the groups. This will be a basis for furhter analysis with machine learning.

### Results:

The distributions and means appear to be the same for the different class structures. All of the grade distributions had a mean of about 83-85 which is not varied enough to be significant. None of the standard deviations or other descriptive statistics stood out either. None of the hypothesis tests were able to reject the null hypothesis for the difference of means between the grade distributions except for Midterm and Online class structures having the same mean final grade was rejected at alpha = 0.077. This was after bucketing to assign students to 6 categories of letter grades. 

It makes sense that the purely online class would have a different average final grade in the class compared to the face to face classes (quiz and midterm). It does stand out a little bit that Quiz and Online class structures having the same mean final grade had a p-value of 0.77308, but Quiz and Midterm grades only had a p-value of 0.1065 after bucketing. 

So although Midterm and Online have statistically different mean final grades, and their is a case for Midterm and Quiz having different means, Quiz and Online are most likely not different.

This is consistent with the descriptive statistics that were calculated were Quiz and Online students had a mean final score of 85 while Midterm students had a mean final score of 83.

This is statistically different, but maybe not practically significant. It is worth recognizing since they were also different after bucketing to account for small percentage gaps like above.

****
## Section 3: Looking at the "Dip"

This section will plot grades of students over the course of the semester. 
The grades of interest are project grades and guided learning grades. 
Quiz grades will also be looked at for the face to face quiz and online groups.
Students will be broken up by their class structure for some of the plots, then they will also be bucketed by their
final grade in the class.

Overall Plots:
 * Plot 1: Overall trend for Project Grades
 * Plot 2: Overall trend for Quiz Grades
 * Plot 3: Overall trend for Guided Learning Grades

Class Structure Plots:
 * Plot 4: Trend for project grades by Class structure
 * Plot 5: Trend for Guided Learning Grades by Class Structure 
 * Plot 6: Trend for Quiz grades by Class Structure

Final Grade Plots:
 * Plot 7: Trend for project grades by grade_bucket 
 * Plot 8: Trend for guided learning grades by grade_bucket 
 * Plot 9: Trend for quiz grades by grade_bucket
 
### Results:

The graphs in this section explored the trend in grades for different class structures assignments, and final grades.
Nothing unexpected arose from these graphs. There was usually a dip in the middle of the semester and a rise at the end with students with lower final grades having lower average grades for the whole span of the semester.

This idea could possibly be used for identify at risk students early on and will be explored more in the capstone project.





***
# Moving Forward:

This analysis did not answer many questions, but it did set the stage for machine learning. Many new dataframes that combine information were compiled here that could be useful for the capstone project. It also ruled out some factors such as duration and attempts for the most part.

It acknowledged that the course structures while statistically different, may or may not be different enough to be practical. It is more likely that class/section time has a larger effect on student success which was not explored in this report. While this report looked at class structure, it did not delve into courses/sections and tie that back to 
specific instructors either. That could be something worth looking into.

This report also only looked at assignments, quizzes, and projects in order but not in the context of the actual date they were taken. What part of the semester were they given in?, what was the actual unit on? etc.

The goal of this project is to identify factors that differentiate at-risk students from successful students. That will be the focus of the capstone project which will expand upon the work done in the preliminary analysis.