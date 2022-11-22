---
layout: distill
title: Digital health technologies and machine learning augment patient reported outcomes to remotely characterise rheumatoid arthritis
description: Our new pre-print is now available online! 🥳 Here I will summarise our main findings and the impact of our work in the 14-day observational study in RA, known as weaRAble-PRO. 
tags: [digital health]  
categories: pre-print summary
date: 2022-11-22
draft: False
preview: assets/img/RA_explainer.png
posts:
    share: [twitter, linkedin]

authors:
  - name: Andrew P. Creagh*
    url: "https://www.andrewcreagh.com"
    affiliations:
      name: IBME, BDI,<br>University of Oxford; <br> GSK, UK.
  - name: Valentin Hamy
    url: "https://uk.linkedin.com/in/valentinhamy"
    affiliations:
      name: GSK, UK.
  - name: Hang Yuan
    url: "https://hangyuan.xyz/"
    affiliations:
      name:  BDI, University of Oxford.
  - name: Gert Mertes
    url: "https://www.bdi.ox.ac.uk/Team/gert-mertes"
    affiliations:
      name: IBME, BDI,<br>University of Oxford.
  - name: Ryan Tomlinson
    url: ""
    affiliations:
      name: GSK, US.
  - name: Wen-Hung Chen
    url: ""
    affiliations:
      name: GSK, US.
  - name: Rachel Williams
    url: ""
    affiliations:
      name: GSK, US.
  - name: Christopher Llop
    url: "https://www.analysisgroup.com/experts-and-consultants/vice-presidents/christopher-llop/"
    affiliations:
      name: Analysis Group, US.
  - name: Christopher Yee
    url: ""
    affiliations:
      name: Analysis Group, US.
  - name: Mei Sheng Duh
    url: "https://www.analysisgroup.com/experts-and-consultants/managing-principals/mei-sheng-duh/"
    affiliations:
      name: Analysis Group, US.
  - name: Aiden Doherty
    url: "https://www.ndph.ox.ac.uk/team/aiden-doherty"
    affiliations:
      name: BDI, NDPH,<br>University of Oxford.
  - name: Luis Garcia-Gancedo
    url: "https://uk.linkedin.com/in/luisgarciagancedo"
    affiliations:
      name: GSK, UK.
  - name: David A. Clifton
    url: "https://ibme.ox.ac.uk/people/david-clifton/"
    affiliations:
      name: IBME, University of Oxford.
bibliography: 2022-11-22-WeaRAble-PRO.bib


# Optionally, you can add a table of contents to your post.
# NOTES:
#   - make sure that TOC names match the actual section names
#     for hyperlinks within the post to work correctly.
#   - we may want to automate TOC generation in the future using
#     jekyll-toc plugin (https://github.com/toshimaru/jekyll-toc).
toc:
  - name: Summary
  - name: Background
  - subsections: 
    - name: Study Objectives
  - name: Dataset
  - name: Methods
  - subsections: 
    - name: Self-supervised learning (SSL) model
    - name: Extraction sensor-based outcomes
    - name: Machine learning estimation of RA 
  - name: Key Findings
  - name: Impact
  - name: Code Availability
  - name: References

# Below is an example of injecting additional post-specific styles.
# If you use this post as a template, delete this _styles block.
_styles: >
  .fake-img {
    background: #ffffff;
    border: 1px solid rgba(0, 0, 0, 0.1);
    box-shadow: 0 0px 4px rgba(0, 0, 0, 0.1);
    margin-bottom: 12px;
  }
  .fake-img p {
    font-family: monospace;
    color: white;
    text-align: left;
    margin: 12px 0;
    text-align: left;
    font-size: 14px;
  }

---

