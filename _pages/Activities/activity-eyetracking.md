---
layout: activity
permalink: /Activities/EyeTracking
title: "CS474: Human Computer Interaction - Modalities - Eye Tracking"


info: 
  goals: 
    - To identify alternative modalities for human-computer interaction
    - To write a program that uses eye tracking for engagement
    - To identify signifiers and affordances for a given application and modality
  additional_reading:
    - link: "https://medium.com/@stepanfilonov/tracking-your-eyes-with-python-3952e66194a6"
      title: "Filonov, S. - Tracking your eyes with Python"
    - link: "https://towardsdatascience.com/real-time-eye-tracking-using-opencv-and-dlib-b504ca724ac6"
      title: "Argawal, V. - Real-time eye tracking using OpenCV and Dlib"
    - link: "https://github.com/opencv/opencv/tree/master/data/haarcascades"
      title: "Haar Cascade Training Data"
    - link: "http://dlib.net/files/"
      title: "dlib shape68 training files"
    - link: "https://cmake.org/download/"
      title: "CMake dependency download"
  models:
    - model: |
        Download the <a href="https://visualstudio.microsoft.com/visual-cpp-build-tools/">Visual Studio installer</a> and install the "Desktop Development for C++" module.
        <br>
        <code>pip install cmake wheel dlib opencv-python face_recognition numpy</code>
        <br>
        Alternatively: <code>git clone https://github.com/davisking/dlib.git && cd dlib && python setup.py install --user --no DLIB_GIF_SUPPORT</code>
        <script src="https://gist.github.com/vardanagarwal/6e0d62f244d9d3280379689499bf990c.js"></script> 
        <br>
        <script src="https://emgithub.com/embed.js?target=https%3A%2F%2Fgithub.com%2Fstepacool%2FEye-Tracker%2Fblob%2FNo_GUI%2Ftrack.py&style=github&showBorder=on&showLineNumbers=on&showFileMeta=on&showCopy=on&fetchFromJsDelivr=on"></script>        
      title: Eye Tracking
      questions:
        - "What kinds of applications can you think of that would benefit from eye tracking?"
        - "How might eye tracking enhance the user experience in applications that might not traditionally incorporate it?  In particular, how might eye tracking applications assist disabled persons using software?"
        - "What are the pros and cons of using a threshold-based detection strategy?  How might you automatically calibrate such a system, and how might you allow it to adapt to changing conditions over time?"

tags:
  - modalities
  - eyetracking
  
---

## Try It: Analyzing Eye Tracking (Gaze) Data

Eye trackers produce a stream of `(x, y)` gaze positions; the interesting part is turning that stream into *fixations*, *scanpaths*, and *heatmaps* that tell us where a user's attention went.  This notebook walks through a classic fixation-detection algorithm (I-DT) and both standard visualizations on synthetic gaze data, so you can experiment even without eye tracking hardware — and it previews the threshold-calibration questions from the models above.

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/BillJr99/Ursinus-CS474/blob/gh-pages/files/notebooks/eyetracking_gaze_analysis.ipynb)

Click the badge to run the notebook in your browser with Google Colab (no installation required), or [download the notebook](https://www.billmongan.com/Ursinus-CS474-Spring2024/files/notebooks/eyetracking_gaze_analysis.ipynb) to run it locally with Jupyter.

## Explore Further

- [WebGazer.js](https://webgazer.cs.brown.edu/) — a Brown University library that does real-time eye tracking with only an ordinary webcam, right in the browser.  Try the live demo and notice how much calibration quality affects accuracy — the same threshold/calibration trade-off you'll face in the programming assignment.
- [Salvucci & Goldberg - Identifying Fixations and Saccades in Eye-Tracking Protocols (ETRA 2000)](https://dl.acm.org/doi/10.1145/355017.355028) — the short, readable paper that defines the I-DT algorithm used in the notebook and compares it to velocity-based alternatives.
- [Nielsen Norman Group - F-Shaped Pattern of Reading on the Web](https://www.nngroup.com/articles/f-shaped-pattern-reading-web-content/) — a famous eyetracking finding (with heatmaps like the one you'll build) showing users read web pages in an "F" pattern, and what that implies for where important content should go.
