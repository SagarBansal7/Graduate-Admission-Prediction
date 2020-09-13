# Graduate Admission Prediction
## Graduate Coure: Managerial Statistics

### Introduction 

This was a team project from a course on Managerial Statistics where we evaluated several parameters which are considered important during the application for Masters Programs. When we went through the process of preparing, applying, and collecting required documents for the admission, we were less informed about how and in what percentage the individual documents will contribute to our selection. Here in this study, we will try to find interesting pattern on how different features relate to chances of admit. The results will surely reveal something insightful. In addition, we have emphasized on making this report comprehensible for non-statistical/technical audiences so the results can then be used by the potential students in strengthening their profile accordingly.

### Data Characterisitcs

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

Here, we can see that the dataset is very rich with useful information. It contains all the major contributing factors which result in an admit or rejection. We have different types of data such as qualitative (ordinal, nominal) and quantitative with different ranges. As we observed, the GRE score has a minimum possible value of 260 and maximum possible value of 340. Similarly, TOEFL score can go as low as 0 and as high as 120. Both of them are integer type i.e., the values are non-decimal. In contrast, the SOP and LOR strength variables are decimal variables. They can go up to one decimal value. Both of them ranges from 1 to 5. At last, CGPA can have up to two decimal values, ranging from 0 to 10. (Note: Although the data may not contain the lowest values for all the quantitative variables, the variables can have those values if we add more data in future).

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

Following table 3 showing values at the 90th percentile for each feature. For universities with rating “3”, it suggests that the 325.6 is greater than the 90 percent of student’s GRE scores. Similarly, 112 for TOEFL score, 4 for SOP Strength, 4.5 for LOR strength, 9.04 for CGPA and 1 for Research.  For the five rated universities, the values are significantly high. It is 338.9 for GRE score, 119 for TOEFL score, 5 for SOP Strength, 5 for LOR strength, 9.778 for CGPA and 1 for Research.  It is clear that scores have to be higher for higher ranked universities. 

Note that, 90th percentile for 3 and 5 rated universities is different than having the 90% chance of admission for 3 and 5 rated universities. The latter is the value of our target variable as “Chances of Admit” tells us the percentage. Whereas 90th percentile is the calculation done on all of the values and getting the one having 90% of the values below it.

#### Table 3: Student profiles at 90th percentile of chance of admit for 3 and 5 rated universities 

![Table 3](https://user-images.githubusercontent.com/37155988/93022839-35e24e80-f5b9-11ea-8094-c18d11bcfa16.png)

#### Graph 2: Average TOEFL scores and average GRE scores by university rank

<img src="https://user-images.githubusercontent.com/37155988/93022773-edc32c00-f5b8-11ea-9de6-3bb249f25306.png" width="500">

The Graph 1 above displaying two admission measures TOEFL and GRE exams from the 400 samples that shows that there is a definite increase of needed scores to be admitted to a higher ranked univers  e School. We based this off of our experience when applying to different Grad Schools. TOEFL is usually only required for Undergraduate admissions which is not the case of our dataset. It makes sense to exclude TOEFL score as we will see later on in our methodology section that it proved not to be a useful predictor of our model. Moreover, the variations in the TOEFL score distorts some of our model assumptions such as the assumption of the constant variance.

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

These intervals will help us in inferring the possible mean value range for different samples we evaluate for the same population. In addition, we get an important insight about our target variable “Chance of Admit”. We noted that on average the mean of chance of admit varies between 70.63% and 73.37%. This is very important because the range is **significantly far from 50%** i.e., many more than half of the students have a good chance to get an admit from the university they apply and they actually get it. This information can also be used by the future applicants as a motivation to apply and expect to get an admit.

**b) Hypothesis Testing/ANOVA**

Early on in our introduction to the data set we mentioned about the hypothesis to establish that higher university ranking, the higher the chance of admit. Now we will do a hypothesis test to establish the fact that there exists a relationship between University Ranking and Chance of Admit using one way ANOVA.  

* For simplification, going forward, we will call University Ranking as UR, Chance of Admit as CoA! 

For Hypothesis Testing, our first step is to create Null & Alternative hypothesis. 

H0 : μ1 = μ2 (There exists no relation whatsoever b/w UR and CoA)
Ha : μ1 is not equal to μ2 (There exists a relationship b/w UR and CoA)
where μ1 = Average of University Ranking
and μ2 = Average of Chances of Admit

For this hypothesis, we will use α = 0.05 = Significance Value and now, we will check which of the hypothesis is true using ANOVA! We will be doing an ANOVA test between University Rating and Chance of Admit.  

#### Table 7: Summary Statistics of Graduate Admission
![Table 7 a](https://user-images.githubusercontent.com/37155988/93023421-dede7880-f5bc-11ea-8edd-ea0f5016ec80.png)

![Table 7 b](https://user-images.githubusercontent.com/37155988/93023426-e867e080-f5bc-11ea-80a6-c437586bd9d8.png)

From the above ANOVA analysis, we can observe that p-value = 1.2099E-198.

Since our p-value is less than α, we will reject the null hypothesis and can call out that our result is statically significant. 

Now, let’s go back a few steps and recall, what did we say in our Alternate Hypothesis (Ha), our alternate hypothesis calls out that μ1 is not equal to μ2 and hence, there exists a relation between University Ranking and Chance of Admit. 

From the above analysis of variance test (ANOVA), we can conclude that the higher the university ranking, the higher the chances of admit.  

**c) Regression Analysis**

We had to do some outside research for what regression method would be best and we decided to go with regression through the origin with no Beta-0 intercept. This is because it makes sense contextually that there should be no intercept for the chance of admit because if a student has 0 scores for the variables analyzed above his/her chance of admit would be zero. Moreover, after exploring the data and the relation between variables we found that students that are applying to higher ranked universities need higher scores for GRE. Therefore, we decided to try out an interaction term using University Rating with different variables. The interaction term between GRE Scores\*University Rating appeared to be the most significant. Below is the model initiated using R-studio.

 model = lm (`Chance of Admit` ~ 0 +`GRE Score`*University Rating + CGPA + LOR+ Research)
 
