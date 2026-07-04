---
layout: activity
permalink: /Activities/AugmentedReality
title: "CS474: Human Computer Interaction - Augmented Reality"


info: 
  goals: 
    - To present information on a graphical overlay using the <code>opencv</code> library
    - To facilitate the dynamic presentation of unobtrusive information in one's field of vision
  additional_reading:
    - link: "https://www.pyimagesearch.com/2021/01/04/opencv-augmented-reality-ar/"
      title: "Rosebrock, A. - OpenCV Augmented Reality (AR)"    
    - link: "https://medium.com/thrive-global/how-technology-hijacks-peoples-minds-from-a-magician-and-google-s-design-ethicist-56d62ef5edf3"
      title: "How Technology is Hijacking Your Mind — from a Magician and Google Design Ethicist"
  models:
    - model: |
        <iframe src="https://www.pyimagesearch.com/2021/01/04/opencv-augmented-reality-ar/" width="100%" height="800"></iframe>  
      title: Augmented Reality
      questions:
        - "What sensors might you detect to display information about your surroundings, such as available wifi signals, or the location of a particular building on campus?"
        - "How might you modify this to use a different detector marker?"
        - "How might you modify this to display a dynamic image?"
        - "What are some ways in which people's actions are influenced by the deliberate manipulation of information visualizations from your own experience?"

tags:
  - ar
  
---

## Try It: The Math Behind AR Overlays

How does an AR app make a virtual card look "glued" to a real surface?  The answer is a 3x3 matrix called a homography.  This notebook computes one from four corner points using plain `numpy` — the same computation `cv2.findHomography` performs — and warps an overlay into a simulated camera frame, so you can see exactly what OpenCV will do for you in the programming assignment.

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/BillJr99/Ursinus-CS474/blob/gh-pages/files/notebooks/ar_overlay_math.ipynb)

Click the badge to run the notebook in your browser with Google Colab (no installation required), or [download the notebook]({{ site.baseurl }}/files/notebooks/ar_overlay_math.ipynb) to run it locally with Jupyter.

## Explore Further

- [Apple Human Interface Guidelines - Augmented Reality](https://developer.apple.com/design/human-interface-guidelines/augmented-reality) — production design guidance for AR; note how many rules concern *not* obstructing the user's view, echoing this activity's goal of unobtrusive information.
- [Google - ARCore Design Guidelines](https://developers.google.com/ar/design) — Google's counterpart, with concrete advice on onboarding users into AR and providing signifiers for interactions that have no physical affordance.
