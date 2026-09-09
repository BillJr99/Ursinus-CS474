---
layout: activity
permalink: /Activities/Bias
title: "CS474: Human Computer Interaction - Bias in Design"


info: 
  goals: 
    - To identify potential blind spots in design and their underlying cause
    - To identify methods to mitigate these blind spots
  additional_reading:
    - link: "https://www.interaction-design.org/literature/article/the-bias-blind-spot-and-unconscious-bias-in-design"
      title: "The Bias Blind Spot and Unconscious Bias in Design"  
    - link: "https://edition.pagesuite.com/popovers/dynamic_article_popover.aspx?artguid=96716b03-dbbf-43e2-988d-5905d1a1167c&appid=1165"
      title: "Color blind? Artificial intelligence could improve the treatment of breast cancer, but there are worries it might worsen disparities"       
  models:
    - model: |
        <a href="https://www.bbc.com/news/science-environment-34910954"><img src="https://ichef.bbci.co.uk/news/976/cpsprodpb/126CF/production/_86917457_surgeon_dilemma-03.jpg" alt="A slide in which a surgeon says that they are about to operate on their son."></a>
      title: Unconscious Bias
      questions:
        - "Can you think of examples of unconscious bias that are beneficial from an evolutionary perspective?"
        - "How might AI be trained to recognize certain groups of people, and what real-world consequences can you think of?"
        - "What can we do to mitigate our unconscious bias, given that we can't necessarily identify them all specifically?"

tags:
  - bias
  
---

## Try It: Measuring Bias with Fairness Metrics

Bias in a system is not just a feeling — it can be measured.  This notebook builds a small simulated resume-screening dataset in which a historical process disadvantaged one group, then computes the standard fairness metrics used in real audits: selection rates, demographic parity, the four-fifths (80%) rule, and equal opportunity.  Along the way you'll see why a model that "never sees" a group attribute can still discriminate through proxies.

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/BillJr99/Ursinus-CS474/blob/gh-pages/files/notebooks/bias_fairness_metrics.ipynb)

Click the badge to run the notebook in your browser with Google Colab (no installation required), or [download the notebook](https://www.billmongan.com/Ursinus-CS474-Spring2024/files/notebooks/bias_fairness_metrics.ipynb) to run it locally with Jupyter.

## Explore Further

- [ProPublica - Machine Bias](https://www.propublica.org/article/machine-bias-risk-assessments-in-criminal-sentencing) — the landmark investigation of the COMPAS recidivism-risk tool; a concrete case where the fairness definitions in the notebook (calibration vs. equal error rates) mathematically conflict.
- [Gender Shades (Buolamwini & Gebru, 2018)](http://gendershades.org/) — an audit showing commercial face-analysis systems performed far worse on darker-skinned women; the interactive site summarizes the paper visually and in text.
- [Google - People + AI Guidebook](https://pair.withgoogle.com/guidebook/) — practical design patterns for building AI-backed interfaces that make model limitations and confidence visible to users, one mitigation for the "rubber-stamping" problem explored in the notebook.
