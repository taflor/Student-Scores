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


## 5. Algorithms & Machine Learning
[Model Report](https://github.com/taflor/Student-Scores/blob/main/notebooks/1.4%20Modeling_Writing_Scoring_Table.ipynb)

## 6. Predictions

## 7. Future Improvements
If this project were to be implemented at a school or for an online program, I would suggest the following improvements:
- Collect information on student's current test grades in each class, after school activities (e.g. sports, music, job), if they plan to go to college, and how many hours they study for each week on average (provide a range): This will provide more insight into the student and his/her life to possibly increase exam score prediction accuracy.
- Using these extra features, predict percentage scores: This will allow us to identify which students are nearing the 'fail' threshold.

## 8. Credits
Thanks to Royce Kimmons for the experimental dataset and to Ram Hariharan for being an amazing Springboard mentor.

## Personal Reasoning Behind This Project

As a former educator, it was always interesting to see the differences in dedication to education at such a young age (6th grade -- 11 to 12 years old). Some students were eager to excel and would seek me out for help, while others would sit back and coast through class. It is up to the teachers to notice these trends, offer extra help, adjust the curriculum, and engage their students. When all of these approaches fail, one wonders why a student falls behind.

Having done some research, I came across <i>The Atlantic's</i> article, ['The 32-Million Word Gap'](https://www.theatlantic.com/technology/archive/2010/03/the-32-million-word-gap/36856/). A study was done by psychologists Betty Hart and Todd Risley in the mid-1980's to determine why some students excel while others do not, even after taking part in Head Start, their program for children of America's low-income workers. They collected data on words spoken by students from "three different socioeconomic levels: (1) welfare homes, (2) working-class homes, and (3) professionals' homes".

They found that "Children in professionals' homes were exposed to an average of more than fifteen hundred more spoken words per hour than children in welfare homes. Over one year, that amounted to a difference of nearly 8 million words, which, by age four, amounted to a total gap of 32 million words. They also found a substantial gap in tone and in the complexity of words being used. As they crunched the numbers, they discovered a direct correlation between the intensity of these early verbal experiences and later achievement. "We were astonished at the differences the data revealed," Hart and Risley wrote in their book Meaningful Differences. "The most impressive aspects [are] how different individual families and children are and how much and how important is children's cumulative experience before age 3.""

This study intrigued me and has resulted in this project, where the correlation between attributes within the file will be examined and economic, gender, and course prep data will be used to predict student performance on a test including math, reading, and writing sections.


**Goals**<br>
- Examine correlation between different attributes.
- Using economic, personal, and course prep data, predict student performance on a test including math, reading, and writing.
