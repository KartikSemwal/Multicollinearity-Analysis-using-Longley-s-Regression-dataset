## Multicollinearity-Analysis-using-Longley-s-Regression-dataset
Multicollinearity occurs when two or more independent variables in a regression model are highly correlated with each other. This means they provide overlapping information, making it difficult for the model to isolate the individual effect of each predictor on the target variable.
While multicollinearity does not affect the overall accuracy or predictions of the model, it severely damages the interpretability of your results:
*_Unstable Coefficients:_ The regression coefficients can fluctuate wildly and change signs based on which other variables are added or removed.
*_Inflated Standard Errors:_ High correlation increases the standard errors of the coefficients, making variables appear statistically insignificant when they actually might be important.

This mini project digs deeper into the concept of multicollinearity, how to detect its presence and what measures to take while dealing with multicollinearity within our dataset.

## About the Dataset
The Longley dataset is a classic US macroeconomic dataset introduced by J.W. Longley in 1967 to test the numerical accuracy of least-squares computer programs. It is famously used to evaluate regression algorithms due to severe multicollinearity among its variables.
Time Period: Annual observations from 1947 to 1962 (n=16).
Features: 6 explanatory variables:
* X1: GNP Implicit Price Deflator
* X2: Gross National Product (GNP)
* X3: Number of Unemployed
* X4: Number of people in the Armed Forces
* X5: Non-institutionalized Population >= 14 years oldYear
* X6: (Time trend)
* Target Variable(Y): Total Employed

## Objectives:
* To fit a **regression** of Y on rest of the independent variables. 
* To detect the presence of Multicollineairty in our dataset based on t-tests and anova.
* Using the rule of thumb i.e. **Auxuliary regression** and **Pairwise correlations** to explore the possibility of high multicollinearity.
* Using the method based on **Fischer's Confluence Analysis** to determine **Useful, Superfluous and Detrimental** variables in the model
* Use the **Farrar and Glauber** test to detect Multicollinearity in the model.

## Key steps and Methodologies:
All the analysis has been done in Excel and SAS(Statistical Analysis System) only.

**_1. Data Collection & Preprocessing:_**
* Source: The data has been collected from Kaggle 
* The dataset is available in the Longley's dataset/ folder with relevant documentation.

**_2.Regression analysis:_**
* Regression of Y on rest of the variables is done to check the overall R^2 value of our dataset and obviously the ANOVA table to check the significance of our model
* Parameter table shows the t-values and the p-values of individual variables through which we can detect which of the variables are insignificant i.e. their p-value is less than 0.05
* We can also check the VIF (Variance Inflation Factor) to check for multicollinearity in the model.
   * If VIF = 1 there is no correlation b/w the variables
   * IF 1 < VIF < 5: The variables are moderately correlated, but model is acceptable
   * VIF > 5 or 10: This indicates a critical level of multicollinearity.
* This is done to suspect the presence of multicollinearity in our model.

**_3.Rule of thumb:_**
* Auxiliary regressions:
  * Individual R^2 values of each independent variables is calculated by making each of them depend variable one by ane and then regressing them with rest of the remaining independent variables.
  * Then these R^2 values are then compared with the overall R^2 value that we calculated above.
  * If auxuliary R^2 is greater than the overall R^2 value, it means that the multicollinearity in the dataset is due to that specific variable
* Pairwise Correlation among regressors:
  * Here we examine the bivariate correlation between explaratory variables
  * If we detect high pairwise correlation between two variables, it means that multicollinearity is present and it is a serious problem in the model.

**_4.Fisher's Confluence Analysis:_**
* In this method, we combine the information from R^2, bivariate correlation and standard error to detect the multicollinearity.
* Here, we classify the variables as Useful, Superfluous and Detrimental
* Useful variavble is retained in the model
* Superfluous variable is rejected from the model
* Detrimental variable is kept in the model after following certain remedial measures.

**_5.Farrar & Glauber Test:_**
It consists of 3 Tests:
* Chi-Square test for detection of multicollinearity and its severity.
   * H0 = Xi's are orthogonal, i.e. MC is absent.
   * H1 = Xi's are not orthogonal, i.e. MC is present.
   * The chi sqaure test statistic is given by: χ² = −[n − 1 − (2p + 5)/6] × ln(det(R)) and is carried out as right tailed test.
* A F-test for finding the location of Multicollinearity.
   * H0 = R^2 = 0
   * H1 = R^2 not equals to 0
   * The F Test statistic is given by: (R^2/(k-1))/((1-R^2)/(n-k)) ~ F(k-1,n-k) where R^2 is the auxiliary regression of individual variable.
* A t-test for finding out the pattern of multicollinearity i.ie finding out the vairable with which the multicollinearity variables are interrelated.
   * H0: the partial correlation is 0.
   * H1: the partial correlation is not 0
   * The t test statistic is given by r^2*sqrt(n-k)/sqrt(1-r^2) ~ t(n-k), where r^2 is the partial correlation between any two regressors.
  
## Obsevations:
* From ANOVA table the model is coming out to be highly significant as 0<0.05
* Out of the 5 explanatory variables, 4(x1,x3,x4,x5) are coming out to be insignificant i.e. thier p values are grater than 0.05.
* __VIF__ of X1, X2, X3 and X5 is greater than 10, showing critical multicollinearity.
* Overall R^2 = 0.987, which means that the model explains 98.7% of the variations.
  
* Auxiliary R^2 X1 = 0.992 > Overall R^2, meaning mc is due to X1
* Auxiliary R^2 X2 = 0.998 > Overall R^2, meaning mc is due to X2
* Auxiliary R^2 X3 = 0.907 < Overall R^2, meaning mc is not due to X3
* Auxiliary R^2 X4 = 0.601 < Overall R^2, meaning mc is not due to X4
* Auxiliary R^2 X5 = 0.997 > Overall R^2, meaning mc is due to X5

* Pairs X1-X2, X1-X5 and X2-X5 shows high pairwise correlation (>0.8), showing mc is a serious problem in the model.

* For __Fischer's confluence__, X2 was taken as the base model as its auxiliary R^2 was the highest (0.998).
* Adding X1 to base model bought negligible change in R^2, thus it is superfluous.
* Adding X3 in the base model, improves R^2 and the model remains significant as well. Thus X3 is regarded as useful and is ratained in the model.
* Adding X4 in the model increases the R^2, but X4 here is insignificant as its p-value is 0.083 (>0.05). Thus we can regard X4 as superfluous and remove it.
* Adding X5 bought negligible change in R^2 and also its addition makes X3 insignificant which was before significant in the model. Thus X5 may be regarded as Detrimental.

__* The Farrar & Glauber test:__
* chi-square test statistics = 141.64
* chi-sq tabulated value at 5% LOS at 10 d.f is 18.307
* Thus Null hypothesis that Xi's are orthogonal is rejected. Thus there is MC present in the model.

__* F test:__
* For all the Xi's we calculated the F statistic and all the calculated values came out to be greater than the tabulated value at 5% level of significance at (4,12) d.f.
* Thus we rejected the Null hypothesis that the Xi's are orthogonal. This implies that there is multicolllinearity in the model due to Xi's

__* t-test:__
* The pairs which showed high multicollinearity were: X2-X5, X1-X3, X1-X2 and X3-X5, as thier t values were greater than the tabulated t value at 5% LOS at 11 d.f.
