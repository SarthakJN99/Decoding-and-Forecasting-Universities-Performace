# Decoding-and-Forecasting-Universities-Performance
Analyzing global university performance via Times Higher Education Rankings. Predictive models highlight critical predictors: teaching quality, research output, citations, industry income, and international outlook. Insights aid administrators in enhancing global standing, appealing to students, and attracting industry partners.

### Business Question
How can universities identify and leverage the key factors influencing their rankings to enhance their attractiveness to students and industry partners, and proactively anticipate their rankings to maintain or improve their competitive position?

### Business Case
In an increasingly competitive academic environment, universities are striving not only to attract the best students and faculty but also to secure funding and partnerships. A higher ranking can significantly enhance a university's attractiveness to potential students, faculty, and investors. Understanding the key factors that contribute to these rankings can help university administrators implement targeted improvements to enhance their global standing, thus attracting more talent and resources.

### Analytics Question
How can the development of predictive models that accurately quantify the impact of each predictor on university rankings and provide clear interpretability help university administrators make informed decisions to strategically improve their global standing?

Outcome Variable of Interest
The outcome variable of interest is the university's global ranking on an ordinal scale based on ranking methodology.

### Key Predictors
The dataset features key predictors critical for university analysis, including the number of students, student-to-staff ratio, proportion of international students, and the female to male ratio, as well as numeric scores for teaching quality, research output, citations, industry income, and international outlook.

### Data Set Description
This dataset, sourced from Kaggle but originally derived from the Times Higher Education World University Rankings, consists of 2,341 rows and 13 columns. It encompasses a broad spectrum of metrics related to universities globally, including rankings, names, locations, student demographics, and performance scores across various domains such as teaching, research, citations, industry income, and international outlook. The dataset is a mix of numerical and categorical data. Notably, the "Female
Ratio" column has 213 missing values, and crucial performance indicators like "Overall Score," "Teaching Score," "Research Score," etc., exhibit over 500 missing values. Addressing these gaps during data preprocessing will be essential, involving standardization, missing value handling, and data type verification to prepare the dataset for comprehensive analysis and predictive modeling.

### Descriptive Statistics of Key Variables
The dataset reveals significant variability in university metrics. With an average student body of 22,982 and a standard deviation of 27,462, sizes vary widely. The average student-to-staff ratio is 18.77, suggesting differences in potential student engagement across institutions. International students constitute an average of 10.65%, highlighting the global dimension of many universities. Gender distribution shows a slight female majority (53.39 females to 47.97 males per 100 students), indicating diverse student populations. Performance scores across teaching, research, and citations display considerable diversity, with averages of 27.16, 23.40, and 49.67, respectively, underscoring varied institutional strengths. Geographically, the United States leads with 171 universities in the dataset, followed by Japan (115), China (82), and India (65), showing a concentration of recognized institutions in these countries.

