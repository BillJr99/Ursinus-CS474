---
layout: assignment
permalink: /Assignments/Programming/AugmentedReality
title: "CS474: Human Computer Interaction - Augmented Reality"


info:
  coursenum: CS474
  points: 100
  goals:
    - To write a program that uses augmented reality to display dynamic educational material
    - To use opencv to create a dynamic image and display it as an AR overlay
  rubric:
    - weight: 20 
      description: Human-Centric Design
      preemerging: A trivial application of the modality is provided without regard to proper signifiers or affordances to facilitate human interaction
      beginning: Some consideration is given to the manner by which augmented reality is incorporated into the program, but it is not clear at all times to the user what to do and how to interact
      progressing: The user is able to interact with the program using augmented reality in most cases, with a few minor ambiguities that could be identified through additional testing
      proficient: The user experience is enhanced by the use of augmented reality
    - weight: 20
      description: Design Report      
      preemerging: No design report is included
      beginning: A design report is included that describes the approach taken to solving the problem and incorporating augmented reality in a trivial way
      progressing: A design report is included that describes the approach taken to solving the problem and incorporating augmented reality in a manner that carefully considers the problem from the perspective of one stakeholder
      proficient: A design report is included that describes the approach taken to solving the problem and incorporating augmented reality through documented discussions and test cases with a variety of stakeholders
    - weight: 30
      description: Algorithm Implementation
      preemerging: The algorithm fails on the test inputs due to major issues, or the program fails to compile and/or run
      beginning: The algorithm fails on the test inputs due to one or more minor issues
      progressing: The algorithm is implemented to solve the problem correctly according to given test inputs, but would fail if executed in a general case due to a minor issue or omission in the algorithm design or implementation
      proficient: A reasonable algorithm is implemented to solve the problem which correctly solves the problem according to the given test inputs, and would be reasonably expected to solve the problem in the general case
    - weight: 20
      description: Code Quality and Documentation
      preemerging: Code commenting and structure are absent, or code structure departs significantly from best practice, and/or the code departs significantly from the style guide
      beginning: Code commenting and structure is limited in ways that reduce the readability of the program, and/or there are minor departures from the style guide
      progressing: Code documentation is present that re-states the explicit code definitions, and/or code is written that mostly adheres to the style guide
      proficient: Code is documented at non-trivial points in a manner that enhances the readability of the program, and code is written according to the style guide
    - weight: 10
      description: Writeup and Submission
      preemerging: An incomplete submission is provided
      beginning: The program is submitted, but not according to the directions in one or more ways (for example, because it is lacking a readme writeup or missing answers to written questions)
      progressing: The program is submitted according to the directions with a minor omission or correction needed, including a readme writeup describing the solution and answering nearly all questions posed in the instructions
      proficient: The program is submitted according to the directions, including a readme writeup describing the solution and answering all questions posed in the instructions
  readings:
    - rtitle: "Modalities - Augmented Reality Activity"
      rlink: "../../Activities/AugmentedReality"
    - rlink: "https://www.pyimagesearch.com/2021/01/04/opencv-augmented-reality-ar/"
      rtitle: "Rosebrock, A. - OpenCV Augmented Reality (AR)"
    - rtitle: "Creating your own image using numpy and opencv"
      rlink: "https://theailearner.com/2018/10/22/create-own-image-using-numpy-and-opencv/"
    - rtitle: "Drawing Functions in OpenCV"
      rlink: "https://docs.opencv.org/4.x/dc/da5/tutorial_py_drawing_functions.html"
    - rtitle: "Tracking ArUCo Markers"
      rlink: "https://aliyasineser.medium.com/aruco-marker-tracking-with-opencv-8cb844c26628"
tags:
  - modalities
  - eyetracking
  
---

In this assignment, you will incorporate [the augmented reality](../../Activities/AugmentedReality) program we explored in class into a user application.  Specifically, you will write a program to solve one of two problems:

* Wireless hotspot locations and relative signal strengths
* A scavanger hunt / capture the flag game on campus using clues and hot/cold markers to inform the user

For your application, detect a particular marker on the screen (if you like, you can use a marker other than the default ArUCo dictionary, or overlay your information over the entire screen without a marker), and create a dynamic image to display meaningful information on the webcam overlay.

In addition to your implementation, be sure to include a LaTeX design report in academic journal format (you can use [Overleaf](https://www.overleaf.com/) for this purpose) that describes your initial design, rationale, stakeholder evaluation, and any subsequent revisions you made from your stakeholder input.
