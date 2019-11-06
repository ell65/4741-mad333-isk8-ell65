# ORIE 4741 Project Midterm Report
## Elizabeth Lentine, Ian Konigsberg, Maximilian de Ledebur

Our group has spent significant time looking into the context of the data we are using for this project. Our Kaggle data reports on the physicochemical properties of red and white varieties of the Portuguese Vinho Verde ("veeng-yo vaird"), which translates to "green wine". This refers not to the color of the wine or the grapes but the fact that the wines are released a few short months (3-6) after harvest. The Vinho Verde region is the largest and one of the oldest winemaking regions in Portugal and is loved by many for its distinct qualities. Some of these include:


- Generally low alcohol content
- Refreshing, fruity flavor
- Great pairing with salad and seafood
- Lower prices per bottle, on average


Surface-level knowledge of oenology implies that red and white wines taste, smell, appear, and are assessed quite differently because of the fundamental differences in the techniques used in making them. Namely, red wines are fermented with the seeds and skins still on the grapes. More information on the differences between these two broad categories can be found [here](https://winefolly.com/tutorial/red-wine-vs-white-wine-the-real-differences/ ).

Because of these important differences, we believed it made the most sense to separate data into two distinct subsets of red and white wines. Additionally, given the considerably more entries corresponding to white wines (most wines from this region are white) we felt it was important to look at them separately to begin to understand the relationships between our features without throwing off our results due to a heavier weight towards the good predictors for the white wines.
<br><br>

So far we have run a few regressions on our data to try to predict the quality of each wine. The assignment for quality in the original data was given based on the median value of three oenologists' rating of the wine on a scale from 1 to 10. We quickly noticed that ratings below 4 and above 7 are quite uncommon in our data.
<br><br>

Our dataset contained very little missing data. Of the 6,497 wine examples, there were only 27 examples that were missing at least one featurespace value. We also noticed that all of these 27 examples were white wines. Because we had a total of 4,897 white wines, we decided to simply remove the 27 white wines of incomplete cases. This left us with 1,593 red wines and 4,870 white wines of complete cases.  Our featurespace includes 12 features which are all physicochemical properties. Below, we describe the feautures in the featurespace for both red wines and white wines.
<br><br>


WHITE: <br>
![](https://github.com/ell65/4741-mad333-isk8-ell65/blob/master/Whites.PNG)
<br>
RED: <br>
![](https://github.com/ell65/4741-mad333-isk8-ell65/blob/master/Reds.PNG)
<br>

How will we prevent overfitting? <br>
We plan on identifying the most important features in the featurespace and regressing on only these important features.


<br>

In fact, when we cleaned our data, we found the following results corresponding to ratings of [1, 2, 3, 4, 5, 6, 7, 8, 9]. 
<br><br>

total reds: 1593 wines [0, 0, 10, 52, 680, 634, 199, 18, 0]

total whites: 4870 wines [0, 0, 20, 162, 1448, 2186, 875, 174, 5]

total: 6497 wines [0, 0, 30, 216, 2138, 2836, 1079, 193, 5]

<br>

Represented as a histogram, the distribution of the ratings in our data looks like:

![](https://github.com/ell65/4741-mad333-isk8-ell65/blob/master/rwhist.jpg)

<br>



After running an initial linear regression on the entire feature space, we have the following results for error:
<br><br>

 "White MSE, test"          0.594466
 
 "Red MSE, test"            0.419574
 
 "White MSE, train"         0.563472
 
 "Red MSE, train"           0.415883
 <br><br>
 "White Mean absolute error, test"   0.771016
 
 "Red Mean absolute error, test"     0.647745
 
 "White Mean absolute error, train"  0.750648
 
 "Red Mean absolute error, train"    0.64489 
 
 <br><br>
 
Where is our project headed? <br>
Our main goal for the forseeable future will be to build a model that can properly categorize wines into one of these three categories: low quality, average quality and high quality. We think a good way to partition our data will be: <br>
quality rating < 4 ==> low quality , quality rating > 7 ===> high quality, otherwise ==> average quality.
<br>
The two regression analyses that we performed above were simple least squares models with no regularizer term. The output variable, y, in the above regressions was the quality of wine on a scale of 1 to 10, NOT the categories "low, average, high." Therefore, we plan on drastically changing the regressions we performed above to properly categorize the wines. We think a good model to fit will be an ordinal regression. We believe that an ordinal regression will be significantly better at classifying the wines than a linear regression model after feature transformation of our ordinal data. 
<br>
We will also strongly consider the use of a loss function other than least squares. The reason for this is that we believe the greatest use of our model will be to confidently identify good or bad wines and make recommendations about the production of those wines. In other words, we want our loss function to care a lot about misclassifying an average wine as a good or a bad wine (because then we will make a recommendation) and to care less about misclassifying a good or bad wine as an average wine (because then we will not make a recommendation). We think a good loss function to capture this will be hinge loss, although we plan on exploring other options. Furthermore, we think it will be necessary to include a regularizer term to avoid overfitting our data. 
