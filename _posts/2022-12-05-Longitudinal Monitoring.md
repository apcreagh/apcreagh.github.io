---
layout: distill
title: Longitudinal Trend Monitoring of Multiple Sclerosis Ambulation Using Smartphones
description: Our paper was recently accepted for publication in IEEE OJEMB! 🥳 Here I will summarise our main findings and the impact of our work. 
tags: [digital health, ieee-ojemb]  
categories: summary
date: 2023-01-05
draft: False
preview: 


authors:
  - name: Andrew P. Creagh*
    url: "https://www.andrewcreagh.com"
    affiliations:
      name: University of Oxford, UK. 
  - name: Frank Dondelinger
    url: "https://ch.linkedin.com/in/frank-dondelinger-bb634992"
    affiliations:
      name: F-Hoffmann La Roche, CH.
  - name: Florian Lipsmeier
    url: "https://ch.linkedin.com/in/florian-lipsmeier-147ab0162/"
    affiliations:
      name: F-Hoffmann La Roche, CH.
  - name: Michael Lindemann
    url: "https://de.linkedin.com/in/michaellindemann/"
    affiliations:
      name: F-Hoffmann La Roche, CH.
  - name: Maarten De Vos
    url: "https://www.esat.kuleuven.be/stadius/person.php?id=203"
    affiliations:
      name: KU Leuven, BE.
bibliography: 2023-01-05-Longitudinal.bib


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
    - name: Estimating Ambulatory-related Disease Severity
    - name: Longitudinal Trend Monitoring 
  - name: Key Findings
  - name: Limitations
  - name: Impact
  - name: References

# Below is an example of injecting additional post-specific styles.
# If you use this post as a template, delete this _styles block.
_styles: >
  .fake-img {
    background: #ffffff;
    border: 1px solid rgba(0, 0, 0, 0.1);
    box-shadow: 0 0px 4px rgba(0, 0, 0, 0.1);
    margin-bottom: 12px;
    text-align: justify;
  }
  .fake-img p {
    font-family: monospace;
    color: white;
    margin: 12px 0;
    text-align: justify;
    font-size: 14px;
  }

  figure {
      display: inline-block;
      margin: 5px; /* adjust as needed */
  }
  figure img {
      vertical-align: middle;
      margin-bottom: 12px;
  }
  figure figcaption {
      text-align: justify;
      margin-bottom: 20px;
  }
