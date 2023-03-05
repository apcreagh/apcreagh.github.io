---
layout: distill
title: Generating synthetic electronic health record (EHR) data using denoising diffusion probabilistic models
description: Our recent work on 'Synthesizing Mixed-type Electronic Health Records using Diffusion Models' is now available on arXiv! 📢
tags: [ClinicalMachineLearning, ElectronicHealthRecords, SyntheticData, GenerativeModels, DiffusionModels, DenoisingDiffusionProbabilisticModels]  
categories: summary, pre-print
date: 2023-03-01
draft: False
preview: 


authors:
  - name: Taha Ceritli
    url: "https://tahaceritli.github.io/"
    affiliations:
      name: IBME, University of Oxford.
  - name: Ghadeer O. Ghosheh
    url: "https://eng.ox.ac.uk/people/ghadeer-ghosheh/"
    affiliations:
      name:  IBME, University of Oxford.
  - name: Vinod Kumar Chauhan
    url: "https://sites.google.com/site/jmdvinodjmd/"
    affiliations:
      name:  IBME, University of Oxford.
  - name: Tingting Zhu
    url: "https://ibme.ox.ac.uk/people/tingting-zhu/"
    affiliations:
      name: IBME, University of Oxford.
  - name: Andrew P. Creagh
    url: "https://www.andrewcreagh.com"
    affiliations:
      name: IBME, BDI,<br>University of Oxford.
  - name: David A. Clifton
    url: "https://ibme.ox.ac.uk/people/david-clifton/"
    affiliations:
      name: IBME, University of Oxford.
bibliography: 

# Optionally, you can add a table of contents to your post.
# NOTES:
#   - make sure that TOC names match the actual section names
#     for hyperlinks within the post to work correctly.
#   - we may want to automate TOC generation in the future using
#     jekyll-toc plugin (https://github.com/toshimaru/jekyll-toc).
toc:
  - name: Challenge
  - name: Solution
  - subsections: 
    - name: Denoising Diffusion Probabilistic Models (DDPMs)
  - name: Evaluation
  - name: Feedback
  - name: Reference

