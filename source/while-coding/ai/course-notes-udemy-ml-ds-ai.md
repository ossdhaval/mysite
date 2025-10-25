# Machine Learning, Data Science & AI Engineering with Python

Course link: https://www.udemy.com/course/data-science-and-machine-learning-with-python-hands-on/learn/lecture/15090142#overview

## Installations

- install anaconda
- `conda activate base`
- 
- install pydotplus : `conda install pydotplus`
- install tensorflow-gpu. Tensorflow installation using the command `conda install tensorflow-gpu` fails if your environment is using the latest python 3.13. At this moment the latest supported python
  is by tensoflow is `3.12`. So we neeed to downgrade the python to install tensorflow using `conda install python=3.12 `. Then install tensorflow `conda install tensorflow-gpu`
- download course material from: https://www.sundog-education.com/machine-learning/. Unzip the file in a directory (e.g `~/docs/learning/tech/certifications/ai/udemy-ml-ds-ai-course/MLCourse`). Open terminal and `cd` to that directory. Then type `jupyter notebook`. A browser should open with your notebooks. 

## statistics

- Mean: aka average. It doesn't give correct idea if your data has outliers.
- Median: sort the sample data and pick the one in the middle, that is your median. Outliers doesn't impact median. This is often a better measure if your data has outliers.
- Mode: is the most frequetly occuring value in your data.

- Histogram: A histogram is a graphical representation of the distribution of numerical data, where the data is grouped into continuous intervals called bins. It consists of adjacent rectangular bars where each bar's height corresponds to the frequency (count) of data points within that bin. Unlike bar graphs, histograms have no space between bars because the bins represent continuous data ranges. The width of each bar represents the interval of values, and the area or height of the bars indicates how often data in those intervals occur, helping to visualize how data is spread, concentrated, or if there are any gaps or patterns in the dataset.

- regression: english meaning: a return to a previous or way of behaving.
- regression analysis: In statistical modeling, regression analysis is a statistical method for estimating the relationship between a dependent variable and one or more independent variables. How does weight of a person change relative to their height. 
- linear regression: The most common form of regression analysis is linear regression, in which the purpose is to find the line that most closely fits the data according to a specific mathematical criterion. For example, the method of ordinary least squares(OLS) computes the unique line that minimizes the sum of squared differences between the data and that line. This line can then be extended to predict unseen data. Another way to perform linear regression is  `gradient descent`. This method is better for 3 dimensional or multi-dimentional data. 
  - r-squared:

    First understand The r value, or correlation coefficient. It measures the strength and direction of a linear relationship between two variables, ranging from -1 to 1. An r value of 1 indicates a perfect positive correlation, while -1 indicates a perfect negative correlation, and 0 means no correlation exists.

    Now `r-squared` is a method of knowing how well the line is fitting the data. It has a value between 0 to 1.  1 means that line is right in the middle of the observations, meaning that each dot(observation) is at equal distance from the line on the both sides, hence it is the best fitting line that you have, i.e the line has fully minimised the squared differences from observations. 0 mean the line does not, at all, minimise the squared differences and is a worse fit. 

    How r-squared helps: You can create a regression for your data using different techniques (linear, it helps you in choosing the correct regression technique by looking at it's r-squared value.

- different regression techniques

  Regression Type                         |  Description                                                                                                             |  Typical Use Case                                                                   
----------------------------------------+--------------------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------
Linear Regression                       |  Models a straight-line relationship between one or more independent variables and a continuous dependent variable.      |  Predicting house prices, sales trends, or temperature levels .                     
Multiple Linear Regression              |  Extension of linear regression using multiple predictors for a single continuous outcome.                               |  Estimating employee salaries from multiple features (experience, education, etc.) .
Logistic Regression                     |  Used when the dependent variable is categorical (binary or multinomial). Predicts probabilities between 0 and 1.        |  Classifying spam vs. not-spam emails, churn prediction .                           
Polynomial Regression                   |  Fits a non-linear (curved) relationship between variables using polynomial terms.                                       |  Modeling growth curves or complex biological relationships .                       
Ridge Regression                        |  A linear regression withL2 regularization, reducing coefficient magnitude to handle multicollinearity and overfitting.  |  High-dimensional datasets with correlated features .                               
Lasso Regression                        |  UsesL1 regularizationto shrink some coefficients to zero, effectively performing feature selection.                     |  Sparse feature selection in big data problems .                                    
Elastic Net Regression                  |  Combines Lasso and Ridge penalties (L1 + L2) to balance coefficient shrinkage and variable selection.                   |  Text or genomic data prediction with many features .                               
Stepwise Regression                     |  Automates variable selection using statistical tests (forward/backward inclusion).                                      |  Identifying significant predictors in large feature spaces .                       
Support Vector Regression (SVR)         |  Based on support vector machines; fits the regression within a defined margin of error.                                 |  Non-linear relationships and noise-tolerant predictions .                          
Decision Tree Regression                |  Splits data into branches to predict values based on decision rules.                                                    |  Modeling categorical and non-linear relationships .                                
Random Forest Regression                |  Ensemble of decision trees averaging results for stability and accuracy.                                                |  Financial forecasting, energy consumption prediction .                             
Bayesian Regression                     |  Applies Bayes’ theorem to estimate probabilistic distributions of model parameters.                                     |  Medical data and uncertainty quantification .                                      
Partial Least Squares (PLS) Regression  |  Reduces features into uncorrelated components before regression, handling multicollinearity.                            |  Chemometrics and bioinformatics .                                                  
