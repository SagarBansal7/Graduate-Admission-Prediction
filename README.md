# Graduate Admission Prediction
## Graduate Course: Managerial Statistics

### Introduction 

This was a team project from a course on Managerial Statistics where we evaluated several parameters which are considered important during the application for masters programs. When we went through the process of preparing, applying, and collecting required documents for the admission, we were less informed about how and in what percentage the individual documents will contribute to our selection. Here in this study, we will try to find interesting pattern on how different features relate to chances of admit. The results will surely reveal something insightful. In addition, we have emphasized on making this report comprehensible for non-statistical/technical audiences so the results can then be used by the potential students in strengthening their profile accordingly.

### Data Characteristics

We are looking at the university data and different admission scores, how it’s correlated to university ranks and if there is a way to predict the admission based on those scores. The hypothesis question we would like to answer is whether the score will be significantly higher for higher ranking university. The data has 400 different results that contain GRE score, TOEFL score, University Rating, SOP, LOR, CGPA, Research (if there’s a research done) and chance of admission based on those scores. 

#### Data Summary

> **For the graduate admission prediction dataset, following is the brief description of the dataset and its features:**
> 
> **Quantitative features:**
> GRE Score - ranges from 260 to 340, integer data type.
> TOEFL Score - ranges from 0 to 120, integer data type.
> SOP strength - ranges from 1 to 5, decimal data type.
> LOR strength - ranges from 1 to 5, decimal data type.
> CGPA - maximum 10, decimal data type.
> 
> **Qualitative feature:** 
> Research Experience – 0 or 1.
> University Rating - ranges from 1 to 5.
> 
> **Total number of independent features**: 7.
> 
> **Total number of observations**: 400.
> 
> **Target Variable**: Chance of Admit - ranges from 0 to 1, decimal data type.
> 
> (Source: https://www.kaggle.com/mohansacharya/graduate-admissions#Admission_Predict_Ver1.1.csv)

Here, we can see that the dataset is very rich with useful information. It contains all the major contributing factors which result in an admit or rejection. We have different types of data such as qualitative (ordinal, nominal) and quantitative with different ranges. As we observed, the GRE score has a minimum possible value of 260 and maximum possible value of 340. Similarly, TOEFL score can go as low as 0 and as high as 120. Both are integer type i.e., the values are non-decimal. In contrast, the SOP and LOR strength variables are decimal variables. They can go up to one decimal value. Both ranges from 1 to 5. At last, CGPA can have up to two decimal values, ranging from 0 to 10. (Note: Although the data may not contain the lowest values for all the quantitative variables, the variables can have those values if we add more data in future).

For qualitative variable, we have university rating and Research experience. Even though the university rating looks like a quantitative variable, on close inspection we can observe that they have an intrinsic order in them, Also, the numbers 1 to 5 do not make much sense in terms of numeric/arithmetic properties i.e., we could have used A to E instead. The properties that matter is that they are distinct and have an order property. 

In the next sections, we will start with the descriptive evaluation and visualization of data to get a better understanding of it. After that, we will construct a methodology suitable to the data we have. This will help us in focusing on important features critical to increase the chance of admit and make recommendation accordingly. We will then provide a conclusion from the results and corresponding interpretations we get.

### Descriptive Summary

First, we calculated averages and mediums of each score. The results are similar for both which means that our data is symmetric. This table below also shows that average scores will give 72% chance of admission. Half of the average admissions include research paper. Median university rank is 3 out of 5. Standard deviation for TOEFL and GRE score shows that there is a dispersion (spread) in the scores, meaning that some admission scores submitted were much better and/or some worse than the average. CGPA scores have very low deviation meaning that they were consistent. 


#### Table 1: Summary Statistics of Graduate Admission

![Image 2](https://user-images.githubusercontent.com/37155988/92817880-11a62800-f395-11ea-86c0-d340afc44165.png)

Since the average university rank is 3 and the university rank 3 shows the highest frequency compared to other university ranks shown in the figure below. We decided to look for the average scores’ person needs to have a higher chance (90%) of being admitted and what are the lower scores with less chances of being admitted (36% chance). We also looked at the higher rated university scores, what is needed to be admitted to such university and what scores are required. The table below shows that with 90% chance of admission the scores are the same for university that is ranked 3 and 5. We noticed that the chance of admission is much less when there is no research submitted for admission. It is also showing that the highest chance of admission (97%) for the highest ranked university (5 out of 5) requires the highest scores for everything. In other words, whoever receives the highest scores plus submits a research work has almost 97% chance of being admitted. 

#### Graph 1: Histogram for University Rating

<img src="https://user-images.githubusercontent.com/37155988/93022763-df751000-f5b8-11ea-835f-a623c3df386d.png" width="400">

#### Table 2: Average profiles with highest and lowest chance of admits for 3 and 5 rated universities.

![Table 2](https://user-images.githubusercontent.com/37155988/93023953-99bc4580-f5c0-11ea-943b-7719378506fe.png)

Following table 3 showing values at the 90th percentile for each feature. For universities with rating “3”, it suggests that the 325.6 is greater than the 90 percent of student’s GRE scores. Similarly, 112 for TOEFL score, 4 for SOP Strength, 4.5 for LOR strength, 9.04 for CGPA and 1 for Research.  For the five rated universities, the values are significantly high. It is 338.9 for GRE score, 119 for TOEFL score, 5 for SOP Strength, 5 for LOR strength, 9.778 for CGPA and 1 for Research.  Scores have to be higher for higher ranked universities. 

Note that, 90th percentile for 3 and 5 rated universities is different than having the 90% chance of admission for 3 and 5 rated universities. The latter is the value of our target variable as “Chances of Admit” tells us the percentage. Whereas 90th percentile is the calculation done on all the values and getting the one having 90% of the values below it.

#### Table 3: Student profiles at 90th percentile of chance of admit for 3 and 5 rated universities 

![Table 3](https://user-images.githubusercontent.com/37155988/93022839-35e24e80-f5b9-11ea-8094-c18d11bcfa16.png)

#### Graph 2: Average TOEFL scores and average GRE scores by university rank

<img src="https://user-images.githubusercontent.com/37155988/93022773-edc32c00-f5b8-11ea-9de6-3bb249f25306.png" width="500">

The Graph 1 above displaying two admission measures TOEFL and GRE exams from the 400 samples that shows that there is a definite increase of needed scores to be admitted to a higher ranked university. We based this off our experience when applying to different Grad Schools. TOEFL is usually only required for Undergraduate admissions which is not the case of our dataset. It makes sense to exclude TOEFL score as we will see later in our methodology section that it proved not to be a useful predictor of our model. Moreover, the variations in the TOEFL score distorts some of our model assumptions such as the assumption of the constant variance.

### Methodology

First, we start off by exploring the correlation of our independent variables with our dependent variable “Chance of Admit” by using some scatterplots and correlation matrices. 

The diagram below shows GRE scores to Chance of Admission that shows us that the higher the score the higher the chance to be admitted.

#### Graph 3: Scatter plot between chance of admit and GRE score

![Graph 3](https://user-images.githubusercontent.com/37155988/93022781-f87dc100-f5b8-11ea-8ee7-68cf9a2c3a08.png)

The diagram below shows TOEFL scores to Chance of Admission that shows the higher the score the higher the chance of admission. However, we can see the extreme variations in the TOEFL scores with regards to the Chance of Admit which solidifies our decision statistically for not using it as a variable to predict the chance of admit.

#### Graph 4: Scatter plot between chance of admit and TOEFL score

<img src="https://user-images.githubusercontent.com/37155988/93022788-00d5fc00-f5b9-11ea-83c4-97a9270494a4.png" width="500">

The diagram below shows a scatterplot of x = CGPA and y = Chance of Admit. We can see a high correlation between CGPA and the chance of admit. We see an interesting trend here as the CGPA gets higher we see a lower variation in the chance of admit. Contextually speaking this makes sense because universities usually require a range of CGPA. For example, universities won’t require a specific CGPA like exactly 9 or 10 to admit students they ask to have a CGPA of 9 or above. Therefore, a CGPA of 9 could have the same chance of admit as a student with a 9.5 CGPA. Moreover, the reason why sees less variations in the chance of admit could also be because the number of students with a high CGPA are less than students with an average or lower CGPA. Overall, we think CGPA will be a good predictor for our model because of our experience and we will see below the correlation matrix shows the highest correlation with the chance of admit (0.87328910).

#### Graph 5: Scatter plot between chance of admit and CGPA

<img src="https://user-images.githubusercontent.com/37155988/93022798-0895a080-f5b9-11ea-92bf-55b62d8ed4b2.png" width="500">

#### Graph 6: Correlation Matrix of Variables

<img src="https://user-images.githubusercontent.com/37155988/93022801-11867200-f5b9-11ea-8a07-e9e5939a215f.png" width="500">

#### Table 4: Step Wise Regression Analysis

<img src="https://user-images.githubusercontent.com/37155988/93022846-3ed32000-f5b9-11ea-921a-f4fadb78aa6e.png" width="500">

Step Wise Analysis is a process of fitting regression model in which the choice of predictive model is carried out by an automatic process.

From the above table 4, we can see a Stepwise Analysis to figure out which are the most important variables which impacts the chance of admit and to what extent. To run a step wise analysis, we consider “Chance of Admit” as the dependent variable, while remainder of the factors are considered as independent variables. From the Table 4, we can see that we have CGPA, GRE Score, LOR, and Research as the most important variables on which the Chances of Admit depends. Again, if we look at the Table 4, and if we see the second column R square, we can interpret that CGPA explains 76.2% of variation in Chance of Admit making CGPA the most important factor while calculating chances of admission. 

Four of the variables combined help is explaining the variation by ~80% which is significantly high and thus, tells us that we have a good chance of predicting the model. 

Remaining 20% of the variation can include other factors such as Ambition of a student or maybe, other subjective factors which we don’t have the data for. Further Market Research study will help us to enable more insightful actions/recommendations to build an even robust model.

#### Table 5: Coefficient Summary for Step Wise Analysis

![Table 5](https://user-images.githubusercontent.com/37155988/93022852-485c8800-f5b9-11ea-8fdc-cfea0e13138e.png)

In the table 5, we can observe the coefficient value (Unstandardized B) of each of the independent variables. 
Considering that we have an equation as Y = m1x1 + m2x2 + m3x3 + m4x4 + c

x1 = GRE Score
x2 = LOR
x3 = CGPA
x4 = Research 

The sign of Unstandardized B – gives us the direction of the relationship independent variables has with the dependent variables. Since, all the independent variables are positive, this implies that they have a positive impact on the Chance of Admit. 

Basis the above equation, we can come up with an equation such as: 

**Chance of Admit = 0.003*GRE + 0.023*LOR + 0.134*CGPA + 0.025*Research**

**a) Confidence Interval**

Here, we will construct the confidence interval for each of the independent feature which are significant based on the previous Step Wise Analysis we performed as well as the target variable. Those features are GRE Score, LOR, CGPA and Research. We know from the Table 1, the mean for each of them. They are 316.8, 3.5, 8.6 and 0.5 for GRE Score, LOR, CGPA and Research respectively. We then calculated the Margin of error with alpha as 0.05 (95% confidence level), Standard deviation (specific to each of them), and the sample size of 400.

#### Table 6: Summary Statistics of Graduate Admission

![Table 6](https://user-images.githubusercontent.com/37155988/93022859-50b4c300-f5b9-11ea-84b0-125c26deea17.png)

**Interpretations:**

1)	GRE Score: 
At 5% significance level, we can say that the average population value of the GRE Score will lie in between 315.68 and 317.92. 

2)	LOR:
At 5% significance level, we can say that the average population value of the LOR will lie in between 3.41 and 3.59. 

3)	CGPA:
At 5% significance level, we can say that the average population value of the CGPA will lie in between 8.54 and 8.66. 

4)	Research:
At 5% significance level, we can say that the average population value of the Research will lie in between 0.45 and 0.55. 

5)	Chance of Admit:
At 5% significance level, we can say that the average population value of our target variable (Chance of Admit) will lie in between **70.63% and 73.37%**.

These intervals will help us in inferring the possible mean value range for different samples we evaluate for the same population. In addition, we get an important insight about our target variable “Chance of Admit”. We noted that on average the mean of chance of admit varies between 70.63% and 73.37%. This is very important because the range is **significantly far from 50%** i.e., many more than half of the students have a good chance to get an admit from the university they apply, and they actually get it. This information can also be used by the future applicants as a motivation to apply and expect to get an admit.

**b) Hypothesis Testing/ANOVA**

