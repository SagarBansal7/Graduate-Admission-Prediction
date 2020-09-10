# Graduate Admission Prediction
## Graduate Coure: Managerial Statistics

### Introduction 

This was a team project from a course on Managerial Statistics where we evaluated several parameters which are considered important during the application for Masters Programs. When we went through the process of preparing, applying, and collecting required documents for the admission, we were less informed about how and in what percentage the individual documents will contribute to our selection. Here in this study, we will try to find interesting pattern on how different features relate to chances of admit. The results will surely reveal something insightful. In addition, we have emphasized on making this report comprehensible for non-statistical/technical audiences so the results can then be used by the potential students in strengthening their profile accordingly.

### Data Characterisitcs

We are looking at the university data and different admission scores, how it’s correlated to university ranks and if there is a way to predict the admission based on those scores. The hypothesis question we would like to answer is whether the score will be significantly higher for higher ranking university. The data has 400 different results that contain GRE score, TOEFL score, University Rating, SOP, LOR, CGPA, Research (if there’s a research done) and chance of admission based on those scores. 

#### Data Summary

![GAP - Pic 1](https://user-images.githubusercontent.com/37155988/92798790-414b3500-f381-11ea-9247-67855ff1b972.png)

Here, we can see that the dataset is very rich with useful information. It contains all the major contributing factors which result in an admit or rejection. We have different types of data such as qualitative (ordinal, nominal) and quantitative with different ranges. As we observed, the GRE score has a minimum possible value of 260 and maximum possible value of 340. Similarly, TOEFL score can go as low as 0 and as high as 120. Both of them are integer type i.e., the values are non-decimal. In contrast, the SOP and LOR strength variables are decimal variables. They can go up to one decimal value. Both of them ranges from 1 to 5. At last, CGPA can have up to two decimal values, ranging from 0 to 10. (Note: Although the data may not contain the lowest values for all the quantitative variables, the variables can have those values if we add more data in future).

For qualitative variable, we have university rating and Research experience. Even though the university rating looks like a quantitative variable, on close inspection we can observe that they have an intrinsic order in them, Also, the numbers 1 to 5 do not make much sense in terms of numeric/arithmetic properties i.e., we could have used A to E instead. The properties that matter is that they are distinct and have an order property. 

In the next sections, we will start with the descriptive evaluation and visualization of data to get a better understanding of it. After that, we will construct a methodology suitable to the data we have. This will help us in focusing on important features critical to increase the chance of admit and make recommendation accordingly. We will then provide a conclusion from the results and corresponding interpretations we get


