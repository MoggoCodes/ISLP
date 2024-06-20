# Introduction to Statistical Learning <br /> Gareth James, Daniela Witten, Trevor Hastie, Robert Tibsirani, Jonathan Taylor

# Table of Contents
1. [Introduction (This Page)](https://github.com/MoggoCodes/IntroToStatLearning)
2. Chapter 2
3. Chapter 3

# This Page
- [What is This Book?](#what-is-this-book)
- [Notation](#notation)
- [Introduction](#introduction)
- [Data Sets](#data-sets)
- [History](#history)

# What is This Book?
The purpose of *An Introduction to Statistical Learning* (ISL) is to facilitate the transition of statistical learning from an academic to a mainstream field. ISL is not intended to replace past texts, but rather make the field more accessible.

ISL is based on the following four premises
1. *Many statistical learning methods are relevant and useful in a wide range of academic and non-academic disciplines, beyond just the statistical sciences*
    - Similar to the prevalence of linear regression, some day many other contemporary statistical learning procedures will become as pervasive in a wide breadth of disciplines
    - Rather than detailing every possible approach, scope will be limited to presenting the most widely applicable methods
2. *Statistical learning should not be viewed as a series of black boxes*
    - Without understanding HOW a technique works, one cannot properly CHOOSE the best approach for their situation
    - Along with presenting how to perform a given technique; the model, intuition, assumptions, and trade-offs behind it will be carefully described
3. *While it is important to know what is happening under the hood, it is not necessary to rebuild the machine inside the box!*
    - Discussion of technical details related to fitting procedures and theoretical properties are minimized
4. *The reader is interested in applying statistical learning methods to real-world problems*
    - Hands-on approach with labs and excercises
    - Lab: walkthrough of a realistic application of some method(s)

# Notation
$n$ - number of observations in our sample  
$p$ - number of variables per observation

An observation is denoted by a column vector of magnitude $p$:

$$x = \begin{pmatrix} x_1 \\\ \vdots \\\ x_p \end{pmatrix}.$$

Here $x_j$ denotes the $j^{th}$ variable where $j = 1, \ldots, p$.

Note how a single observation $x$ is made up of $p$ scalar values of variables and denoted by grouping them in a column vector. 
Similarly a sample is made up of $n$ observation vectors and can be denoted by grouping them in a matrix.

$$\boldsymbol{X} = \begin{pmatrix} x_1 & \ldots & x_n \end{pmatrix}.$$  

Here $x_i$ denotes the $i^{th}$ observation vector where $i = 1, \ldots, n$.

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
Though the term *statistical learning* is fairly new, it is underlined by concepts developed long ago.
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
- <ins>**Support Vector Machines**</ins> - 1990s

Now statistical learning has emerged as a new subfield in statistics focused on modeling and prediction. Progress has been marked by the increasing availability of powerful software. We are amidst a transformation from merely a set of techniques into a proper subdiscipline with substantial breadth and depth.