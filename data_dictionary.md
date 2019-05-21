# Data Dictionary

* File Name: Assessment Response Log
  * Description: Each row represents a response to a question in a Guided Learning.  A student may have more then one record per question if they chose to respond more then once (like if they the answer wrong the first time or were testing themselves).  A student may also have more then one attempt per Guided Learning.
  * Field Descriptions
    * User_param_external_user_id: identifies the student. This can be used to match to the student’s grades in the Course Grades files, Assessment Page Views file, and the Click History file.
    * Created_at: Date/Time stamp for when a particular response was provided.
    * Assessment_attempt_id: identifies the assessment attempt. Assessment_attempt_id + question_id + created_at = unique response record.
    * Assessment_type: this contains the recognizable name for the assessment.
      * Mapping to Course Grades Assignment Names
        * HealthySelfChapterAssessment = Chapter 1 Guided Learning
          * BehaviorChangeChapterAssessment = Chapter 2 Guided Learning
          * KsuChronicDiseaseChapterAssessment = Chapter 3 Guided Learning
          * KsuCardioFitnessChapterAssessment = Chapter 4 Guided Learning
          * KsuMuscleHealthChapterAssessment = Chapter 5 Guided Learning
          * KsuNutritionChapterAssessment = Chapter 6 Guided Learning
          * PlantBasedNutritionChapterAssessment = Chapter 7 Guided Learning
          * KsuWeightManagementChapterAssessment = Chapter 8 Guided Learning
          * HealthyRelationshipsChapterAssessment = Chapter 9 Guided Learning
          * KsuSexualHealthChapterAssessment = Chapter 10 Guided Learning
          * MentalHealthChapterAssessment = Chapter 11 Guided Learning
          * KsuStressChapterAssessment = Chapter 12 Guided Learning
          * KsuAddictionChapterAssessment = Chapter 13 Guided Learning
          * KsuConclusionChapterAssessment = Chapter 14 Guided Learning
    * Correct_threshold: Score needed to get the question correct.
    * Question_id: identifies which question is being answered. This is unique to an assessment type only (meaning there will be multiple 1s, 2s, 3s, etc.) Since its based on the order of the questions in an assessment, the actual question associated to it can be different if any questions are inserted or removed. This did not happen during the last semester, so this should be ok to use to identify a question in an assessment.
    * Question_tag: not really used in this data set. Going forward this will be used to uniquely identify a question so that when questions are added or removed, a specific question can still be identified.
    * Question_type: defines what type of question was asked.
      * Options
        * multipleChoice = 1 correct answer
        * multipleSelect = 1 to many answers must be chosen for correct
        * matching = must match all things correctly for correct
    * score: this represents if the user got the question correct.  If the score equals the correct_threshold value, the user got the question correct. If the score is less then the correct_threshold value, the user got the question wrong.
    * Subcategory: each question is assigned a subcategory based on which chapter topic it represents.
    * Taxonomy: each question is assigned a difficulty level (1-6) based on bloom’s taxonomy. This field holds the value for a particular question.
    * Text: this is the actual text from the answer choice(s) that the student selected
    * Value: “value” is used in the JSON for a question to identify the response choices position in the order of answer options.  For multipleChoice questions, there will be one number in this field and it will represent where in the order of response choices the response the student selected was. For multipleSelect questions, this will be an array (since there is usually more the none response that needs to be selected. 0 = first response choice on list.
* File Name: Assessment Page Views
  * Description: Each row represents a page view in a specific guided learning.  Each visit to a page is logged separately, so a student may have multiple records for the same page of an assessment. This data can be used to determine how much time a student spends in a guided learning.
  * Fields: 
    * assessment_attempt_id: identifies the assessment attempt. This will match the assessment_attempt_id field in the Assessment Response Log.
    * assessment_attempt_type: The guided learning assessment the student was completing.  See the section called File Name: Assessment Response Log for more complete information on assessment_attempt_type.
    * canvas_assignment_id: The assignment id of the assessment in a particular course.
    * canvas_course_id: The course id for the student. 
    * canvas_section_id: The section id for the student.
    * created_at: The date the record was created.
    * duration: This is the amount of time spent on the page for a specific visit. This is in milliseconds.
    * id: this is the unique identifier for each row in the file.
    * page_id: this identifies a specific page in the assessment. This is unique to an assessment but not unique across all assessments (i.e. each assessment has a page 1, 2, 3, etc.)
    * raw_lti_param_ext_outcome_submission_submitted_at_accepted: this confirms that the students time was logged. 
    * user_param_external_user_id: this is the id that identifies a particular student. This can be used to match the students in the other files.
* File Name: Course Grades (Detail View) Fall 2018
  * Description: This file contains grades for all of the assignments for each student.
* File Name: Course Grades (Final Grade Only View)
  * Description: This file contains the final grade information for all of the Fall 2018 Well1000 students.
* File Name: Click History Fall 2018
  * Description: This file contains all of the student click history that was not within a Guided Learning Asssessment for the KSU Well1000 courses from Fall 2018. 
  * Fields:
    * Context_id: this identifies which course the click was in. this matches canvas_course_id from other files.
    * Controller: this identifies the type of page being accessed.
    * Created_at: the date and time the click happened
    * http_method: helps determine if the click was a page view or if the student submitted something on a page.
    * interaction: an estimated time spent. This field isn’t very accurate, though.
    * render_time: time it took the page to render
    * session_id: browser session id. 
    * url: actual url the student clicked.
    * user_agent: browswer/computer information about the device used to access the page.
    * user_id: identifies the user who clicked. This can be used to match the students in the other files.