---
[<img src="https://raw.githubusercontent.com/FortAwesome/Font-Awesome/6.x/svgs/regular/window-maximize.svg" width="50" height="50">](https://ieeexplore.ieee.org/document/9944841)
[<img src="https://raw.githubusercontent.com/FortAwesome/Font-Awesome/6.x/svgs/regular/file-pdf.svg" width="50" height="50">](/assets/pdf/Creagh_2022_longitudinal-trend-monitoring.pdf)<br>
<b>Note:</b> This article is best viewed in 'light mode'!  <img src="https://raw.githubusercontent.com/FortAwesome/Font-Awesome/6.x/svgs/regular/sun.svg" width="20" height="20"/>

## Summary

In recent years, the emergence of consumer digital technologies such as smartphones which are used for healthcare applications, has opened the possibility of developing rich, continuous, and objective measures of disease that can be administered remotely outside of standard clinical settings. For instance, consumer smartphone devices can objectively characterise ambulation and fatigue in people with multiple sclerosis (PwMS) which is one of the main symptoms of disease. Importantly, it has been shown that earlier identification of changes in PwMS impairment are important to identify and provide better therapeutic strategies. 

In this work, we demonstrated how PwMS’ ambulatory patterns can be captured from smartphone inertial sensor-based measurements recorded during a daily “two-minute walk test” (2MWT), a remotely administered walking test as part of Roche's seminal FLOODLIGHT study in MS. Deep networks offer state-of-the-art and data-driven approaches that are capable of learning smartphone sensor-based features capturing ambulatory information. Our study subsequently explored how deep convolutional neural networks (DCNNs) could be used to distinguish healthy controls (HC) from PwMS that have mild and moderate disability, longitudinally, over the 24-week study. 

Our results indicated that smartphone-based ambulatory severity outcomes could accurately estimate MS level of disability, as measured by the clinician-administered EDSS score. Furthermore, longitudinal severity outcomes were shown to accurately reflect individual participants' level of disability over the study duration. Anecdotally, we even observed the possibility of these measurements to remotely capture MS relapse events, where an increase in model-estimated symptom severity coincided with when two participants had self-reported that a relpase had occured using their smartphone application.
<figure>
<img src="/assets/img/ieee_ojemb/digital_sensor_outcomes.png" width="700"/><br>
<figcaption><b>Digital outcomes for remote MS-patient monitoring</b>. Digital sensor-based outcomes created from digital health technologies, such as smartphone-based sensor outcomes, enable clinicians to continuously monitor the disease course of people with multiple sclerosis (PwMS) outside of the clinic. These objective sensor-based measures can be administered remotely and at high-frequency to PwMS. This granularity of assessment may help capture subtle manifestations of habitual MS, as well as the disease course and relapse events that are currently missed by infrequent and less sensitive in-clinic measures. Diagram adapted from <d-cite key="baker2021digital"></d-cite></figcaption>
</figure>

## Background

The symptoms of neurodegenerative diseases, such as multiple sclerosis (MS), frequently fluctuate over time, and between patients, ensuring
that it is notoriously difficult to quantify effective therapeutic interventions and disease management techniques. Current in-clinic
assessments are often too infrequent to track changes in MS impairment over time. People with MS (PwMS) experience a progressive decline in physical function and quality of life and over time---this often leads to disability and difficulty to perform many tasks of daily life (think about going shopping, getting dressed, taking your dog on a walk, or caring for your children or grandchildren). Currently, the gold-standard methods of measuring the impact of MS on daily life rely on infrequent clinical visits that may often occur every 3--4 months, with assessments depending on a combination of subjective clinician-determined scores---in MS, clinicans use the Expanded Disability Status Scale (EDSS) <d-cite key="kurtzke1983edss"></d-cite>---or specific functional domain assessments (i.e., performance-based tests) such as the Timed 25-Foot Walk (T25FW), which is part of the Multiple Sclerosis Functional Composite score, and the Two-Minute Walk Test (2MWT) which also assesses physical gait function and fatigue in PwMS.

<br>
<img src="/assets/img/ieee_ojemb/RRMS_disease_course.png" width="170"/>
<img src="/assets/img/ieee_ojemb/PPMS_disease_course.png" width="170"/>
<img src="/assets/img/ieee_ojemb/PRMS_disease_course.png" width="170"/>
<img src="/assets/img/ieee_ojemb/SPMS_disease_course.png" width="170"/><br>
<figcaption><b>Typical disease course for various clinically defined multiple sclerosis (MS) phenotypes</b>: Relapsing-remitting MS (RRMS); Primary-progressive MS (PPMS); Secondary-progressive MS (SPMS) and Progressive-relapsing MS (PRMS). Image adapted from Lublin et al.<d-cite key="Lublin1996"></d-cite>.
</figcaption>
<br><!---hack...-->

Although MS follows a highly heterogeneous and subject-specific disease course, the disease profiles have been grouped into four clinical phenotypes which are based on disease progression <d-cite key="RN876"></d-cite><d-cite key="Goldenberg2012"></d-cite><d-cite key="Confavreux2000"></d-cite><d-cite key="Fisher2008"></d-cite><d-cite key="Steinman2001"></d-cite>: 
- <b>Relapsing-remitting MS (RRMS)</b>: the majority of PwMS will initially experience RRMS, a state dominated by sudden acute symptoms developing (a “relapse”) over days before generally plateauing over weeks or months termed "remission". RRMS generally affects 85% of PwMS and disease activity typically occurs acutely at a sub-clinical level.  
- <b>Primary-progressive MS (PPMS)</b>: those experiencing consistent but worsening symptoms can be thought of as having PPMS (roughly 10% of PwMS).
- <b>Secondary-progressive MS (SPMS)</b>: can occur in some RRMS patients, where the disease course continues to worsen with or without periods of remission. Half (50%) of RRMS patients will go onto develop SPMS.  
- <b>Progressive-relapsing MS (PRMS)</b>: is more rare (affecting fewer than 5% of PwMS); it occurs from diagnoses as a progressive disease course, with periods of relapse, but without any remission periods. 

In recent years, there has been a shift towards the a adoption of body worn sensors to objectively evaluate ambulatory performance in PwMS, circumventing the need for resource-intensive and expensive gait laboratory equipment, but also opening up the possibility to measure physical function outside of standard clinical settings. These technologies can provide new data-driven metrics for clinical decision-making during in-clinic visits <d-cite key="brichetto2019beyond"></d-cite> and may be more accurate than conventional clinical outcomes. 


### Study Objectives 
This study builds upon our previous investigations <d-cite key="Creagh2020SmartphoneAmbulation"></d-cite>,<d-cite key="creagh2021interpretable"></d-cite>,<d-cite key="Bourke2020Gait"></d-cite> where we have shown how inertial sensors contained within consumer-based smartphones can be used to characterise gait impairments in PwMS from a remotely administered Two-Minute Walk Test (2MWT). Our previous study <d-cite key="creagh2021interpretable"></d-cite> first introduced how state-of-the-art Deep Convolutional Neural Networks (DCNN) could be applied to smartphone sensor data collected during a remotely performed 2MWT could determine a study participants’ MS status: such as healthy (i.e., no MS), PwMS with mild, or PwMS with moderate disability. The work presented here aims to evaluate how these DCNN severity predictions from daily 2MWTs can characterise the status of healthy participants versus PwMS with mild, or PwMS with moderate disability longitudinally over a 24 week period.

## Dataset
The FLOODLIGHT (FL) proof-of-concept (PoC) app was trialled in a 24-week, prospective study in PwMS and HCs (NCT02952911) to assess the feasibility of remote patient monitoring using smartphone (and smartwatch) devices <d-cite key="midaglia2019adherence"></d-cite>,<d-cite key="montalban2021smartphone"></d-cite>. Participants were provided with a pre-configured smartphone (Samsung Galaxy S7) and smartwatch (Motorola 360 Sport) with the Floodlight PoC app installed. A total of 97 participants (24 HC subjects; 52 mildly disabled, PwMSmild, EDSS [0-3]; 21 moderately disabled PwMSmod, EDSS [3.5-5.5]) contributed data which was recorded from a 2MWT performed out-of-clinic <d-cite key="Creagh2020SmartphoneAmbulation"></d-cite>. Subjects were requested to perform a 2MWT daily over a 24-week period, and were clinically assessed at baseline, week 12 and week 24. 

## Methods

<figure>
<img src="/assets/img/ieee_ojemb/ieee_ojemb_visual_summary.png" width="700"/><br>
<figcaption><b>Remote characterisation of ambulatory function using wearables & AI/ML.</b> Artificial Intelligence (AI) algorithms, such as Deep Convolutional Neural Networks, can transform smartphone inertial sensor measurements to estimate participants’ daily ambulatory-related level of multiple sclerosis (MS) disability, collected during a remotely executed Two-Minute Walk Test (2MWT).</figcaption>
</figure>

### Estimating Ambulatory-related Disease Severity 
The foundation of this work employs a Deep Convolutional Neural Network (DCNN) to estimate participants MS severity from the smartphone inertial sensor data was recorded while participants performed a daily, at home, two minute walk test (2MWT).  The raw accelerometer sensor data from each 2MWT were then partitioned into multiple vector sequences (epochs), where a DCNN was then trained to classify a given epoch as having been performed by a HC, PwMSmild or PwMSmod participant. The DCNN model implemented has previously been introduced in Creagh et al. (2021) <d-cite key="creagh2021interpretable"></d-cite>, where the network was first pre-trained on the UCI smartphone-based Human Activity Recognition (HAR) dataset, and thereafter fine-tuned on the data in FL for MS severity classification. 

The network outputs are interpreted as $$\hat y_k(\mathbf{x}_n,\mathbf{w}) = p(y_{k} = k|\mathbf{x}_n)$$. As such, $\hat y_k$ can be thought of as the probability that a given epoch $$\mathbf{x}_n$$ belonged to class $k$. A continuous estimate of severity (i.e., the predicted level of MS disability) can then be captured by taking an average of all epoch predictions over a test for a given assessment day, $d$ such that:
$$
\begin{align}
\hat{y}_d= \frac{1}{N}\sum_{n=1}^{N} \underset{k}{\mathrm{argmin}} (p(\hat{y}_k=k | \mathbf{x}_n))
\end{align}
$$
where $N$ are the number of windowed epochs for a given test date, $d$, and $k$ lies in an ordinal range of $[0, 1,...K]$. Therefore $\hat{y}_d$ will be continuous such that $0\leq \hat{y}_d \leq K$ and can conceptualised as a naive estimate of MS disease severity, mapping a predicted level of disability ranging from healthy to mild to moderate.

### Longitudinal Trend Monitoring 
Longitudinal trends of specific participants were examined as a time-series by considering the severity estimates $\hat{y}$ of repeated 2MWTs over all their available data for the duration of the FL study. The goal of this work was to perform longitudinal analysis of participants severity and visualise the average severity trends over time. First, missing 2MWT DCNN-based outcomes were first imputed using piecewise linear interpolation (PLI), by considering $\hat{y}$ as a time-series to impute missing test severity observations on a given date. Note: imputed 2MWTs were only included for calculation of average trend estimation for individual participants and not for model evaluation. Next, a simple trend estimation was applied to the time sequence of severity estimates ($\hat{y}$) across days ($d$) using a $d-$ centred linear moving average filter (MAF). A 7-day window was implemented in order to capture the trends in $\hat{y}_d$ over the study duration. 

## Key Findings

#### 1. Remote smartphone sensor-outcomes reflect clinician-determined MS severity
In this work, it was shown how a deep network classification model could (naïvely) estimate the level of participant disability from ordinal classification categories.  Severity outcome estimates stratified across HC and PwMS groups and were strongly correlated to disease status ($r$: 0.75; $\rho$: 0.71, p$<$0.001), as measured by the EDSS---considered the ground-truth assessment in PwMS <d-cite key="kurtzke1983edss"></d-cite>. 

<div class="fake-img l-body">
  <img src="/assets/img/ieee_ojemb/dcnn_edss_scatter.png" width="400"/> 
  <figcaption><br><b>The relationship between the continuous disease severity outcome estimate, EDSS and subject group</b>. Figure depicts the scatter plot demonstrating the positive correlation ($r$: 0.75; $\rho$: 0.71; $p<$0.001) between the average severity outcome and average EDSS score per subject. A DCNN model was constructed based on the average class predictions (HC, PwMSmild, PwMSmod) per subject over all 2MWTs, creating an estimated continuous prediction probability distribution, ranging from healthy to moderate MS. Each point therefore represents the average estimated severity outcome (probability) for that subject.  A black line represents the line of best fit between severity and EDSS ($r^2$: 0.56, $p<$0.001).</figcaption>
</div>

For instance, no misclassifcation of HC as PwMSmod was observed, or vice-versa, indicating that severity estimates were reflective of true disease status. More interestingly, those subjects at classification boundaries displayed severities representative of their clinical assessments. For instance, those with EDSS just above 3.5 (i.e. PwMSmod) were misclassified more as PwMSmild compared to those with EDSS much greater than 3.5, implying that a reflective estimate of disease severity could be captured by transforming a DCNN model into a simple probabilistic outcome per subject. 

#### 2. Smartphones can longitudinally monitor MS ambulatory severity over a 24-week study
The longitudinal patterns of healthy controls versus participants with varying manifestations of MS severity could be characterised by examining severity outcomes over the duration of the FL study for individual subjects. For instance, the figure below depicts examples of stable trends for a correctly classified HC and PwMSmod subject respectively. While both participants had some incorrect predictions, the mean severity prediction over all repeated tests reflected the participant's true class grouping. 

<div class="fake-img l-body">
  <br><img src="/assets/img/ieee_ojemb/Longitudinal_HC.png" width="700"/><br><br><img src="/assets/img/ieee_ojemb/Longitudinal_PwMSmod.png" width="700"/> <figcaption><br><b> Panel plot illustrating the longitudinal severity estimate outcome for correctly classified a HC and a PwMSmod subject.</b>  Depicted are the estimated level of disability for an example a HC subject and PwMSmod subject during the study. Each circle represents the severity outcome estimate for a 2MWT performed on a given date. Shaded blue lines depict the and 7-day trend, represented by the d-point centred moving average across days (d). Dashed black lines represent site-visits where the participant was assessed clinically.</figcaption>
</div>

#### 3.  Remote smartphone sensor-outcomes can remotely capture MS relapse events
Evaluating subject's performance longitudinally suggested that severity estimates may be sensitive to capture MS-symptom worsening, particulary relapses. During the FL study, four participants experienced relapses which they self-reported using the application on their smartphones. Longitudinal analysis of the trajectories of daily severity estimates from these subjects revealed useful insights into the manifestation of relapses expressed in remote inertial sensor data. For instance, two subjects displayed an increased severity outcome up to and around the data of reporting a relapse (see figures below), suggesting that sensor-based ambulatory outcomes could potentially be sensitive enough to remotely capture relapse events.

<div class="fake-img l-body">
  <br><img src="/assets/img/ieee_ojemb/Longitudinal_PwMSmild_relapse_example-1.png" width="700"/><br><br><img src="/assets/img/ieee_ojemb/Longitudinal_PwMSmod_relapse_example-1.png" width="700"/><br><br>
  <figcaption><b>Panel plot illustrating the longitudinal severity estimate outcomes for PwMS participants who self-reported a relapse using the FLOODLIGHT smartphone application during the study.</b>  Each circle represents the severity outcome estimate for a 2MWT performed on a given date. Shaded blue lines depict the and 7-day trend, represented by the $d$-point centred moving average across days ($d$). Dashed black lines represent site-visits where the participant was assessed clinically. Dates of self-reported relapse onset are represented in black.</figcaption>
</div>

#### 4. Missing data might be indicative of changes in disability status
We need to consider that missing data might also contain useful information relating to how a patient is feeling or their MS disability status. For example, the study participant below reported (non-relapse) adverse clinical events occurring on non-specified dates between weeks 8 and 12. Around these dates the particiapnt's adhereance drops and they stop contributing daily 2MWTs. Obviously, this is an anecdotal example, but it poses the question: "<em>did the adverse event affect this participant's adherence or ability to perform the test</em> ?" 

<div class="fake-img l-body">
  <br><img src="/assets/img/ieee_ojemb/Longitudinal_PwMSmod_relapse_example-2.png" width="700"/><br>
 <figcaption><br><b>Panel plot illustrating the longitudinal severity estimate outcomes for a PwMS participants with missing data.</b>
  Each circle represents the severity outcome estimate for a 2MWT performed on a given date. Shaded blue lines depict the and 7-day trend, represented by the $d$-point centred moving average across days ($d$). Dashed black lines represent site-visits where the participant was assessed clinically. Dates of self-reported relapse onset are represented in black.  This participant also reported (non-relapse) adverse clinical events occurring on non-specified dates between weeks 8 and 12.
 </figcaption>
</div>

Indeed, missing data might be a marker of changes in disability status itself (i.e., that the data is not missing-at-random (MAR)). However, it is difficult to monitor patients if they’re not contributing data over a long periods---adherence will often be a problem when prescribing 2 minutes of walking a day, daily, for 24 weeks. Therefore, we must consider patinent burden when developing our digital biomarker assessments and solutions. In my opinion, I think we need to consider how we can incorporate as much information as possible from passive approaches, collecting sensor data during daily life. For example, a smartwatch could collect sensor-data characterising physical activity and ambulation unobtrusively from patients. Swapping out some prescribed "active" tests, or reducing the frequency of assessments by supplementing with passive data could help build more robust longitudinal models and help circumvent some of the problems associated with missing assessment data. 


## Limitations
Despite the potential of smartphone-based outcomes to remotely monitor individual participant's ambulatory function longitudinally, there are several limitations of this study which must be considered. 

1. <strong>Severity outcomes explored in this work were naïve estimates</strong>: although outcomes captured a trend of increased impairment with higher severity (as modelled by EDSS), they should not be considered an exact measure of MS, nor a surrogate clinical outcome to permit any clinical diagnosis, or replace in-clinic assessments. 
2. <strong>Estimates were not always correct!</strong>: there were many subject misclassifications. In this work we only showed correct and stable estimate examples, however, it must be noted that some participants, both healthy or with MS, followed irregular trends or whose estimated level of disability were consistently incorrect. 
3. <strong>Predicted outcomes were based solely on ambulation performance</strong>: The 2MWT is an assessment originally only intended to investigate ambulatory function and fatigue in PwMS through the measurement of distance travelled <d-cite key="scalzitti2018validation"></d-cite><d-cite key="kieseier2012"></d-cite>. Many participants in the FL PoC study may not have had ambulatory-related dysfunction, or whose milder level of disease did not impair their gait, compared to the healthy control cohort.
  * Constructing more robust severity outcomes should also aim to incorporate the data captured from other functional domains, such as dexterity and cognition assesments.
4. <strong>The performance of 2MWT can be highly influenced by the testing environment</strong>: the FL 2MWT was a remotely executed out-of-clinic assessment. We cannot determine how factors such as the length of the hallways, or the number and frequency of subject turns can affect individual's performance and the subsequent relaibility of our model. 
5. <strong>The time-series nature of daily repeated 2MWT measurements was not fully utilised</strong>: Each repeated test was treated as independent, and as such, trajectories did not incorporate any temporal information across a population or within a subject; for example, whether the previous day's $d-1$ test could affect the outcome at $d$ or $d+1$). 
  * It would be assumed that this is critically missing temporal information which could help build more reliable and accurate longitudinal models.
  * For instance, the repeated FL assessments, and therefore sensor outcomes that were extracted, could be analysed with models that exploit this aggregation of temporal information directly <d-cite key="schwab2019phonemd"></d-cite><d-cite key="vaswani2017attention"></d-cite>.



## Impact
We believe that the work presented in this study to be of important value, emphasising the potential of remote sensor outcomes to augment current in-clinic acquired patient information. The long-term remote monitoring of PwMS function could open up the space for true personalisation: the clustering of disease trajectories or similar patients, estimating the likelihood of disease progression, quantifying response to different treatments as a population or an individual, as well catching the mutable patterns of MS disease that are only visible out-of-clinic and as a function of time.  We believe that our work helps informs future digital health technology-based study design, to better remotely characterise the impact of MS, ultimately to expand the use of DHT to develop more sensitive, and patient-centric, endpoints in clinical trials and real-world studies.


## Reference
If you use or like our work, please consider citing us:

```tex
@article{creagh2022longitudinal, 
  author={Creagh, Andrew P. and Dondelinger, Frank and Lipsmeier, Florian and Lindemann, Michael and De Vos, Maarten}, 
  journal={IEEE Open Journal of Engineering in Medicine and Biology},  
  title={Longitudinal Trend Monitoring of Multiple Sclerosis Ambulation Using Smartphones},  
  year={2022}, 
  volume={3},  
  number={},  
  pages={202-210}, 
  doi={10.1109/OJEMB.2022.3221306}
}
```
