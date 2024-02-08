---
layout: assignment
permalink: /Assignments/Programming/EyeTracking
title: "CS474: Human Computer Interaction - Eye Tracking"
excerpt: "CS474: Human Computer Interaction - Eye Tracking"

info:
  coursenum: CS474
  points: 100
  goals:
    - To write a program that uses eye tracking for engagement
    - To consider the affordances and signifiers necessary to implement a voice system
    - To consider and mitigate the accessibility challenges when integrating eye tracking for accessibility   
  rubric:
    - weight: 20 
      description: Human-Centric Design
      preemerging: A trivial application of the modality is provided without regard to proper signifiers or affordances to facilitate human interaction
      beginning: Some consideration is given to the manner by which eye tracking is incorporated into the program, but it is not clear at all times to the user what to do and how to interact
      progressing: The user is able to interact with the program using eye tracking in most cases, with a few minor ambiguities that could be identified through additional testing
      proficient: The user experience is enhanced by the use of eye tracking
    - weight: 20
      description: Design Report      
      preemerging: No design report is included
      beginning: A design report is included that describes the approach taken to solving the problem and incorporating eye tracking in a trivial way
      progressing: A design report is included that describes the approach taken to solving the problem and incorporating eye tracking in a manner that carefully considers the problem from the perspective of one stakeholder
      proficient: A design report is included that describes the approach taken to solving the problem and incorporating eye tracking through documented discussions and test cases with a variety of stakeholders
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
    - rtitle: "Modalities - Eye Tracking Activity"
      rlink: "../../Activities/EyeTracking"
    - rlink: "https://medium.com/@stepanfilonov/tracking-your-eyes-with-python-3952e66194a6"
      rtitle: "Filonov, S. - Tracking your eyes with Python"
    - rlink: "https://towardsdatascience.com/real-time-eye-tracking-using-opencv-and-dlib-b504ca724ac6"
      rtitle: "Argawal, V. - Real-time eye tracking using OpenCV and Dlib"
    - rtitle: "What is eye tracking"
      rlink: "https://us.tobiidynavox.com/pages/what-is-eye-tracking"
tags:
  - modalities
  - eyetracking
  
---

In this assignment, you will incorporate [the Eye Tracking](../Activities/EyeTracking) program we explored in class into a user application.  Specifically, you will write a program to solve one of two problems:

* Message Dictation with Eye Tracking: display words on the screen and allow a user to select one by looking at it for some period of time.  Based on the word selected, use a dictionary structure to select a number of appropriate words that could follow that word.  When the user looks at a punctuation mark (for example, a period), the sentence is ended and read aloud via text to speech.
* A game in which words that represent colors are displayed on-screen.  Each word is displayed in a color other than the text of the word (for example, the word RED would appear in blue), except for one word which will match.  Give the user points inversely proportional to the time it took to fixate on the word that correctly matches its color.

Your solution should utilize only eye tracking.  In other words, the keyboard and mouse should not be utilized; however, you can display information on the screen.  Careful consideration should be given to the workflow of the use case: I suggest creating a flowchart prior to implementing your solution that describes what, how, and when you will obtain feedback from the user at each step in your program.  The goal is to create a seamless experience for the user without requiring a keyboard or mouse.  Specifically, there are a few considerations that you should keep in mind and document:

* How will you indicate to the user that you are ready for some kind of response?  What clear, consise prompts would you give to the user at particular points in the program?
* How will you indicate correctness or incorrectness to the user?  How will you verify their actions?

I strongly recommend running your program with your classmates to obtain feedback.  Pay particular attention to the way in which they use the program, and look for "mistakes" that they make along the way.  Don't tell them anything, but consider instead that these "mistakes" may be ambiguities in your program that you can address.  Obtain feedback from them at the end, and document and consider it in any revisions you might make.

In addition to your implementation, be sure to include a LaTeX design report in academic journal format (you can use [Overleaf](https://www.overleaf.com/) for this purpose) that describes your initial design, rationale, stakeholder evaluation, and any subsequent revisions you made from your stakeholder input.
