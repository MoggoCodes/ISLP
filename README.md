# Introduction to Statistical Learning <br /> Gareth James, Daniela Witten, Trevor Hastie, Robert Tibsirani, Jonathan Taylor

# Table of Contents
1. [Introduction](https://github.com/MoggoCodes/IntroToStatLearning)
2. Chapter 2
3. Chapter 3

# This Page
- (#Introduction)

# Introduction
*Statisticial Learning* refers to a vast set of tools for <ins>**understanding data**</ins>
- These tools can be classified as <ins>**supervised**</ins> or <ins>**unsupervised**</ins>
- *Supervised* Learning - Building a statistical model for predicting an <ins>**output**</ins> based on one or more <ins>**inputs**</ins>
- *Unsupervised* Learning - There are inputs but no supervising output
    - "Learn" about relationships and structure within the input data

# Data Sets
1. Wage Data
    - Wage data for a group of men from the Atlantic region of the United States
    - 9 predictors: Year, Age, Marital Status (5 level factor), Race (4 level factor), Education (5 level factor), Region, Job Class (2 level factor), Health (2 level factor), and Health Insurance (boolean)
    - (Quantitative) Outcome: wage

2. Smarket Data
    - Daily movements in the S&P500 between 2001 and 2005
    - 7 predictors: Year, Individual percentage return from the last 5 days, Volume of shares traded today
    - (Quantitative) Outcome: Today's percentage return
    - (Qualitative) Outcome: +/- return

3. Gene Expression Data
    - 6,830 gene expression measurements for each of 64 cancer cell lines
    - NO OUTCOME; desire to create clusters/groups

# History
Though the term *statistical learning* is fairly new, it is underlined by conceps developed long ago.
- <ins>**Linear Regression**</ins> - The method of *Least Squares* was developed in the 19th century.
    - First applied in astronomy.
    - Useful for predicting qualitative outcomes
- <ins>**Linear Discriminant Analysis**</ins> - Proposed in 1936
    - Can predict a qualitative outcome
- <ins>**Logistic Regression**</ins> - 1940s
    - Alternative approach to predict a qualitative outcome variable
- <ins>**Generalized Linear Model**</ins> - Termed in the early 1970s
    - Describes an entire class of statistical learning models
    - Includes both LDA and logistic regression as special cases

By the end of the 1970s many mature <ins>**Linear Methods**</ins> were available, but the development of *Nonlinear approaches* was restricted by computation constraints. By the 1980s, computing technology improved sufficiently to support the development of *Nonlinear* statistical learning techniques.
- <ins>**Classification and Regression Trees**</ins> - 1980s
- <ins>**Generalized Additive Models**</ins> - 1980s
- <ins>**Neural Networks**</ins> - 1980s
- <ins>**Support Vector Machines</ins> - 1990s

Now statistical learning has emerged as a new subfield in statistics focused on modeling and prediction. Progress has been marked by the increasing availability of powerful software. We are amidst a transformation from merely a set of techniques into a proper subdiscipline with substantial breadth and depth.