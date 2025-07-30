# Applying Propensity Score Matching in R

## Description
[Propensity score matching](https://en.wikipedia.org/wiki/Propensity_score_matching) is a method employed across diverse fields of research to assess the causal impact of treatments, interventions, or exposures in observational studies. By equating covariates between treatment and control groups, it mitigates bias and confounding, thereby enabling the estimation of causal effects. 
In essence, propensity score matching constructs control and treatment groups that are highly comparable in terms of their individual characteristics. This process mitigates the influence of potential confounders, thus facilitating more accurate causal inferences.

## Use Cases
- **Education Policy Evaluation**: [Assessing the impact of educational interventions on student outcomes](https://telearn.hal.science/hal-00190019/document)
    This involves assessing the effects of educational interventions, such as curriculum changes, teaching methods, or educational programs, on student outcomes. Researchers use propensity score matching to compare the outcomes of students who received the intervention with those who did not, while controlling for potential confounding variables like socioeconomic status or prior academic achievement.

    **Example**: A study might examine the impact of a new teaching method on student performance in mathematics. By matching students who received the new method with similar students who did not, researchers can determine whether the intervention led to improvements in math scores.
- **Healthcare Interventions**: [Evaluating the effectiveness of medical treatments on patient outcomes](https://www.tandfonline.com/doi/pdf/10.1080/00273171.2011.568786)
This entails evaluating the effectiveness of medical treatments, interventions, or healthcare programs on patient outcomes. Propensity score matching allows researchers to compare the outcomes of patients who received a particular treatment with those who did not, while adjusting for factors like age, gender, and medical history.

    **Example**: Researchers might investigate the impact of a new medication on reducing symptoms of a chronic disease. By matching patients who received the medication with similar patients who did not, they can assess whether the medication led to improvements in symptom severity or overall health.

- **Labor Market Studies**: [Analyzing the effects of job training programs on employment outcomes](https://www.nber.org/system/files/working_papers/w6829/w6829.pdf)
This involves analyzing the effects of job training programs, employment services, or labor market policies on employment outcomes such as job retention, wage growth, or career advancement. Propensity score matching helps researchers compare the employment outcomes of individuals who participated in a program or intervention with those who did not, while controlling for factors like education level, work experience, and industry sector.

   **Example**: A study might examine the impact of a government-sponsored job training program on the employment rates of participants. By matching program participants with similar individuals who did not participate, researchers can assess whether the training program increased participants' likelihood of finding and maintaining employment.

- **At-Risk Youth: Mentoring Program Impact**: [examine the impact of a mentoring program on academic achievement outcomes among at-risk youth](https://books.google.de/books?hl=de&lr=&id=5Y_MAwAAQBAJ&oi=fnd&pg=PP1&dq=Propensity+Score+Analysis:+Statistical+Methods+and+Applications.+Sage+Publications.&ots=WY57gK_A9w&sig=h8usM9tYzJGz-RRhnca-iyx0cnA#v=onepage&q=Propensity%20Score%20Analysis%3A%20Statistical%20Methods%20and%20Applications.%20Sage%20Publications.&f=false)
This involves examining the impact of mentoring programs on academic achievement outcomes among at-risk youth, such as high school dropout rates, academic performance, or college enrollment. Propensity score matching allows researchers to compare the academic outcomes of youth who participated in a mentoring program with those who did not, while controlling for factors like socioeconomic background, parental involvement, and prior academic performance.

   **Example**: Researchers might investigate the impact of a mentoring program on reducing dropout rates among at-risk high school students. By matching program participants with similar students who did not receive mentoring, they can assess whether the program led to improvements in graduation rates or academic performance.

- **Academic Mobility of Researchers**: [Assessing the impact of academic mobility on scientific outcomes](https://doi.org/10.1016/j.joi.2022.101280)
This involves assessing the impact of academic mobility, such as international collaborations, sabbaticals, or research exchanges, on scientific outcomes such as publications, citations, or research productivity. Propensity score matching helps researchers compare the research outcomes of academics who engaged in mobility experiences with those who did not, while controlling for factors like disciplinary field, gender, age, international collaboration, and prior publication record.

   **Example**: A study might explore the impact of participating in an international research collaboration on an academic's publication output. By matching academics who engaged in collaborations with similar academics who did not, researchers can assess whether international mobility positively influences research productivity or citation rates.

## Input Data
This method can work with any dataset containing variables of interest, a treatment indicator, and covariates. Sample input data can be provided in CSV format with columns representing variables of interest (PPY, COPP, CPP), a treatment indicator (MOBILE), and covariates (REGION, MAIN_FIELD, INTERNATIONAL_COAUTHOR, GENDER, GDP_PC_ORIGIN, AGE). (mydata_sample.csv).
Here is a screenshot of sample input data:
![](sample_data.PNG)

## Output Data
The output includes standardized mean differences (SMD) for both unmatched and matched data, along with mean differences, t-values, and standard errors for the variables of interest.

By examining the SMD for unmatched and matched data under different covariances, we assess the effectiveness of the matching process in achieving balance between the treatment and control groups. A lower SMD indicates a smaller difference between the two groups. For instance, in this example, the SMD for the variable "AGE" is 0.34 for unmatched data and 0.03 for matched data. This suggests that the treatment group in the matched data is more similar to the control group compared to the unmatched data.
**SMD:**

![](output_SMD.PNG)

**Main difference:**
A mean difference of 3.04 for the variable CPP indicates that, on average, the treatment group's CPP value is 3.04 units higher than that of the control group.
![](output_mainDiff.PNG)

## Hardware Requirements
The method runs on a regular virtual machine provided by cloud computing company (2 x86 CPU core, 4 GB RAM, 40GB HDD). 

## Environment Setup
To run this method locally, ensure you have R (version  3.6.0 or higher) installed on your system.

Install the required R packages:
- Matching
- tableone

## How to Use
1. Download  ["mydata_sample.csv"](https://github.com/momenifi/methodHub/blob/main/academic_mobility_propensity_score/method/mydata_sample.csv), ["propensity_matching_functions.R"](https://github.com/momenifi/methodHub/blob/main/academic_mobility_propensity_score/method/propensity_matching_functions.R), and ["main_script.R"](https://github.com/momenifi/methodHub/blob/main/academic_mobility_propensity_score/method/main_script.R) in a folder.
2. Run the commands in "main_script.R"
    - Load the input dataset into R (data_sample) (lines 1 to 5)
    - Define the functions (line 8)
    - Define the treatment variable (treatment_var) and covariates (covariates)(lines 11 and 12)
    - Call the `perform_propensity_matching` function to conduct propensity score matching (line 15) with parameters data_sample, treatment_var, and covariates.  
      The output contains SMDs of unmatched/matched data (unmatched_smd in line 20)/matched_smd in line 21) and 
    - Define the variables of interest (vars_of_interest) (line 29) and Matched data (matched_data in line 24)
    - Call the `calculate_mean_diff` function to calculate mean differences for variables of interest (line 33) with parameteres matched_data, treatment_var, and vars_of_interest. The output gets the mean differences of vars_of_interest. 

## Technical Details
![](PS_explanation.jpg)
To elucidate, consider an example where two distinct groups of entities, represented by balls or ducks in our illustrations, are subjected to different conditions – treatment and control. The initial setup shows these entities with varying characteristics, such as size and color. The subsequent arrangement, either through sorting or linking, aims to pair entities with similar attributes across the treatment and control groups.

In the ball analogy, balls of similar size and color are matched between the treatment and control groups, creating pairs where each treated entity corresponds to a similar untreated entity. Similarly, in the duck analogy, ducks with comparable features, like color and size, are connected to their counterparts in the comparison group, ensuring a balanced representation.

It is used to construct control/treatment groups in scientific studies, in such a way that individuals in the control group are as similar as possible to individuals in the treatment group. 

## Contact Details
For questions or feedback, contact [fakhri.momeni@gesis.org](mailto:fakhri.momeni@gesis.org).
