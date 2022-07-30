![Figure 0](https://github.com/tekinuyan/ML-Studies/blob/main/Covid19%20Survival%20Analysis/Assignment%20report_pictures/image001.png#center)
# Covid19 Survival Analysis

This report is covid-19 survival analysis. The goal of the study is to analize what are the important factors for Covid-19 to survive after it has been diagnosed. To aid the analysis and tracking of the COVID-19 epidemic we
collected and curated individual-level data from national, provincial, and municipal health reports, as well as additional information from online reports.



## Data Records and Description
The given dataset is extracted via fallowing features which are assumed to be most related ones on the covid19 survival analysis. The detailed explanation of the features are below (See Figure 1):


![Figure 1](https://github.com/tekinuyan/ML-Studies/blob/main/Covid19%20Survival%20Analysis/Assignment%20report_pictures/image003.png)

age - Age of the case reported in years. When not reported, N/A is used. Age ranges are recorded as start_age-end_age e.g. 50–59.

sex - Sex of the case. When not reported, N/A is used.

date_confirmation - Date when the reported case was confirmed as having COVID-19 using rt-PCR. Confirmation accuracy is contingent on the data source used. Specific dates are reported as DD.MM.YYYY.

chronic_disease_binary - 0 represents a case that was reported to have no chronic disease and 1 represents cases that reported a chronic disease.

date_death_or_discharge - Reported date of death or discharge in DD.MM.YYYY format.

outcome - Patients outcome, as either “died” or “discharged” from hospital.
## Exploratory Data Analysis
The time of report is constructed which the database contained 572679 geopositioned records from December 1, 2019 to 22th of February 2021.
Figure 2 shows the histogram of the covid-19 patiens by their age scale. The figure indicated that most of patiens got the virus around age of 36 to 38. This migth indicate the active young age class has mostly affacted by the virus.

![Figure 2](https://github.com/tekinuyan/ML-Studies/blob/main/Covid19%20Survival%20Analysis/Assignment%20report_pictures/image005.png)

Figure 2 Histogram of Covid-19 Patients


Figure 3 indicates that the dead of covid-19 patients are mostly belong to the old age male group that are above 65 years old. 

![Figure 3](https://github.com/tekinuyan/ML-Studies/blob/main/Covid19%20Survival%20Analysis/Assignment%20report_pictures/image007.png#center)
![Figure 3](https://github.com/tekinuyan/ML-Studies/blob/main/Covid19%20Survival%20Analysis/Assignment%20report_pictures/image009.png#center)

Figure 4. shows the analysis specification for this example. The Kaplan-Meier procedure estimates the instantaneous risk of death at any particular time as the ratio of the number who died at that time to the number in the current risk set, which is defined to be the set of individuals currently at risk of experiencing the outcome of interest.


![Figure 4](https://github.com/tekinuyan/ML-Studies/blob/main/Covid19%20Survival%20Analysis/Assignment%20report_pictures/image010.png)

Figure 4.  KM Survival Curve

Figure 5 indicates that the difference in survival between gender groups was statistically significant. The null hypothesis is false , meaning we continue believing that survival rate for different age groups differ.

![Figure 5](https://github.com/tekinuyan/ML-Studies/blob/main/Covid19%20Survival%20Analysis/Assignment%20report_pictures/image012.png)

Figure 5. KM curve over three age groups. young: age < 40; middle: 40 - 65 and old: > age 65

Figure 6. indicates that the log-rank test provided a p-value of 0.005 is smaller than significant level 0.01 indicating that the difference in survival between gender groups was statistically significant. Meaning we continue believing that survival rate for different age groups differ as the previous Figure 3. show the male deaths cause by Covid-19 virus are more than females.


![Figure 6](https://github.com/tekinuyan/ML-Studies/blob/main/Covid19%20Survival%20Analysis/Assignment%20report_pictures/image016.png)

![Figure 6](https://github.com/tekinuyan/ML-Studies/blob/main/Covid19%20Survival%20Analysis/Assignment%20report_pictures/image014.png)

Figure 6.  KM curve for female and male gender and log-rank test.

## Conclusion
Overall, 

•	The y-axis represents the probability a patient is still alive after t days, where 𝑡 days is on the x-axis.

•	About 99% of patients survived more than 400 days.

•	 Age group plays significant role in patient survival time, over 99% of young age patients are still alive if after 400 days. The Covid-19 patient survival chance decreases dramatically when patients are old. 

![Figure 7](https://github.com/tekinuyan/ML-Studies/blob/main/Covid19%20Survival%20Analysis/Assignment%20report_pictures/image018.png)
![Figure 7](https://github.com/tekinuyan/ML-Studies/blob/main/Covid19%20Survival%20Analysis/Assignment%20report_pictures/image020.png)

Figure 7. of Cox model coefficients of all Covariates

In Figure 7. the exponentiated coefficients(exp(coef)) indicates Hazard ratios. The key output is this is interpreted as the scaling of hazard risk for each additional unit of the variable, 1.00 being neutral, meaning a patient is less likely to die. Briefly, Cox regression indicated that being male will increase the baseline hazard by a factor of exp(0.01)=1.01 - about 1%. On the other hand having a chronical disease will increase the dead event significantly as 81%. Contrary, being in young age reduces the hazard by a factor of 0.59, or 41%. Being young is associated with good prognostic. Males in old age groups having a chronical disease would be the most vulnerable against covid19 virus.

![Figure 8](https://github.com/tekinuyan/ML-Studies/blob/main/Covid19%20Survival%20Analysis/Assignment%20report_pictures/image022.png)

![Figure 9](https://github.com/tekinuyan/ML-Studies/blob/main/Covid19%20Survival%20Analysis/Assignment%20report_pictures/image024.jpg)
