---
layout: activity
permalink: /Activities/ExperimentalObservation
title: "CS474: Human Computer Interaction - Experimentally Evaluating UX"


info: 
  goals: 
    - To design experiments to obtain informative feedback from diverse stakeholders to improve the user experience
  additional_reading:
    - link: "http://manoa.hawaii.edu/hci/readings/interactions2010_norman_nielsen.pdf"
      title: "Norman and Nielson - Gestural Interfaces: A Step Backward In Usability"   
    - link: "https://en.wikipedia.org/wiki/A/B_testing#Email_marketing"
      title: "A/B Testing Example"
    - link: "https://www.uxbooth.com/articles/complete-beginners-guide-to-design-research/"
      title: "Complete Beginner's Guide to Design Research"
    - link: false
      title: "Norman Chapter 5"    
  models:
    - model: |
        <img src="../images/uxstudy/uxstudy.jpg" alt="User Experience Study Qualitative and Quantitative Elements">
      title: "Evaluating the User Experience"
      questions:
        - "Whose fault is it when a user fails to use a system properly?"
        - "A tree test presents the user with the workflow steps, one step at a time, and allows the user to progress in a choose-your-adventure style.  What kinds of deficiencies might this kind of study reveal?"
        - "An A/B test evaluates if one call to action is more effective than another.  How might you employ this in a software system to evaluate different user interface designs or workflows?"
        - "What would likely happen in these studies if all the stakeholders in a medical application UX study had the same job title?"
      embed: |
        <iframe src="https://www.billmongan.com/Ursinus-CS474/assets/code-viewer.html?zip=https%3A%2F%2Fraw.githubusercontent.com%2FBillJr99%2FUrsinus-CS474%2Fgh-pages%2Ffiles%2Freplit%2FProportionsHypothesisTest.zip&title=ProportionsHypothesisTest"
          height="600px"
          width="100%"
          scrolling="yes"
          frameborder="no"
          allowfullscreen="true"
          sandbox="allow-scripts allow-same-origin">
        </iframe>
        <br>
        <iframe src="https://www.billmongan.com/Ursinus-CS474/assets/code-viewer.html?zip=https%3A%2F%2Fraw.githubusercontent.com%2FBillJr99%2FUrsinus-CS474%2Fgh-pages%2Ffiles%2Freplit%2FMeansTTest.zip&title=MeansTTest"
          height="600px"
          width="100%"        
          scrolling="yes"
          frameborder="no"
          allowfullscreen="true"
          sandbox="allow-scripts allow-same-origin">
        </iframe>
        
tags:
  - design
  
---

## Try It: Did the Redesign Help?  Analyzing a UX Experiment

Observation tells you *what* goes wrong; experiments tell you whether your fix *helps*.  This notebook analyzes a simulated A/B test of two checkout designs end-to-end: visualizing the distributions, running a t-test, computing an effect size (because "statistically significant" is not the same as "meaningful"), and extending to three designs with an ANOVA.  It is directly reusable for the user experience study in your final project.

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/BillJr99/Ursinus-CS474/blob/gh-pages/files/notebooks/ab_test_analysis.ipynb)

Click the badge to run the notebook in your browser with Google Colab (no installation required), or [download the notebook]({{ site.baseurl }}/files/notebooks/ab_test_analysis.ipynb) to run it locally with Jupyter.

## Explore Further

- [Nielsen Norman Group - Why You Only Need to Test with 5 Users](https://www.nngroup.com/articles/why-you-only-need-to-test-with-5-users/) — the classic (and often misapplied) argument that small qualitative studies find most usability problems; contrast this with the sample sizes the notebook shows you need for *statistical* claims.
- [Nielsen Norman Group - Quantitative vs. Qualitative UX Research](https://www.nngroup.com/articles/quant-vs-qual/) — a short guide to choosing between counting and observing, and why mature UX practice does both.
