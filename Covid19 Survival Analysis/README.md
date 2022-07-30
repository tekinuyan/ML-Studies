!(https://github.com/tekinuyan/ML-Studies/blob/main/Covid19%20Survival%20Analysis/Assignment%20report_pictures/image001.png)
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

The time of report is constructed which the database contained 572679 geopositioned records from December 1, 2019 to 22th of February 2021.
Figure 2 shows the histogram of the covid-19 patiens by their age scale. The figure indicated that most of patiens got the virus around age of 36 to 38. This migth indicate the active young age class has mostly affacted by the virus.
![Figure 2](https://github.com/tekinuyan/ML-Studies/blob/main/Covid19%20Survival%20Analysis/Assignment%20report_pictures/image005.png)
