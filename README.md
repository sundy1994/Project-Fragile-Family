# Project: Early social and structural determinants of adolescent wellbeing
**Key Words:** R, Data Mining, EDA, Machine Learning, Model Fitting, Prediction

## Overview

Where there is a robust body of work about early predictors of adolescent outcomes, there are several gaps in this understanding. Firstly, although early child exposures are well described, less is known about the impact of social conditions prenatally or at time of birth. Secondly, many samples inadvertently overrepresent families with majority identities. This preferentially develops an evidence base that is not sensitive to needs of families who are disadvantaged across stratifications of race and class, among others. Third, most prior research relies on the report of one individual to measure social constructs at the family level. Especially as it concerns child development, mothers are most likely to provide this information and the paternal role is not as well described. Lastly, adolescent wellbeing is often assessed by constructs that are proximate to the individual, like peer relationships and health behaviors. Models that include early social development are not frequently combined with structural determinants that may act as unmeasured confounders. 

This study will fill these gaps using a unique application of a longitudinal dataset through the following aims: 1) develop a model of adolescent well-being from early social and structural health determinants and 2) determine which informant report is most predictive in this model.*


## Background

In late 2021 the US Surgeon General’s Advisory released a public health statement about the alarming assaults on youth wellbeing. Even before the COVID pandemic, 20% of US youth reported a mental health disorder, and only half received appropriate treatment. In the last two years, emergency room visits for psychiatric crises have doubled and youth have reduced access to friends, teachers and healthcare providers that can recognize early signs of mental health challenges. This report called for coordinated action for community support of adolescents, including increased attention in schools and healthcare systems. There is a need to identify mechanisms that underpin mental health symptoms. This is especially true for adolescents who disproportionally experience social conditions that predispose them to poor outcomes, like poverty, food insecurity and local environmental factors. While child mental health infrastructure has long been under resourced, there is a renewed urgency to understand how to prevent poor outcomes and promote resilience among at risk youth.

The global burden of childhood mental health symptoms is significant, non-communicable diseases are now the leading cause of disability. This longstanding public health problem has developed a large body of research linking early childhood exposures to longitudinal health outcomes. Specifically, adverse childhood experiences were identified in a landmark study as associated with almost every adult disease. These include neighborhood violence, food insecurity, interpersonal trauma, and other assaults to development. This study, and research that followed, had significant impact for healthcare systems that had not traditionally considered social structures as exposures for health outcomes. This work also unveiled the devastating cumulative impact of experiences that render children vulnerable to poor outcomes later in life. Of particular interest is the prenatal environment, which is a sensitive period for neurodevelopment that impacts both child and maternal health. These exposures are more prevalent, pervasive, and compounded by systemic racism for Black and Hispanic children, which can lead to longstanding sequela for these populations. Investments in child wellbeing are a health equity issue.


## Data Source

To answer these questions, we use data from the [Fragile Family and Child Wellbeing Study](https://fragilefamilies.princeton.edu/), which is a collaboration between Princeton and Columbia Universities. This study uses a stratified, multistage design of nearly 5,000 children born in US cities between 1998 and 2000. Sixteen cities were randomly selected of urban areas with populations over 200,000 and weighted to create a nationally representative panel. The study oversampled single parent households, racial-ethnic minority families and low-income caregivers at time of birth and is well positioned to investigate the mechanisms that contribute to disparities in child outcomes. Follow-up interviews were conducted at ages 1,3,5,9 and 15 and data collection is ongoing. Although there is some attrition, over 70% of families completed surveys at 15 years of age. Included in this panel was self-report from adolescents in addition to primary caregiver participation across many constructs, including health and wellbeing.

The original study sought to understand the nature of unmarried parents, longitudinal outcomes of children and how policies and environmental conditions impact young families. Each wave collected data on attitudes and expectations, childcare, behavioral development, demographics, education, employment, family ties, finances, health, housing, criminal legal systems, parenting, and romantic relationships. For this study, we use the unweighted sample for ease of analysis with the unrestricted data. Adolescent wellbeing is the selfreported outcome variable, constructed through 12 questions and adapted to a 100-point scale. Predictor variables were extracted from those related to social determinants of health and multiformat report of child social skills at birth and preschool age. We preferentially chose variables that are sensitive to evidence based social or health interventions, like neighborhood safety and food insecurity, and questions answered by two caregivers.


## Part I: Data Preparation and Exploratory Data Analysis

### Data Prep

The very first stepWe first select 12 columns based on domain knowledge that are related to children’s wellbeing. These items
were created by study researchers from the Adaptive Social Behaviora Inventory and the Social Skills Rating
System. Both are tools validated to assess adolescent social and psychological wellbeing. These scales ask
questions like: I am open and direct about what I want, I make friends easily, I am self-confidenc tin social
15
situations. For each column, a larger value stands for better self report of wellness. We sum them to create
a total score for wellbeing. Finally, we multiplied this score by 4.16 to create a variable scaled to 100 for
easier understanding.
We then selected more than 60 columns that are associated in the literature with positive child development
at birth and age 5. The total number of children in survey is 4800, so we dropped all columns with >2000
NAs. This is a reasonable decision because the survey has skip patters and not all families were asked these
questions. At year 15, the study had an attrition rate of less than 30% and questions were administered by
in-person research staff. We are confident the data is not biased based on missingness and therefore did not
conduct sensitivity analyses.
For the remainder of the variables, we used a package called “mice” to impute the values. We used
method=‘polr’ for ordinal categorical columns and method=‘pmm’ for continuous column. We checked the
percentage for each level, which was similar before and after imputing. This indicates that the imputations
did not change the distribution for each level, which is a good indicator for the following analyses.
We elected not to list all study questions used as variables in this project, however key constructs include
parental life satisfaction, presense of prenatal care, neighborhood saftey, and father’s investment in child
rearing at the time of birth. At age 5 we included variables associated with prosocial behavior (child gets
along with peers, child is nervous, child emotion regulation), participation in school events, recieving social
services like supplemental income, exposure to interpersonal violence and family sleep hygiene.
At this stage, we have two choices, leave the categorical as categorical or change it to numeric. We tried
both methods and found numeric is a better choice for modeling. If needed, we can change it to numeric
directly because the data frame has ordered categorical columns. This cleaned data was used in the study
to model adolescent wellbeing from early life predictors.
