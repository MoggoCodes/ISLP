# Introduction to Statistical Learning <br /> Gareth James, Daniela Witten, Trevor Hastie, Robert Tibsirani, Jonathan Taylor

## Table of Contents
1. [Introduction *(This Page)*](https://github.com/MoggoCodes/IntroToStatLearning)
2. Chapter 2
3. Chapter 3

## This Page
- [What is This Book?](#what-is-this-book)
- [Notation](#notation)
- [Introduction](#introduction)
- [Data Sets](#data-sets)
- [History](#history)

## What is This Book?
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

## Notation
$n$ - Number of observations in our sample  
$p$ - Number of predictors measured per observation

$x$ - Predictive quantity of interest
$y$ - Outcome measurement

|    Variable     |    Denotes     |    Collection    |     Tensor      | Shape |
| :-------------: | :------------: | :--------------: | :-------------: | :---: |
| $\boldsymbol X$ |     Sample     | $n$ observations | Rank-2 (matrix) | (n,p) |
|       $y$       | Outcome Sample | $n$ measurements | Rank-1 (vector) |  (n)  |
|      $x_i$      |  Observation   | $p$ measurements | Rank-1 (vector) |  (p)  |
| $y_j$/$x_{ij}$  |  Measurement   |       self       | Rank-0 (scalar) | point |

#### Random Variable
A *Random Variable* (RV) is a quantity that is unknown until its value is measured. The objective of *Statistical Learning* is to find predict the measurement of one RV based of the measurement of others.
- **Supervised** - Predict outcome $Y$ based on corresponding measurements of $X_1, \ldots, X_p$
- **Unsupervised** - Predict $X_1, \ldots, X_3$ based on corresponding measurements of $X_4, \ldots, X_p$

A RV is denoted with $X$ if it is a predictor and $Y$ if it is the outcome. A random variable can be a quantitative or qualitative. Furthermore, the set of ALL possible values can be ANY subset of $\mathbb R$. The only constraint is that if it is a qualitative variable (i.e. color) then it is defined as a factor (1 = red, 2 = blue, etc).

#### Measurement
In this context, a *measurement* refers to a single observation of a random variable. 

Suppose that a person's weight is a random variable of interest. It is observed and a measurement is taken denoted with a rank-0 tensor $x$.

#### Observation
An *observation* refers to the collection of the values of its $p$ measurements. As defined above, each *measurement* is a rank-0 tensor. It follows that a rank-1 tensor is needed to group $p$ rank-0 tensors. Furthermore, since there are multiple measurements, they can be distinguished between by changing their denotion from $x$ to $x_j$.

Suppose that we are interested in predicting a person's height based of their age, sex, and weight. We can define random variable $Y$ to be height, $X_1$ to be age, $X_2$ to be sex, and $X_3$ to be weight. Next we get a participant and take an *observation*: a measurement of each of these variables. We denote our measurements as $y$, $x_1$, $x_2$, and $x_3$ depending on what variable was measured. We denote this observation with a rank-1 tensor $x = \begin{pmatrix} x_1 & x_2 & x_3 \end{pmatrix}$.

In a situation with $p$ predictive random variables of interest denoted $X_1, \ldots, X_p$ a single observation can be made by taking a measurement of each of the RVs, each denoted with a rank-0 tensor $x_j$. The entire observation can be denoted by a rank-1 tensor $$x = \begin{pmatrix} x_1 \\ \vdots \\ x_p \end{pmatrix}.$$

#### Sample
A *sample* refers to the collection of its $n$ observations. As defined above, each *measurement* is a rank-1 tensor. It follows that a rank-2 tensor is needed to group $n$ rank-1 tensors. Furthermore, since there are multiple observations, they can be distinguished between by changing their denotion from what is shown above to $$x_i = \begin{pmatrix} x_{i1} \\ \vdots \\ x_{ip} \end{pmatrix}.$$

Take the same situation detailed above. A single observation is not going to help very much to predict the height of a random person given their age, sex, and weight. However with a *sample* of 3000 people, it is likely that trends and correlations in the data that will be useful to make predictions will show themselves.


 Each value is denoted by a rank-0 tensor (scalar). Each of these tensors is grouped together in a rank-1 tensor (column vector) of size $p$ to denote a single observation as such. Suppose that $x_i$ is the $i^{th}$ observation comprised of $p$ variables. Each value is denoted by $x_{ij}$ and can be grouped together in a sample as such

$$x_i = \begin{pmatrix} x_{i1} \\\ \vdots \\\ x_{ip} \end{pmatrix}.$$

A *sample* refers to the collection of the values of its $n$ observations. 


Here $x_j$ denotes the $j^{th}$ variable where $j = 1, \ldots, p$.

Note how a single observation $x$ is made up of $p$ scalar values of variables and denoted by grouping them in a column vector. 
Similarly a sample is made up of $n$ observation vectors and can be denoted by grouping them in a matrix.

$$\boldsymbol{X} = \begin{pmatrix} x_1 & \ldots & x_n \end{pmatrix}.$$  

Here $x_i$ denotes the $i^{th}$ observation vector where $i = 1, \ldots, n$.

## Introduction
*Statisticial Learning* refers to a vast set of tools for **understanding data**
- These tools can be classified as **supervised** or **unsupervised**
- *Supervised* Learning - Building a statistical model for predicting an **output** based on one or more **inputs**
- *Unsupervised* Learning - There are inputs but no supervising output
    - "Learn" about relationships and structure within the input data

## Data Sets
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
- **Linear Regression** - The method of *Least Squares* was developed in the 19th century.
    - First applied in astronomy.
    - Useful for predicting qualitative outcomes
- **Linear Discriminant Analysis** - Proposed in 1936
    - Can predict a qualitative outcome
- **Logistic Regression** - 1940s
    - Alternative approach to predict a qualitative outcome variable
- **Generalized Linear Model** - Termed in the early 1970s
    - Describes an entire class of statistical learning models
    - Includes both LDA and logistic regression as special cases

By the end of the 1970s many mature **Linear Methods** were available, but the development of *Nonlinear approaches* was restricted by computation constraints. By the 1980s, computing technology improved sufficiently to support the development of *Nonlinear* statistical learning techniques.
- **Classification and Regression Trees** - 1980s
- **Generalized Additive Models** - 1980s
- **Neural Networks** - 1980s
- **Support Vector Machines** - 1990s

Now statistical learning has emerged as a new subfield in statistics focused on modeling and prediction. Progress has been marked by the increasing availability of powerful software. We are amidst a transformation from merely a set of techniques into a proper subdiscipline with substantial breadth and depth.