<!---------------------------------------------------------------------------------------------------------->
<!----------------------------------------- Abstract ------------------------------------------------------->

  <p style="text-align: center;"> <strong>Manucript Abstract</strong></p>

  <p align="justify">
  Digital measures of health status captured during daily life could greatly augment current in-clinic assessments for rheumatoid
  arthritis (RA) which will enable better assessment of disease progression and impact. This work presents results from weaRAble-PRO,
  a 14-day observational study, which aimed to investigate how digital health technologies (DHT), such as smartphones and
  wearables, could augment patient reported outcomes (PRO) to identify RA status and severity in a study of 30 moderate-to-severe
  RA patients, compared to 30 matched healthy controls (HC). Sensor-based measures of health status, mobility, dexterity,
  fatigue, and other RA specific symptoms were extracted from daily iPhone guided tests (GT), as well as actigraphy and heart
  rate sensor data, which was passively recorded from patients’ Apple smartwatch continuously over the study duration. We
  subsequently developed a machine learning (ML) framework to distinguish RA status and to estimate RA severity. It was found
  that daily wearable sensor-outcomes robustly distinguished RA from HC participants (F1, 0.807). Furthermore, by day 7 of the
  study (half-way), a sufficient volume of data had been collected to reliably identify the characteristics of RA participants. In
  addition, we observed that the detection of RA severity levels could be improved by augmenting standard patient reported
  outcomes with sensor-based features (F1, 0.833) in comparison to using PRO assessments alone (F1, 0.759) and that the
  combination of modalities could reliability measure continuous RA severity, as determined by the clinician-assessed RAPID-3
  score at baseline (r<sup>2</sup>, 0.692; RMSE, 1.33). The ability to measure the impact of disease on daily life—through objective
  and remote digital outcomes that are meaningful to patients—paves the way forward to enable the development of more
  patient-centric and personalised measurements for use in RA clinical trials.
  </p>