Early on in our introduction to the data set we mentioned about the hypothesis to establish that higher university ranking, the higher the chance of admit. Now we will do a hypothesis test to establish the fact that there exists a relationship between University Ranking and Chance of Admit using one way ANOVA.  

For simplification, going forward, we will call University Ranking as UR, Chance of Admit as CoA! 

For Hypothesis Testing, our first step is to create Null & Alternative hypothesis. 

H0 : μ1 = μ2 (There exists no relation whatsoever b/w UR and CoA)
Ha : μ1 is not equal to μ2 (There exists a relationship b/w UR and CoA)
where μ1 = Average of University Ranking
and μ2 = Average of Chances of Admit

For this hypothesis, we will use α = 0.05 = Significance Value and now, we will check which of the hypothesis is true using ANOVA! We will be doing an ANOVA test between University Rating and Chance of Admit.  

#### Table 7: Summary Statistics of Graduate Admission
![Table 7 a](https://user-images.githubusercontent.com/37155988/93024790-01758f00-f5c7-11ea-88bc-310b37a11380.png)

![Table 7 b](https://user-images.githubusercontent.com/37155988/93023426-e867e080-f5bc-11ea-80a6-c437586bd9d8.png)

From the above ANOVA analysis, we can observe that p-value = 1.2099E-198.

Since our p-value is less than α, we will reject the null hypothesis and can call out that our result is statically significant. 

Now, let’s go back a few steps and recall, what did we say in our Alternate Hypothesis (Ha), our alternate hypothesis calls out that μ1 is not equal to μ2 and hence, there exists a relation between University Ranking and Chance of Admit. 

From the above analysis of variance test (ANOVA), we can conclude that the higher the university ranking, the higher the chances of admit.  

**c) Regression Analysis**

We had to do some outside research for what regression method would be best and we decided to go with regression through the origin with no Beta-0 intercept. This is because it makes sense contextually that there should be no intercept for the chance of admit because if a student has 0 scores for the variables analyzed above his/her chance of admit would be zero. Moreover, after exploring the data and the relation between variables we found that students that are applying to higher ranked universities need higher scores for GRE. Therefore, we decided to try out an interaction term using University Rating with different variables. The interaction term between GRE Scores\*University Rating appeared to be the most significant. Below is the model initiated using R-studio.

    model = lm (`Chance of Admit` ~ 0 +`GRE Score`*University Rating + CGPA + LOR+ Research)
 
![Table 8](https://user-images.githubusercontent.com/37155988/93025593-16552100-f5cd-11ea-865a-2dccdeb3f707.png)

    Y = 0.0232654x1 + 0.1313719x2 – 0.1313719x3 – 0.3802179x4 + 0.0012303

<img src="https://user-images.githubusercontent.com/37155988/93025594-16edb780-f5cd-11ea-9a35-e9f009f3d60c.png" width="500">

Above we can see the out- put of R shows a highly significant F-test (p-value < 2.2\*10^-16) which tells us that this is a highly useful model for predicting the chance of admission. Moreover, the individual t-tests for our independent variables show that our predictors are highly significant at the alpha = .01 level. The adjusted R-squared of our Model shows that our model can predict the chances of admission with high precision by explaining approximately 99% of the observed variations in the chances of admissions in our dataset.  Next, we start checking for any Multicollinearities using the Vif function in R which represents the variance inflation factors of the model. Any Vif > 5 is usually representing that multicollinearity exists in our model. Below we can see that there is Multicollinearity. However, after doing some research we learnt that Multicollinearity is not always a problem. It is a problem when the global F-test shows a significant p-value and the individual t-tests are distorted. This is not our case because all the individual t-tests are very highly significant. Therefore, in this case Multicollinearity is not causing any problems to our model.

<img src="https://user-images.githubusercontent.com/37155988/93025595-17864e00-f5cd-11ea-88a7-28952945f229.png" width="500">

#### Checking Observed values vs Predicted Values (Y vs Y-hat) and Model Assumption of Constant Variance

#### Graph 6: Plot(Chance of Admit, model$fittedvalues)

<img src="https://user-images.githubusercontent.com/37155988/93025596-17864e00-f5cd-11ea-8e97-0871c72c15b7.png" width="500">

It is quite clear to us that the model can precisely predict the chances of admission between 0.8 and 0.9 (80% - 90%). In contrast, the model does poorly at predicting the chances of admission below 70%. In the diagram below we can also see that the unobserved variables which is known as residuals or predicted errors have a higher impact on lower chances of admission compared to the higher admissions. The problem of constant variance here known as heteroscedasticity is seen. This implies a misspecification of the model or that we should use some techniques such as logistic regression to transform some variables and go through the process of variance stabilization. This is some advanced statistics that we did not cover in class and hope to cover in upcoming stats courses. However, we believe there are some contextual reasons that may have caused this heteroscedasticity. Note, that the explained by variance of the model is extremely high.  One reason for heteroscedasticity is that our dataset and model do not encompass how determined or ambitious the student applying is. For instance, a student who has high scores on all tests and strong Letters of Recommendations is likely to seem to the recruiter as highly ambitious and the recruiter would highly admit the student. The high ambition of the student could have highly contributed to the chances of admission. This shows that there are some unobserved factors that have not been considered that contributes highly to the high chances of admission. Moreover, we know that beyond a certain threshold student will be admitted instantly. While students with lower scores will be admitted based on other factors that are only known to the recruiter. Also, this depends on the recruiter himself some recruiters value some factors more than other factors. Therefore, we kind of get a sense that the heteroscedasticity arising might not be from the model misspecification but could be from other factors that are not captured by the dataset.

#### Graph 7: Plot(model$fittedvalues, model$residuals)

<img src="https://user-images.githubusercontent.com/37155988/93025597-181ee480-f5cd-11ea-9e81-62c76286a401.png" width="500">

#### Graph 8: Hist(model$residuals) Checking the assumption of Distribution of estimated errors

<img src="https://user-images.githubusercontent.com/37155988/93025598-181ee480-f5cd-11ea-99e6-d0b00a6b252c.png" width="500">

Here checking the distribution of the model residuals, we can see that it is fairly negatively skewed, and it is not satisfying the model assumption of normality. On the next page, we used the q-q norm function and we see a slight curvature which shows that it doesn’t satisfy the model assumption that errors are normally distributed (Graph 9 ). A QQ plot combines a normally distributed set of quantiles and if they are both normally distributed that means we should see a straight line. In our case we see a slight curvature which further enhances that the model assumption of the errors being normally distributed is violated.

#### Graph 9: QQnorm Checking the assumption of Distribution of estimated errors

<img src="https://user-images.githubusercontent.com/37155988/93025599-181ee480-f5cd-11ea-8f50-e14b7b5a077b.png" width="500">

After some research we decided to transform some terms to try to satisfy the model assumption. Therefore, our new model is model2 = lm (`Chance of Admit`~ 0 + LOR + CGPA +log (`GRE Score`\*`University Rating`)). By adding the term log () to the interaction term we see in Graph 10 is that the curvature is slightly fixed. Also, all the p-values for the variables and the global F – test are significant with a slightly lower adjusted R-square of .98. This means that our model explains 98% of the observed variations in the chances of predictions of admitting students.

#### Graph 10: QQnorm with the log() term

<img src="https://user-images.githubusercontent.com/37155988/93025600-181ee480-f5cd-11ea-8590-cc58287b034a.png" width="500">

### Conclusion and Future Directions

Based on the above findings, or the analysis that we have done/presented, we can infer the below mentioned info: 

*	We are 95% confident that the mean of all chance of admits lies between 70.63% and 73.37% i.e., many more than half of the students who apply get an admit.
*	Using ANOVA, we concluded that higher the GRE Score, more are the chances of a student getting admitted to a high university ranking!
*	CGPA, GRE Score, LOR, and Research comes out to be the most important factors among all the variables on which the chances of admission depend.
*	Since all of these have a positive relationship with the Chance of Admission, higher the independent factors, more will be the Chance of Admission.

Our report is open to use for future research as the data may change and we may find more data features with all of them that were given to us. We would suggest collecting data that involves some of the following:
*	The dataset didn’t include the circumstances in which a student applied in. For instance, a student can be privileged in terms of financial resources. He may have used his family reputation or wealth in getting an admit. This isn’t captured in the dataset which could be a reason for inaccuracy percent of the model.
*	In addition, two universities with the same rating can have a totally different process of student selection. Some universities focus more on the CGPA of the candidate and others emphasize on the GRE score. So, having the University name and selection criteria for each record in the dataset can truly help us in further digging into the patterns and going more granular.

### References 

*	Mohan S Acharya, Asfia Armaan, Aneeta S Antony: A Comparison of Regression Models for Prediction of Graduate Admissions, IEEE International Conference on Computational Intelligence in Data Science 2019
*	Jaggia, Sanjiv, and Alison Kelly. 2019. Business statistics: communicating with numbers, 3rd edition.
*	Statistics for Managers Using Microsoft Excel, 8th edition, by David M. Levine, David F. Stephan, and Kathryn A. Szabat.