# Below is an example of injecting additional post-specific styles.
# If you use this post as a template, delete this _styles block.
_styles: >
  .fake-img {
    background: #ffffff;
    border: 1px solid rgba(0, 0, 0, 0.1);
    box-shadow: 0 0px 4px rgba(0, 0, 0, 0.1);
    margin-bottom: 20px;
  }
  .fake-img p {
    font-family: monospace;
    color: white;
    text-align: left;
    margin: 12px 0;
    text-align: left;
    font-size: 14px;
    margin-bottom: 20px;
  }
  .fake-img figcaption {
      text-align: justify;
      margin-bottom: 20px;
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

[<img src="https://raw.githubusercontent.com/FortAwesome/Font-Awesome/6.x/svgs/regular/window-maximize.svg" width="50" height="50">](https://arxiv.org/abs/2302.14679)
[<img src="https://raw.githubusercontent.com/FortAwesome/Font-Awesome/6.x/svgs/regular/file-pdf.svg" width="50" height="50">](https://arxiv.org/pdf/2302.14679.pdf)<br>
<b>Note:</b> This article is best viewed in 'light mode'!  <img src="https://raw.githubusercontent.com/FortAwesome/Font-Awesome/6.x/svgs/regular/sun.svg" width="20" height="20"/>

## Challenge
The latest advances in machine learning and artificial intelligence (AI/ML) has opened up new possibilities to improve healthcare outcomes by harnessing the large volumes of data contained in electronic health records (EHRs). However, due to the sensitive nature of the information contained in EHRs, strict data sharing requirements and the need to preserve patient privacy has hindered the development and deployment of AI/ML models across healthcare settings. 

## Solution
Generating synthetic patient data, instead, offers a promising solution to mitigate these risks, although creating realistic data is often very tricky and still an open challenge. In our recent work, led by [Dr. Taha Ceritli](https://eng.ox.ac.uk/people/taha-ceritli/), we have explored how a new state-of-the-art type of generative model, known as Denoising Diffusion Probabilistic Models (DDPMs), could generate more realistic synthetic EHR data beyond existing techniqus, such as well-known Generative Adversarial Networks (GANs). 

<div class="fake-img l-page">
  <img src="/assets/img/diffusion_pipeline.png"  width="1050"/> 
  <figcaption><br><b>An overview of the TabDDPM pipeline</b>: step (1) demonstrates the synthetic data generation process, followed by step (2) where the synthetic data is evaluated based on quality, privacy, utility, and augmentation performance.</figcaption>
</div>


### Denoising Diffusion Probabilistic Models (DDPMs)
Diffusion models are inspired by non-equilibrium thermodynamics, and they learn to generate synthetic data through denoising. Learning by denoising consists of two processes, forwards and reverse, each of which is a Markov Chain:

#### Forward process
In the forward process, random noise is added to the orginal data in a series of time steps $$(t_1, t_2, \ldots, t_n)$$, following $$ q(\mathbf{x}_t|\mathbf{x}_{t-1}) $$, where $$q(\cdot)$$ is a Markovian process that produces the corrupted samples at each $$t$$. Samples at each time step are drawn from a Gaussian distribution, where the mean of the distribution is conditioned on the sample at the previous time step, and the variance of the distribution follows a fixed schedule. At the end of the forward process, the samples become pure noise.

#### Reverse process
During the reverse process, we try to remove the added noise at every time step, beginning with the pure noise distribution (the last step of the forward process). During the reverse process we can only approximate $$q(\mathbf{x}_{t−1}|\mathbf{x}_t)$$, which we do using the conditional probabilities $$p_{\theta}(\mathbf{x}_{t−1}|\mathbf{x}_t)$$, as estimated from our neural network. We then try to denoise each sample backwards from $$(t_n, t_{n-1}, \ldots, t_1)$$ to the original data. 

## Evaluation
Our diffusion model, known as <b>TabDDPM</b> due to its flexibility incorporating tabular- and mixed-type data, was compared on four evaluation criteria: 
1. <b>Data quality</b>: can similar and comparable data be generated?
2. <b>Data privacy</b>: Can the the privacy of original patients be preserved?
3. <b>Data utility</b>: Can synthesized data be useful for downstream predictive models?
4. <b>Data augmentation</b>: Can combining original and synthetic data strengthen the capacity of downstream predictive models?

We found that TabDDPM outperformed many of the state-of-the-art methods on benchmark datasets, except for privacy, highlighting the difficult balance that needs to be maintained when synthesizing EHR. Our the abilty to generate more realistic clinical data comes with the cost of too closly mimicing the unique and confidential characteristics of the original patients. 

We're not there yet, but we hope that our promising results motivates future work exploring how diffusion models could generate realistic healthcare data, without compromising on the privacy considerations of patients. 

## Feedback
This project is still evolving and we welcome any feedback. If you have comments or suggestions, feel free to reach out to myself or [Dr. Taha Ceritli](mailto:taha.ceritli@eng.ox.ac.uk). 
Congratulations to all co-authors, Taha Ceritli, Ghadeer Ghosheh, Vinod Kumar Chauhan, Tingting Zhu and David Clifton. 

## Reference
If you use our work, please consider citing:

```tex
@article{ceritli2023synthesizing,
  title = {Synthesizing Mixed-type Electronic Health Records using Diffusion Models},
  author = {Ceritli, Taha and Ghosheh, Ghadeer O. and Chauhan, Vinod Kumar and Zhu, Tingting and Creagh, Andrew P. and Clifton, David A.},
  doi = {https://doi.org/10.48550/arxiv.2302.14679},
  url = {https://arxiv.org/abs/2302.14679},
  publisher = {arXiv},
  year = {2023},
}

```
