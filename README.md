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
Statistical learning methods are derived from linear and matrix algebra. As a result, it is common to deal with scalars, vectors, and matrices. This is why it is important to have very clear notation rules as to follow the math and understand what various objects represent.

### Scalars $(a \in \mathbb R)$
Scalar objects will be notated by *normal font* letters. This means non-bold.

#### Random Variables
An object that represent a random variable will be notated by an *upper case normal font* letter.
$$ \forall j \in [1, 5]_\mathbb{Z}: \ \ X_{1j}, \ldots, X_{100j} \overset{\mathrm{i.i.d}}{\sim} \mathcal N(0,1) $$

#### Constants and Coefficients
Scalar constants and coeffients will be notated by *lower case normal font* letters. These letters may be greek or english.
$$n = 100, \ p = 5 \\ \hat y_i = \hat \beta_0 + \begin{pmatrix} X_{i1} & \ldots & X_{i5} \end{pmatrix} \begin{pmatrix} \hat\beta_1 \\ \vdots \\ \hat\beta_5 \end{pmatrix}$$



### Vectors $(v \in \mathbb R^k)$
Vectors are notated by a *normal font letter* in most cases. The reason for the distinction between bold and normal will be clear when discussing matrices.
$$X_i = \begin{pmatrix} X_{i1} \\ \vdots \\ X_{i5} \end{pmatrix} , \ \ \ \beta = \begin{pmatrix} \beta_1 \\ \vdots \\ \beta_5 \end{pmatrix}$$

#### Shape
The shape of a vector is a bit of a tricky subject. Obviously, they CAN be represented by a column or a row vector without any rhyme or reason. The truth is that they are neither. A vector is actually a rank-1 tensor, which means that it only has one dimension. Whether that dimension is represented vertically or horizontally is irrelevant.

However, this DOES becomes an important distinction in matrix algebra. This is because essentially we are often implicitly casting a rank-1 tensor to rank-2 (matrix) and although vector shapes $(k,) = (k) = (,k)$ are equivalent; matrix shapes $(k, 1) \neq (1, k)$ are not. This ambiguity does not occur with scalars since a rank-0 tensor (scalar) has shape $(0)$. Casting it to a higher rank can only result in $(1,), (,1), (1,1)$, etc. all of which are indistinguishable.

A hand-wavey way to understand when row vs. column vectors are appropriate is to understand what higher order tensors truly are. Higher order tensors CAN represent an object of higher dimension, but the same object can be used as a function to map between tensors of different dimension. In linear regression $\beta$ represents a map from a rank-1 tensor to a rank-0 tensor, compare this to $X_i$, which is used as an input to this map.

This distinction is important and our solution will be to ALWAYS use shape $(k,)$ for vectors and represent them by column vectors. Furthermore, the transpose operator $(\boldsymbol v^T)$ will be used to flip to $(,k)$ when necessary.
$$\hat y_i = \hat\beta_0 + X_i^T \hat\beta$$

### Matrices $(\boldsymbol M \in \mathbb R^{n \times p})$
Matrices are notated by a *bold letter*.

#### Shape
$\boldsymbol M$ has shape $(n,p)$: $n$ rows and $p$ columns.
$$\boldsymbol X = \begin{pmatrix} X_{11} & \ldots & X_{1p} \\ \vdots & \ddots & \vdots \\ X_{n1} & \ldots & X_{np} \end{pmatrix}$$

#### Iterators
$i \in \mathbb Z: 1 \leq i \leq n$ is used to iterate through all the rows of a matrix AND represent the selection of an arbitrary single row.
$$X_i \in \mathbb R^p$$
$j \in \mathbb Z: 1 \leq j \leq p$ is used to iterate through all the columns of a matrix AND represent the selection of an arbitrary single column.
$$\boldsymbol X_j \in \mathbb R^n$$
When referring to vector $X_k$, it is ambiguous if we are selecting a row or a column, which is why if a vector if of size $(n)$, it is denoted with a *bold* letter.

### Statistical Experiments
Recall that the goal of a statistical experiment is to take measurements on a *sample* and extrapolate the results to the entire *population*.

Tensors of rank 0, 1, and 2 adhering to the notational rules above will be used together to represent various components within a statistical experiment. Note that many statistical experiments can be used on a single dataset.

For contextualizing the following subsections, consider this example. We are interested in predicting the height of a random person in our city based upon their age, sex, and weight. We will take a random sample of $100$ people where we record their height, age, sex, and weight.

#### Set Up
Before an experiment begins, multiple parameters must be selected to govern it. 2 of the most important are:
$n$ - Number of observations
$p$ - Number of predictors

In our example $n = 100$ and $p = 3$

#### Random Variable (RV)
An experiment begins with the repeated measurements. Each measurement is a *Random Variable*.
$$ \forall i \in [1,n], j \in [1, p]_\mathbb{Z}: \ \ X_{ij} \overset{\mathrm{i.i.d}}{\sim} \mathcal N(0,1) $$