[<img src="https://raw.githubusercontent.com/FortAwesome/Font-Awesome/6.x/svgs/regular/window-maximize.svg" width="50" height="50">](https://www.medrxiv.org/content/10.1101/2022.11.18.22282305v1)
[<img src="https://raw.githubusercontent.com/FortAwesome/Font-Awesome/6.x/svgs/regular/file-pdf.svg" width="50" height="50">](/assets/pdf/Creagh2022_DHTAugmentPROinRA.pdf)
[<img src="https://raw.githubusercontent.com/FortAwesome/Font-Awesome/6.x/svgs/brands/github.svg" width="50" height="50">](https://github.com/OxWearables/ssl-wearables)

<b>Note:</b> This article is best viewed in 'light mode'! <img src="https://raw.githubusercontent.com/FortAwesome/Font-Awesome/6.x/svgs/regular/sun.svg" width="20" height="20"/>

<!--------------------------------------- End abstract ----------------------------------------------------->
<!---------------------------------------------------------------------------------------------------------->

## Summary
In recent years, the emergence of consumer digital health technologies (DHT) has opened the possibility of developing rich, continuous, and objective measures of rheumatoid arthritis (RA) disease that can be administered remotely outside of standard clinical settings. In this work, we investigated how DHT, in this case a wrist-worn Apple smartwatch device and a bespoke iPhone mobile app., could augment patient reported outcomes (PRO) to characterise the impact of RA on the daily life of 30 moderate-to-severe RA patients, compared to 30 matched healthy controls (HC). This observational study, known as “weaRAble-PRO” (GSK212295) and collected in collaboration with industrial partners GSK plc., demonstrated how smartphone and smartwatch sensor-outcomes could characterise meaningful aspects of RA impairment and physical function impacting daily life.

From these remotely collected wearable sensor-outcomes (such as from the iPhone and Apple smartwatch) we establish how ML can help characterise the impact of RA on daily life. For example, modelling of objective sensor-outcomes could identify RA participants from healthy controls---with improved performance when combining the sensor-data from both devices---and augmented standard patient (self-) reported outcomes to remotely estimate RA severity, as measured by the in-clinic RAPID-3 assessment of RA. To the best of our knowledge, these results offer the first comprehensive evaluation and insight how remote monitoring outcomes in daily life can can characterise RA status and severity, which represents an important first step towards the development of more sensitive and patient-centric measurements for use in RA clinical trials and real-world studies.

<img src="/assets/img/RA_explainer.png" width="700"/><br>
<p align="justify"><b>The potential of digital health technologies (DHT) to monitor RA.</b> DHT can be administered remotely outside of standard clinical settings to better measure how disease can impact a person’s daily life. These objective and more frequently collected measures&mdash;known as <em>digital biomarkers</em>&mdash;offer huge potential  to augment standard in-clinic assessments for RA, ultimately to develop more sensitive and patient-centric measurements for use in RA clinical trials and real-world studies. 
</p>


## Background
We know that rheumatoid arthritis (RA) patients follow quite subtle and unpredictable disease courses, patient-to-patient, and have a progressive
decline in physical function and quality of life and over time---this often leads to disability and difficulty to perform many tasks
of daily life (think about going shopping, getting dressed, taking your dog on a walk, or caring for your grandchildren). Currently, the gold-standard methods of measuring the impact of RA on daily life rely on infrequent clinical visits that may often occur every 3--4 months, with assessments depending on a combination of subjective clinician-determined scores <d-cite key="banderas2017development"></d-cite> and patient-reported outcomes (PROs) (i.e., usually in the form of questionnaires that patients fill out) <d-cite key="lubeck2004patient"></d-cite>. Given that people with RA need to manage their daily life based on the fluctuations of their symptoms <d-cite key="flurey2014juggle"></d-cite>, it would be beneficial to develop <em>meaningful</em> metrics to patients that can objectively measure the impact of disease on <em>their</em> daily life, remotely over a continuous period, rather than restricting assessments to only intermittent physician visits.

The concept behind our work is to use digital health technologies (DHT) (typically these are consumer-grade mobile apps., smartphones, and wearable devices <d-cite key="taylor2020outcome"></d-cite>) to objectively measure participants’ symptoms during daily life <d-cite key="piga2017telemedicine"></d-cite>. DHTs have already shown great promise to increase study engagement, improve patient convenience, streamline collection of PROs, and potentially generate more frequent and accurate data that can characterise disease <d-cite key="munos2016mobile"></d-cite><d-cite key="pratap2020evaluating"></d-cite><d-cite key="lipsmeier2022reliability"></d-cite><d-cite key="creagh2020smartphone"></d-cite>. In our previous work, we have also shown specifically how DHT can measure RA symptoms and functions, such as range of motion (ROM) and gait-specific metrics during prescribed <em>"active"</em> assessments<d-cite key="crouthamel2018using"></d-cite><d-cite key="hamy2020developing"></d-cite>. Other studies have shown how <em>"passive"</em> wearable actigraphy sensor-outcome measurements capture differences in RA physical activity (PA) in daily life, compared to healthy controls (HC) <d-cite key="prioreschi2013clinical"></d-cite>, as well as to detect flaring of RA symptoms <d-cite key="gossec2019detection"></d-cite>.

### Study Objectives 
Unfortunately, there remains a lack of sufficient evidence for how DHT can provide objective insights into the impact of therapies for RA. Particularly, the benefit of sensor-outcomes generated from prescribed active assessments compared with passive monitoring has not yet been explored together. Furthermore, while digitised PROs enhance patients' ability to frequently record disease activity<d-cite key="el2016toward"></d-cite>, it remains unclear how objective sensor-outcomes could provide additional insight beyond PROs to characterise the impact of RA on daily life. The sensitivity of DHT to measure RA symptoms, such as the volume of remote data required and the number of sensor-outcome measurements needed, also needs to be determined. Finally, the application of DHT sensor-outcomes to monitor RA daily life remains to be validated against standard in-clinic administered assessments of RA impact<d-cite key="coravos2019developing"></d-cite>.

<img src="/assets/img/wearable-pro-study.png" width="700"/><br>
<p align="justify"><b>Illustration detailing the objectives of this study</b>. The weaRAble-PRO 14-day trial aimed to investigate how
digital health technologies (DHT)&mdash;a wrist-worn Apple smartwatch and an iPhone device, with bespoke mobile apps.&mdash;could augment patient reported outcomes (PRO) to characterise the impact of rheumatoid arthritis (RA) on the daily life of 30 moderate-to-severe RA patients, compared to 30 matched healthy controls (HC).</p>

## Dataset
The GSK weaRAble-PRO study (GSK212295)<d-footnote>The full GSK study title is "Novel Digital Technologies for the Assessment of Objective Measures and Patient Reported Outcomes in Rheumatoid Arthritis Patients: A Pilot Study Using a Wrist-Worn Device and Bespoke Mobile App. (212295, weaRAble-PRO)".</d-footnote> was a 14-day observational study with 30 RA patients and 30 matched Healthy Controls (HCs) to investigate how digital health technologies could objectively measure the impact of RA on participants’ daily lives. Remotely collected sensor data was obtained from a wrist-worn Apple Watch---enabling continuous 14-day passive monitoring---and an iPhone, integrated with a bespoke mobile app., which prescribed daily guided assessments.  Sensor-based measures of physical function, mobility, dexterity, and other RA specific symptoms were extracted from daily prescribed (active) iPhone guided tests, such as a wrist-range of motion exercise, a walking assessment, a nine-hole peg test, as well as two pose transition-based mobility exercises, lie-to-stand (LTS) and sit-to-stand (STS). In addition, continuous (passive) actigraphy was recorded from participants’ Apple smartwatch over the study duration in order to characterise daily activity patterns and sleep. Patient-reported outcomes (PRO), most often self-report questionnaires, were also administered to assess disease activity, symptoms, and health status and quality of life from the participants’ perspective. 

<b>Note</b>: this work details a sub-study of weaRAble-PRO; trial design, feasibility, participant adherence, and other primary related study outcomes will be published as part of a complementary manuscript.

## Methods
### Self-supervised learning (SSL) model

The foundation of this work employs the latest advances in machine learning (ML), such as our self-supervised learning (SSL) methodology, which enabled a robust estimate of participants’ daily activity to be generated over the 14-day study. Building on our previously released work by Yuan et al.<d-cite key="yuan2022self"></d-cite>, in this study we demonstrated the first deployment of our deep convolutional neural network (DCNN)--which was pre-trained using SSL on 700,000 person days in the publicly available UK Biobank (significantly the largest of its kind to date)---in a clinical study. Our SSL DCNN model helped transform continuously collected Apple smartwatch sensor data to meaningful outcomes characterising the daily life for RA participants, such as the time spent active, sleeping, and other RA-specific measures, such as morning stiffness. 

In this study, we build upon our previous work by adding a temporal dependency to the DCNN (SSL) through a hidden markov model (HMM), which
was appended to obtain a more accurate sequence of predicted activities over the continuous study period. It was found that the DCNN (SSL) + HMM improved activity estimation in Capture-24 ($\kappa$, 0.862 ± 0.088; F1, 0.815 ± 0.103) as compared to a baseline random forest (RF) + HMM approach ($\kappa$, 0.813 ± 0.108; F1, 0.775 ± 0.117) <d-cite key="willetts2018statistical"></d-cite>. Our SSL DCNN+HMM model enables a more robust and fine-grained estimation of daily activity patterns beyond traditional acceleration magnitude levels <d-cite key="prioreschi2013clinical"></d-cite><d-cite key="gossec2019detection"></d-cite>, which we propose allows for a richer characterisation of PA and sleep from wearable sensor data.

<img src="/assets/img/ssl_wearable-pro.png" width="700"/><br>
<p align="justify"><b>Self-supervised learning pipeline</b>. Continuous (passive) actigraphy was recorded from participants' Apple smartwatch over the study duration. Deep convolutional neural networks (DCNN) were pre-trained on 700,000 person days in the publicly available UK Biobank using self-supervised learning&mdash;and fine-tuned with the Capture-24 dataset&mdash;to estimate participant's daily activity patterns in the weaRAble-PRO study. Physical activity (PA) metrics of daily-life, for example, the time spent walking, the frequency of exercise, or the length and quality of sleep were investigated as markers to characterise symptoms of disease in people with RA compared to HC.</p>


### Extraction sensor-based outcomes
Wearable sensor-based features were derived from the smartphone during the active guided tasks and passively from the
smartwatch during daily life. “Active” features were extracted from smartphone sensor-based measurements during the prescribed guided tests, and aimed to capture specific aspects of RA physical function, related to pain, dexterity, mobility and fatigue. In addition, “passive” features were extracted from smartwatch sensor-based measurements, collected continuously in the background over the 14-day period. Daily activity predictions from the ML SSL model were summarised into general features measuring activity levels, period, duration, and type of activity, as well as sleep detection and sleeping patterns.

### Machine learning estimation of RA 
From our sensor-based outcomes that we developed, we next explored how state-of-the art machine learning (ML) models could characterise the impact of RA on the daily life of the participants in the 14-day weaRAble-PRO study. Multivariate modelling aimed to explore the ability of active, passive, and PRO measures to: <b>(1)</b> distinguish RA participants from healthy controls (HC) and <b>(2)</b> to estimate RA disease severity: between RA participants with moderate symptoms (RA mod) and severe symptoms (RA sev) as binary classification tasks. Expansions of this analysis subsequently investigated how the in-clinic RAPID-3 assessment, a continuous measure of RA severity, could be estimated from the combination of PRO and sensor-based outcomes.

 We first outlined how regularised linear regression (LR) models, with combinations of $\ell_1$ and $\ell_2$ priors, such as LR-lasso ($\ell_1$), LR-ridge ($\ell_2$), and LR-elastic-net ($\ell_1$ +$\ell_2$), could yield predictive, yet sparse model solutions for estimating RA status. Further regularisation extensions were also investigated using the sparse-group lasso (SG-lasso)--an extension of the lasso that promotes both group sparsity and within group parameter-wise ($\ell_2$) sparsity, through a group lasso penalty and the lasso penalty---which aims to yield a sparse set of groups and also a sparse set of covariates in each selected group <d-cite key="friedman2010note"></d-cite><d-cite key="simon2013sparse"></d-cite>. We also compared linear LR models to common, off-the-shelf, non-linear to decision tree (DT) based non-linear models, for instance Random Forest (RF) <d-cite key="breiman2001RF"></d-cite> and Extreme Gradient Boosted Trees (XGB)<d-cite key="chen2016xgboost"></d-cite>. 

## Key Findings

#### 1. Remote sensor-outcomes reflect RA status and severity
In this work, we detailed how raw data collected from smartphone and smartwatch sensors can be transformed into sensor-based outcomes that are reflective of disease status. In concurrence with previous studies, many remotely collected smartphone sensor-outcomes distinguished RA participants and RA severity levels. For example, it was observed that joint ROM features differentiated HC and RA groups---a similar finding to our previous work <d-cite key="hamy2020developing"></d-cite>---and that RA participants were less mobile, taking longer to move between positions (as measured during the lie-to-stand exercise)---as previously shown by Andreu-Perez, et al. <d-cite key="andreu2017developing"></d-cite>.

Activity monitoring revealed distinct differences distinguishing RA status, for example the daily percent of the day in moderate-to-vigorous physical activity and similar features, were significantly lower in the RA population compared to healthy controls---a similar finding by Prioreschi, et al. <d-cite key="prioreschi2013clinical"></d-cite> and an observation people with RA regularly self-report <d-cite key="sokka2008physical"></d-cite>. Other specific RA symptom measurements, like morning stiffness or disrupted sleep, were evident in certain RA participants. For example, the mean acceleration value $>$30 [mins] after wake-up were lower in RA---also a similar finding to Keogh, et al. <d-cite key="keogh2020thorough"></d-cite>---or that the number of movement episodes during night-time sleep distinguished some specific RA participants. 

<div class="fake-img l-body">
  <img src="/assets/img/pop_activity_patterns.png" width="700"/><br>
  <p>Population-wide daily activity by time of the day. Variation in the average ML SSL model predicted daily-activity (probability) over time for participants in the 14-day weaRAble-PRO study.</p>
</div>


#### 2. Combined benefit of active and passive sensor data, but patient burden needs to be considered
Our work is the first study to combine active smartphone and passive wearable measurements to distinguish RA status and measure variations in RA severity. While models trained on only passive features tended to marginally outperform models trained solely on active guided test features, combining both active + passive features led to the best performance in RA identification for all models investigated. Interestingly, it was found that completely different RA subjects were misclassified by active versus passive models.

In addition, further experiments with the LR-SG-lasso determined that only activity monitoring domain features were mainly needed in order to identify RA participants. This indicates that we sometimes do not need to prescribe all guided test assessments, or to parse all activity feature domains, but that a small number of prescribed assessments can be sufficient to characterise RA status. For example, including only the lie-to-stand assessment rather than also prescribing the similar and highly correlated sit-to-stand assessment in feature studies; or removing the prescribed walking assessment (shown to have little predictive value in the weaRAble-PRO study) and using passive daily life walking predictions generated from the activity recognition model instead, which could reduce patient burden. 

<div class="fake-img l-body">
  <img src="/assets/img/PRO_sensor_barchart.png" width="350"/><img src="/assets/img/sensor_barchart.png" width="350"/><br>
  <p><b>Ability of combined sensor-outcomes to distinguish between RA status and RA severity levels.</b> Comparison of (a) RA identification (RA vs. HC) performance and (b) RA severity level estimation (RA (mod) vs RA (sev)), using patient reported outcomes (PRO) and combined PRO, active, and passive sensor-based outcomes in the weaRAble-PRO study. auroc: Area under the receiver operator curve; $\kappa$, Cohen's Kappa statistic; F<sub>1</sub>, Macro-F1 score.</p>
</div>

#### 3. Only 7 days of sensor-outcomes are required to remotely characterise RA impact
We also observed that after collecting 7 days of sensor-data in the weaRAble-PRO study, a sufficient volume of data had already been recorded to reliably distinguish RA participants from a healthy population; participant feature reliability (as measured ICC values) stabilised at good-to-excellent levels, maximal identification performance of RA participants plateaued, and that there was no additional benefit to averaging over a fortnight's worth of data versus a week. Therefore it is recommended that considering at least one week's worth of sensor data is collected, it might be more beneficial to gather less data from a greater number of participants, rather than greater duration of sensor data from the same participants.

<div class="fake-img l-body">
  <img src="/assets/img/daily_f1.png" width="350"/><img src="/assets/img/daily_icc.png" width="350"/><br>
  <p><b>The number of days of sensor-data required to remotely characterise RA impact.</b>  Comparison of <b>(a)</b> the minimal amount of days of data needed distinguish RA status, as measured by the F1 score across 5-fold cross validation (CV), between active, passive, and combined feature sources; <b>(b)</b> the feature (test-retest) reliability, as measured by the intraclass correlation coefficient (ICC), between RA participants and HC across the study duration (14 days); F1 scores and ICCs suggest that model performance and feature reliability stabilises once more than 7 days of data are used per participant.</p>
</div>

#### 4. In-clinic RA severity scores can be remotely estimated from PRO and sensor-based outcomes
We found that combining patient-reported outcomes (PRO) and objective sensor-outcomes could better capture RAPID-3-based RA severity at baseline than PROs alone; most estimated RAPID-3 scores correctly stratified participants across severity levels from healthy to moderate to severe RA, suggesting that sufficient information to characterise RA disease severity could be reflected in the remote monitoring outcomes derived in the 14-day weaRAble-PRO study. To the best of the authors knowledge, this offers the first evaluation and insight how remote monitoring outcomes in daily life can estimate in-clinic administered assessments of RA impact. 

<div class="fake-img l-body">
  <img src="/assets/img/rapid3_estimation_pro_sensor.png" width="700"/><br>
  <p align="justify"><b>The ability of remote PRO + sensor-outcomes to estimate in-clinic determined RA severity scores</b>. Scatter plot of baseline RAPID-3 scores versus predicted scores per subject. Participant model-estimated RAPID-3 scores can be further interpreted through detailed inspection of the daily smartphone-based patient-reported joint pain map (JMAP) total scores&mdash;which was not included as a predictor in the model. Higher JMAP scores indicate higher levels of pain experienced. Additional interpretability, through the JMAP, demonstrated that PRO + sensor-based outcome estimation of the RAPID-3 could reliably reflect patient's perceived daily RA symptoms.</p>
</div>


## Limitations
There are a number of limitations that must be considered in the weaRAble-PRO study. Despite rich individual level measurements, the study recruited a relatively small sample size (HC, n=30; RA, n=30). As such, a degree of variability and uncertainty existed in constructing cross-validated models to distinguish RA participants, RA severity levels, or estimate the in-clinic RAPID-3 assessment. There are also limitations associated with modelling a clinician-administered assessment, or clinical labels formulated from in-clinic assessments. A degree of variability and uncertainty existed in modelling the RAPID-3, or RA severity levels, and certainly extrapolation of results aimed at generalising RA is therefore not possible without the availability of larger cohorts and further external validation. Furthermore, the RAPID-3 was assessed at baseline, with participants recalling the prior week, yet the PRO and sensor-based features were calculated as averages over subsequent 14-day trial period from baseline. As such, the baseline RAPID-3 may not have precisely reflected the participant's disease status recorded earlier, due to the underlying mutability and heterogeneity of RA symptoms over short periods of time. The subjectivity of PRO predictors should also considered, for instance, pain or perceived quality of sleep is relative, and some healthy participants recorded experiencing pain or affected sleep in PRO questionnaires. As a result, some PRO values influenced HC RAPID-3 predictions greater than zero, i.e., indicating the presence of RA symptoms---albeit non-zero estimated RAPID-3 predictions for HCs were generally low ($<$2). 

## Impact
Our findings in the weaRAble-PRO study demonstrate how digital health technology (DHT) captured sensor-outcomes, recorded from smartphone-based active tests and continuously collected passive smartwatch-based monitoring, could characterise meaningful aspects of rheumatoid arthritis (RA)
impairment and physical function impacting daily life. Remotely collected wearable sensor-outcomes could distinguish RA status from healthy controls—demonstrating further improved performance when combining the sensor-data from both devices—and how objective sensor-outcomes could augment
patient (self-) reported outcomes to remotely estimate RA severity. Furthermore, by the half-way point of the weaRAble-PRO study (day 7), a sufficient volume of data had already been collected to reliably distinguish the characteristics of RA participants. 

The weaRAble-PRO study typifies how continuously collected patient self-reported and sensor-based outcomes may more closely reflect participant perceived and experienced symptoms that impact daily life. While in-clinic assessments are considered the gold-standard means of assessing disease
severity in RA, it is clear that remotely collected, continuous, patient-centric measurements generated from PRO and sensorbased
outcomes offer promising insights that can undoubtedly augment in-clinic assessments for RA. We believe that our work—the first comprehensive evaluation how remote sensor data can augment traditional PRO measures to estimate clinician-determined RA severity—helps informs future DHT
study design to better characterise the impact of RA on daily life, ultimately to expand the use of DHT to develop more
sensitive, and patient-centric, endpoints in RA clinical trials and real-world studies.


## Code Availability
Apple Watch sensor processing was performed using a bespoke version of the biobankAccelerometerAnalysis toolkit, found at: [https://github.com/OxWearables/biobankAccelerometerAnalysis](https://github.com/OxWearables/biobankAccelerometerAnalysis). 

Deep networks were built using Python v3.7 through a PyTorch v1.7 framework. Our self-supervised learning activity prediction code and trained models are publicly available at:  [https://github.com/OxWearables/ssl-wearables](https://github.com/OxWearables/ssl-wearables), including pre-trained models on 100K participants in the UK Biobank. 

Some guided test exercises and health metrics calculated are proprietary to Apple ResearchKit [http://researchkit.org/](http://researchkit.org/) and Apple HealthKit [https://developer.apple.com/documentation/healthkit](https://developer.apple.com/documentation/healthkit), check these out for more details. 

Statistical and machine learning analysis was developed using scikit-learn v1.1.1. Further analysis code can be made available by reaching out to me by email at [andrew.creagh@eng.ox.ac.uk](andrew.creagh@eng.ox.ac.uk). 


## Reference
If you use our work, please consider citing:

```tex
@article{creagh2022digital,
  title = {Digital health technologies and machine learning augment patient reported outcomes to remotely characterise rheumatoid arthritis},
  author = {Creagh, A. P. and Hamy, V. and Yuan, H. and Mertes, G. and Tomlinson, R. and Chen, W-H. and Williams, R. and Llop, C. and Yee, C. and Duh, M-H. and Doherty, A. and Garcia-Gancedo, L. and Clifton, D. A.},
  elocation-id = {2022.11.18.22282305},
  year = {2022},
  doi = {10.1101/2022.11.18.22282305},
  publisher = {Cold Spring Harbor Laboratory Press},
  html = {https://www.medrxiv.org/content/10.1101/2022.11.18.22282305v1},
  journal = {medrXiv},
  abbr = {medrXiv},
}
```