![image](https://github.com/kritika2004/-Decoding-and-Forecasting-Universities-Performace/assets/112310702/12ae5628-a061-4ba5-abf5-913f0815f68e)

#### Distribution of Key Variables
Our analysis began with examining the distribution of several key variables to understand the landscape of the universities included in our dataset. Histograms generated provided insightful visualizations into these distributions:

Student Numbers: Right-skewed, indicating most universities have smaller sizes with a few notable exceptions.
International Student Percentages: Also right-skewed, showing lower proportions of international students in most universities.
Overall Scores: Slightly right-skewed, suggesting a concentration of higher performance among fewer institutions.
Geographic Concentration: A notable concentration of ranked universities in the United States, indicating geographic disparities in educational excellence.

### Data Pre-Processing and Transformations
We enhanced the dataset for a more detailed analysis by:

Creating new columns for the number of males and females per 100 students from the existing male-to-female ratios.
Transforming the "International Student %" column from a string to a numeric format by removing the percentage sign.
Cleaning and converting columns with numerical data formatted as strings to numeric formats.
Removing special characters in the ranks and overall score columns for clarity.
Calculating and replacing ranges in columns with their average values to provide a consistent, singular value for each range.

### Correlation and Co-Variation Analysis
Our analysis highlights the crucial factors affecting university rankings, demonstrating significant correlations and variations. Key findings include:

A strong positive correlation between International Outlook and Industry Income Scores, indicating that globally engaged universities often enjoy higher industry income.
Negative correlations between university rank (numerically) and both teaching and research scores emphasize the importance of academic excellence for achieving higher rankings.
Geographical location significantly influences rankings, suggesting that a university's location, alongside its academic and financial performance, plays a pivotal role in its global standing.

![image](https://github.com/kritika2004/-Decoding-and-Forecasting-Universities-Performace/assets/112310702/06debb20-e373-401c-818f-0dcddec60ad7)

### Modeling Methods and Model Specifications
Initial Model Specification
We identified 'University Rank' as an ordinal outcome variable. The model includes numerical predictors such as 'Number of Students,' 'Staff-to-Student Ratio,' 'International Student Ratio,' 'Teaching Score,' and 'Research Score'. Preliminary regression results highlight 'Teaching Score,' 'Citations Score,' and other related scores as significant predictors.

## Initial OLS Results
Our regression model reveals significant determinants of university rankings. Holding all variables constant:

Teaching Score: Each point increase leads to a 6.259 improvement in rank.
Research Score: Each point increase enhances rankings by 2.307 ranks.
Citations Score: Each point increase improves rankings by 11.25 ranks.
Industry Income: Improves rankings by 2.812 ranks per point increase.
International Outlook: Improves rankings by 3.628 ranks per point increase.
Number of Students: A marginal 0.04225 unit increase per student.
Student-to-Staff Ratio: Negatively impacts rankings by 0.8548 units.
International Students: Slight positive association with rankings.
Statistically significant, the model explains a substantial 92.95% variance in rankings, asserting the robustness of these findings with high predictive power.

![image](https://github.com/kritika2004/-Decoding-and-Forecasting-Universities-Performace/assets/112310702/948f781b-9ffa-4810-ac5e-f1557b22a4dc)

## Assumption Tests
In our analysis, several OLS assumptions were not met:

The dependent variable Y, university rankings, was not continuous.
Errors were not normally distributed (Shapiro-Wilk test p-value: 1.628e-12).
Linearity assumption was violated for some predictors.
Constant variance assumption was violated (Breusch-Pagan test p-value < 2.2e-16).

![image](https://github.com/kritika2004/-Decoding-and-Forecasting-Universities-Performace/assets/112310702/2b1e3b02-080e-4793-b4d9-be5d6dc74386)
![image](https://github.com/kritika2004/-Decoding-and-Forecasting-Universities-Performace/assets/112310702/ecf4e7c9-d3fa-4e1a-9242-3ab0ce9fa35d)

### Model Candidates and Rationale
We initially adopted an Ordinary Least Squares (OLS) model but faced multiple assumption violations. We then implemented a Weighted Least Squares (WLS) model to address heteroscedasticity, but issues persisted. Consequently, we transitioned to a non-parametric Boosted Tree model, offering a flexible and robust alternative for our analysis.

![image](https://github.com/kritika2004/-Decoding-and-Forecasting-Universities-Performace/assets/112310702/8ea234ad-0149-42f2-ac03-bfbc6b6e5792)

## Cross Validation Testing
To assess the performance of all six predictive models, we employed 10-fold cross-validation using Root Mean Squared Error (RMSE) as the statistical metric for comparison:
![image](https://github.com/kritika2004/-Decoding-and-Forecasting-Universities-Performace/assets/112310702/cc688e42-3232-417e-97fc-a5fe86b319da)

### Analysis of Results
## OLS Model
The OLS model explains approximately 92.73% of the variability in university rankings, highlighting its effectiveness in capturing the dynamics that influence rankings. Quantitative predictors show:

Teaching Score: Decreases ranking by 6.25 units per point increase.
Research and Citation Scores: Decline ranking by 2.3 and 11.25 units, respectively.
Industry Income and International Outlook Scores: Positively affect rankings, decreasing them by 2.8 and 3.6 units per point increase.
Number of Students: Slight negative impact on rankings.
Student-to-Staff Ratio: Higher ratio negatively impacts rankings.
International Students: Slightly improve rankings.

## Reduced Boosted Tree Model
The reduced Boosted Tree model focuses on key predictors, achieving an impressive RMSE of 65.15. The model assigns the greatest importance to:

![image](https://github.com/kritika2004/-Decoding-and-Forecasting-Universities-Performace/assets/112310702/80e348c2-b5a4-401c-af46-0e408026cdc6)

Citations Score: Accounts for over 71% of the model's weighting.
Research Score: Comprises about 18% of the model's influence.
Teaching Score: Influences rankings by 7%.
International Outlook Score: Moderate impact with a 2% influence.
Number of Students and Industry Income Score: Minimal impacts.
Applying Reduced Boosted Tree to Full Dataset
The model demonstrates exceptional predictive performance, explaining approximately 98.63% of the variability in university rankings with a Prediction RMSE of 54.01333.

### Conclusion from the Analysis
The most influential factors affecting university rankings include Citations Score, Research Score, and Teaching Score. Higher scores lead to better (lower numerical) rankings. Additionally, Industry Income and International Outlook Scores positively influence rankings, suggesting that financial robustness and global engagement are valuable assets. Our analytical approach using OLS and Boosted Tree models provides predictive insights into the potential results of specific strategic

### Recommendations for Universities
Based on our analysis, we recommend the following three main strategies to enhance university rankings:

Enhance Research Output:

Finding: Research and Citation Scores significantly improve rankings.
Recommendation: Invest in research facilities and encourage faculty to publish in high-impact journals to boost research productivity and increase citation counts.
Improve Teaching Quality:

Finding: Teaching Score significantly decreases ranking units, indicating its critical impact.
Recommendation: Focus on improving teaching methodologies, faculty development, and regularly update curricula to reflect the latest industry trends and academic advancements.
Strengthen International Outlook:

Finding: International Outlook Score positively influences rankings.
Recommendation: Promote international collaborations and exchange programs to enhance global engagement, and increase the proportion of international students through targeted recruitment strategies.