For each observation $i$, $p$ predictive RVs: $X_{i1}, \ldots, X_{ip}$ are measured making a total of $np$ RVs. In supervised learning situations, there are total of $n(p + 1)$ RVs since an outcome RV $(Y_i)$ is also measured.

In our example, there is an outcome (height) thus supervised learning approaches are appropriate. For observation $i$ Let us define our RVs.
$Y_i$ - height (decimal)
$X_{i1}$ - age (integer)
$X_{i2}$ - sex (factor - 2)
$X_{i3}$ - weight (decimal)

#### Observation
Each of these RVs is grouped into a single *observation*. We are most interested in the feature vector of observation-$i$.
$$X_i = \begin{pmatrix} X_{i1} \\ \vdots \\ X_{ip} \end{pmatrix}$$

Note that outcome $y_i$ may have been measured, but is not part of $X_i$.

#### Sample
All $n$ feature vectors can be grouped together into a single *sample*.
$$\boldsymbol X = \begin{pmatrix} X_1 \\ \vdots \\ X_n \end{pmatrix} = \begin{pmatrix} X_{1,1} & \ldots & X_{1p} \\ \vdots & \ddots & \vdots \\ X_{n1} & \ldots & X_{np} \end{pmatrix}$$

$\boldsymbol{X}_j$ is a vector of specific interest. It has many uses across various SL techniques and is a sample of feature $j$. The goal is that $n$ is large enough so that each $\boldsymbol X_j$ has the same distribution as the feature in the population. While each element is still an RV, $\boldsymbol X_j$ is a *variable* (not random).

#### Outcome
This is only relevant in experiments with a defined outcome. As mentioned in the RV section, there are an extra $p$ measured RVs missing from our *sample* matrix. We store them seperate in an *outcome* vector $(\boldsymbol Y)$.
$$\boldsymbol Y = \begin{pmatrix} Y_1 \\ \vdots \\ Y_n \end{pmatrix}$$

#### Putting it Together
All of these parts represent the data collection stage. The question that we have hopefully already answered (with a yes) before we began our experiment is if we believe there truly exists a function $f$ that maps $X_i$ to $Y_i$.
$$Y = f(X) + \epsilon$$

Here $\epsilon$ represents random noise present in the real world. Our goal now is to use the data that we have gathered to predict $f$. We want to train a *model* on our data.
$$\hat {\boldsymbol Y} = \hat f (\boldsymbol X)$$

Here $\hat{\boldsymbol{Y}}$ represents our *predicted* outcomes. There is an infinite number of models $(\hat f)$ that can accomplish this, but our predictions will just be really bad. To check if our predictions are good we measure the residual error of observation-$i$: $e_i = Y_i - \hat Y_i$. The lower $|e_i|$ is the better our model performed for data point $i$. Thus we want a model with a small magnitude of $\boldsymbol{e} = \begin{pmatrix} e_1 & \ldots & e_n \end{pmatrix}^T$ such that
$$\boldsymbol Y = \hat f (\boldsymbol X) + e$$

We mentioned before that it we can make $\hat f$ function and just accept that $e$ will be very large. It is also quite easy for a computer to play "connect-the-dots" and find a $\hat f$ with a near 0 magnitude $e$. This is also not a good model because of *overfitting*. This will be discussed deeper in future chapters, but as a preliminary look at the equation that we are modeling, the $\epsilon$ term is the key. Random noise exists in the real world and thus, we do not want $\hat f$ to be a perfect map to the outcome. Instead of $|e| = 0$ we actually want $e = \epsilon$. The problem is that $\epsilon$ is unmeasurable.

#### What's Next
Our next step is to collect a new sample. Our first sample is our training data. Our next sample is testing data. Our model was created with no knowledge of this data. Evaluating its performance on this new data is our best metric of its performance.

#### Summary
We can summarize the various objects that we now have 

#### Parameters
The experiment is governed by the selection of various parameters. 2 of the most important are:

$x$ - Predictive quantity of interest
$y$ - Outcome measurement

|     Variable      |     Denotes     |      Collection      |     Tensor      | Shape |
| :---------------: | :-------------: | :------------------: | :-------------: | :---: |
|  $\boldsymbol X$  |     Sample      | $n$ Feature Vectors  | Rank-2 (matrix) | (n,p) |
|  $\boldsymbol Y$  |     Labels      |     $n$ Outcomes     | Rank-1 (vector) |  (n)  |
| $\boldsymbol X_j$ |    Variable     | $n$ Random Variables | Rank-1 (vector) |  (n)  |
|       $X_i$       | Feature Vector  | $p$ Random Variables | Rank-1 (vector) |  (p)  |
|       $Y_i$       |  Outcome (RV)   |         self         | Rank-0 (scalar) |  ()   |
|     $X_{ij}$      | Random Variable |         self         | Rank-0 (scalar) |  ()   |

#### Random Variable
A *Random Variable* (RV) is a quantity that is unknown until its value is measured. The objective of *Statistical Learning* is to predict the measurement of one RV based of the measurement of others.
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