# Analysis of Student Exam Preparation Course and Student Score Predictor

<i>Exams are extremely common for students and even for adults. On average, students in the US public school system take around 112 mandatory standard tests between pre-K and high school graduation according to a new [Council of the Great City Schools study](https://www.cgcs.org/cms/lib/DC00001581/Centricity/Domain/4/Testing%20Report.pdf) (2015). This is in addition to teacher-written tests within the class.</i>
  
  <i>With exams being part of every day school life, determining who passes and who fails, which school a student will get into, and even the confidence level of a student, it's important to understand how best to improve a student's grasp on a topic as well as how to demonstrate that understanding. Oftentimes, this is through additional support. In this project, I will analyze the affects of a student exam preparation course, students' background and demographics to better understand what influences student exam scores. Using this information, I will create a classification model to predict when students will pass or fail an exam that is heavily influenced by the exam prep course so that students in need of additional support are made aware of the optional prep course, as well as it's positive influence on exam scores.</i>

## 1. Data
This project's dataset was obtained from [Royce Kimmons randomly generated Student Performance Dataset](http://roycekimmons.com/tools/generated_data/exams), originally found on [Kaggle](https://www.kaggle.com/spscientist/students-performance-in-exams). It is purely fictional and is used to demonstrate how a school or online program could analyze an exam preparation course and to offer additional support to students who are predicted to perform below passing.

The Kaggle dataset provided the first 1,000 rows of data, while Royce Kimmons' random generator provided the remaining 9,000 rows.

<i>Please note that due to each child and his/her life being very different from his/her peer's, scores predicted should never be used in place of giving the student a chance to perform their best on the exam. Instead, these predictions should be used to offer additional support should they be interested.</i>

## 2. Method
Two major prediction problems in supervised machine learning are classification and regression.
- **Classification:** The process of discovering an algorithm that divides the dataset into classes (discrete) based on each instances' features. In the realm of this particular project, this would be like determining whether a student will pass or fail an exam.
- **Regression:** The process of discovering the correlations between the independent and dependent variables in order to predict the output value (continuous). In this project, it would be like predicting a student's percentage score on an exam.

I chose to work with a classification problem to determine students who might score below passing on an exam. This would provide educators with a list of students who are at risk of failing an exam and who could use the additional support. As is the nature of teaching, teachers would be able to double check this list and add to it based on their experience while teaching the students.

## 3. Data Cleaning
[Data Cleaning Report](https://github.com/taflor/Student-Scores/blob/main/notebooks/1.1%20Data%20Wrangling.ipynb)

In a classification problem, the key features to used as input variables consisted of economic, personal, and course prep data. These features were originally categorical in nature with no missing values, allowing for a smooth transition to one-hot encoded columns. As input variable consisted purely of 0's and 1's, there was no need to standardize the features.

One important feature noting whether the parents participated in higher education was added. This new feature utilzied the parental education information to further breakdown and classify education in a way that only a human (rather than machine) would know is an important distinction (high school education vs higher level education).

## 4. EDA
[EDA Report](https://github.com/taflor/Student-Scores/blob/main/notebooks/1.2%20Exploratory%20Data%20Analysis.ipynb)

A significance test was run on each set of exam scores. Overall, it was found that the students who completed the exam preparation course scored higher on all tests, as well as the average, than students who did not complete the course. It was also found that the greatest difference between scores of students who took teh exam prep course and those who did not existed between the scores on the writing exam. Therefore, moving forward, the writing score is used as the predicted variable to ensure students who could benefit the most from the exam prep course are identified.

The boxplots below compare the scores students who did not take the exam prep course and the scores of students who did. As can be seen, the greatest impact of the exam prep course is on the writing exam.

![Boxplot of Exam Scores with Exam Prep Course](https://github.com/taflor/Student-Scores/blob/main/figures/EDA_exam_scores_boxplots.png)

After running a one-sided test for the null hypothesis that the writing mean scores are equal for students who complete the exam prep course and those who do not, a p-value of 5.8e-224 allowed us to reject the null hypothesis and accept the alternative. The alternative states that the writing mean score of students who complete the exam prep course is greater than the mean score of students who do not complete the exam.

![Distribution Writing Scores](https://github.com/taflor/Student-Scores/blob/main/figures/EDA_distribution_writing_scores.png)

## 5. Algorithms & Machine Learning
[Model Report](https://github.com/taflor/Student-Scores/blob/main/notebooks/1.4%20Modeling_Writing_Scoring_Table.ipynb)

Our original problem: Identify students who might fail the exam to provide optional additional support via an exam preparation course.

According to our problem, we are most interested in detecting students who are at risk of failing the exam. This means the recall -- calculation for how many actual "fails" our model captures by labeling it "fail" -- is the metric we are most interested in.

![Baseline Comparison of Models](https://github.com/taflor/Student-Scores/blob/main/figures/MODEL_baseline_comparison.png)

Examining Recall of a handful of machine learning models, we see that in this particular training set and cross validation split up the following models produced the best results:
- Linear Support Vector Classifier
- Logistic Regression

Using these models, we performed hyperparameter tuning to discover the best model for predicting students who will fail the exam. The model with the best recall score is the Linear Support Vector Classifier as can be seen in the confusion matrix and classification report below.

![Confusion Matrix](https://github.com/taflor/Student-Scores/blob/main/figures/MODEL_hyptertuned_linearsvc.png)

![Classification Report](https://github.com/taflor/Student-Scores/blob/main/figures/MODEL_classification_report_tunedSVC.png)

Key:
- 0 represents 'No Exam Prep'
- 1 represents 'Completed Exam Prep Course'

## 6. Predictions
[Predictions Report](https://github.com/taflor/Student-Scores/blob/main/notebooks/1.5%20Predictions.ipynb)

Analysis of the model's predictions:
- 73.5% of students who failed the exam were correctly identified.
- **92.7% of students identified as failing did indeed fail the exam or scored within 10 points of failing. This flagging of students therefore would provide them with the extra opportunity to improve their grade.**
- **80.8% of students who failed and have not taken the prep course were correctly flagged to suggest the exam prep course to. This provides a great base of students to suggest the exam prep course to.**
- 11.7% of students who failed the exam have taken the exam prep course AND were missed by the model's prediction.
- **14.7% of students who failed the exam have not taken the prep course AND were missed by the model's prediction. This is a cause for concern as these students failed the exam, did not take the exam prep course, and were missed by the prediction model. In future improvements, we would aim to decrease this percentage.**

## 7. Future Improvements
If this project were to be implemented at a school or for an online program, I would suggest the following improvements:
- Collect information on student's current test grades in each class, after school activities (e.g. sports, music, job), if they plan to go to college, and how many hours they study for each week on average (provide a range): This will provide more insight into the student and his/her life to possibly increase exam score prediction accuracy.
- Using these extra features, predict percentage scores: This will allow us to identify which students are nearing the 'fail' threshold.
- Aim to decrease the percentage of students who failed the exam, did not take the prep course, and were missed by the prediction model.

## 8. Credits
Thanks to Royce Kimmons for the experimental dataset and to Ram Hariharan for being an amazing Springboard mentor.

## Personal Reasoning Behind This Project

As a former educator, it was always interesting to see the differences in dedication to education at such a young age (6th grade -- 11 to 12 years old). Some students were eager to excel and would seek me out for help, while others would sit back and coast through class. It is up to the teachers to notice these trends, offer extra help, adjust the curriculum, and engage their students. When all of these approaches fail, one wonders why a student falls behind.

Having done some research, I came across <i>The Atlantic's</i> article, ['The 32-Million Word Gap'](https://www.theatlantic.com/technology/archive/2010/03/the-32-million-word-gap/36856/). A study was done by psychologists Betty Hart and Todd Risley in the mid-1980's to determine why some students excel while others do not, even after taking part in Head Start, their program for children of America's low-income workers. They collected data on words spoken by students from "three different socioeconomic levels: (1) welfare homes, (2) working-class homes, and (3) professionals' homes".

They found that "Children in professionals' homes were exposed to an average of more than fifteen hundred more spoken words per hour than children in welfare homes. Over one year, that amounted to a difference of nearly 8 million words, which, by age four, amounted to a total gap of 32 million words. They also found a substantial gap in tone and in the complexity of words being used. As they crunched the numbers, they discovered a direct correlation between the intensity of these early verbal experiences and later achievement. "We were astonished at the differences the data revealed," Hart and Risley wrote in their book Meaningful Differences. "The most impressive aspects [are] how different individual families and children are and how much and how important is children's cumulative experience before age 3.""

This study intrigued me and has resulted in this project, where the correlation between attributes within the file will be examined and economic, gender, and course prep data will be used to predict student performance on a test including math, reading, and writing sections.
