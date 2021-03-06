[![Repo Checks](https://github.com/Sta663-Sp22/hw04_team03/workflows/Repo%20Checks/badge.svg)](https://github.com/Sta663-Sp22/hw04_team03/actions?query=workflow:%22Repo%20Checks%22)


# Rasch Models Three Ways

*Team Members*: Li, Tianhao, Lu, Lexin, Wang, Jingjing, Yu, Camilla


## Background

A basic model for exploring logistic item response data is the Rasch
model where the goal is to model a subject’s performance on a task based
on a simple combination of their “ability” and the “difficulty” of the
question. Imagine we give an exam to
![J](https://latex.codecogs.com/svg.latex?J "J") subjects who then all
answer the same ![K](https://latex.codecogs.com/svg.latex?K "K")
questions, which are then marked correct
(![y\_{jk}=1](https://latex.codecogs.com/svg.latex?y_%7Bjk%7D%3D1 "y_{jk}=1"))
or
incorrect(![y\_{jk}=0](https://latex.codecogs.com/svg.latex?y_%7Bjk%7D%3D0 "y_{jk}=0")).
These data can then be modeled using,

![
\\text{Pr}(y\_{jk}=1) = \\text{logit}^{-1}(\\alpha_j - \\beta_k)
](https://latex.codecogs.com/svg.latex?%0A%5Ctext%7BPr%7D%28y_%7Bjk%7D%3D1%29%20%3D%20%5Ctext%7Blogit%7D%5E%7B-1%7D%28%5Calpha_j%20-%20%5Cbeta_k%29%0A "
\text{Pr}(y_{jk}=1) = \text{logit}^{-1}(\alpha_j - \beta_k)
")

where
![\\alpha_j](https://latex.codecogs.com/svg.latex?%5Calpha_j "\alpha_j")
is the *ability* of subject
![j](https://latex.codecogs.com/svg.latex?j "j") and
![\\beta_k](https://latex.codecogs.com/svg.latex?%5Cbeta_k "\beta_k") is
the *difficulty* of question
![k](https://latex.codecogs.com/svg.latex?k "k"). For our purposes we
will assume that all subjects completed all questions so that there is a
total of
![J \\times K](https://latex.codecogs.com/svg.latex?J%20%5Ctimes%20K "J \times K")
rows in our data. For a detailed review of Rasch models and some
considerations around identifiability see Section 14.3 Item-response and
ideal-point models from Data Analysis Using Regression and
Multilevel/Hierarchical Models (2006) by Gelman & Hill. This section has
been posted on Sakai and is available via the following
[link](https://sakai.duke.edu/access/content/group/f7f5a63a-12dd-45a3-9193-6cfb1106465b/DAURMHM%20-%20IRT.pdf).

We have constructed a simulated data set of 200 students taking an exam
with 20 questions and the results are presented in `data/exam.csv`.
These data were simulated using the basic Rasch model described above,
so each student has a specific ability score and each question a
difficulty. For the sake of identifiability we will always assume that
the distributions of abilities will have a mean of 0 while difficulties
do not. Keep this in mind when constructing your model(s) and
interpreting your results.

## Task 1 - Data Cleaning

Starting from the given data, tidy it and construct any columns that are
necessary for the subsequent models in Tasks 2 - 5. All code for tidying
/ cleaning the data should occur in this section exclusively.

Once the tidying and cleaning is finished, construct a test / train
split of these data.

## Task 2 - Basic EDA

Using these data (training split) answer the following questions to the
best of your ability using summary statistics, include the code used to
answer each question and provide a brief (1-2 sentence) justification
for your answer.

-   What is the average *difficulty* of the questions in these data?
    (Here and for all subsequent questions on difficulty we want to know
    the probability of getting an average question correct)
-   What was the hardest question based on these data?
-   Which student had the highest ability based on these data?

## Task 3 - Logistic Regression

Using these data (training split) fit a standard logistic regression
model using student id and question number as features. You may use
either sklearn or statsmodels to fit this model. Once the model has been
fit answer the following questions based on your model results:

-   What is the average *difficulty* of the questions according to this
    model?
-   What was the hardest question according to this model?
-   Which student had the highest ability according to this model?

As before include the code used to answer each question and provide a
brief (1-2 sentence) justification for your answer. Hint - be careful
about the sign of your coefficients relative to the Rasch model, also
remember the assumption above that abilities should have mean 0 for the
purposes of interpreting the model results.

## Task 4 - Mixed Effects

Repeat the previous task but now fit a mixed effects model for these
data using statsmodels. Make sure to justify your choice of what is
treated as a random effect and a fixed effect.

Once the model has been fit answer the following questions based on your
model results:

-   What is the average *difficulty* of the questions according to this
    model?
-   What was the hardest question according to this model?
-   Which student had the highest ability according to this model?

As before include the code used to answer each question and provide a
brief (1-2 sentence) justification for your answer. Previous hints are
also relevant for this model.

Note - when writing this question I had assumed that statsmodels fully
supported fitting GLM mixed effects models which is not the case,
however `BinomialBayesMixedGLM` is available and sufficient for fitting
this model. I recommend using the `fit_vb()` method to efficiently
obtain an approximate fit. You can completely ignore the Bayesian aspect
of this model and simply use the posterior means of all model parameters
/ coefficients.

## Task 5 - Bayesian Model

Finally, again fit these data (training split) but this time using a
Bayesian implementation of the Rasch model using PyMC3. As stated above
you may assume that ability has mean 0 and an unknown variance. For all
model parameters pick any reasonable weakly or non-informative prior.
Include at least some basic diagnostics showing that the model
converged.

Once the model has been fit answer the following questions based on your
model results:

-   What is the average *difficulty* of the questions according to this
    model?
-   What was the hardest question according to this model?
-   Which student had the highest ability according to this model?

As before include the code used to answer each question and provide a
brief (1-2 sentence) justification for your answer.

## Task 6 - Comparison

Summarize your findings from the previous 4 tasks and discuss the
similarities and differences you found between the models and EDA in
terms of the three questions. Include any visualization and or tables to
support your conclusions.

## Task 7 - Evaluation

Compare the performance of the 3 models using out-of-sample data (test
split) by constructing and plotting ROC curves that also include the AUC
of each model. For the Bayesian model from Task 5 this should be
constructed using the posterior median or mean of the predicted
probabilities.
