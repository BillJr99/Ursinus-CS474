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
