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
```
<p align="center">

#### Table 1: Summary Statistics of Graduate Admission

![Image 2](https://user-images.githubusercontent.com/37155988/92817880-11a62800-f395-11ea-86c0-d340afc44165.png)

</p>
```
Since the average university rank is 3 and the university rank 3 shows the highest frequency compared to other university ranks shown in the figure below. We decided to look for the average scores’ person needs to have a higher chance (90%) of being admitted and what are the lower scores with less chances of being admitted (36% chance). We also looked at the higher rated university scores, what is needed to be admitted to such university and what scores are required. The table below shows that with 90% chance of admission the scores are the same for university that is ranked 3 and 5. We noticed that the chance of admission is much less when there is no research submitted for admission. It is also showing that the highest chance of admission (97%) for the highest ranked university (5 out of 5) requires the highest scores for everything. In other words, whoever receives the highest scores plus submits a research work has almost 97% chance of being admitted. 
