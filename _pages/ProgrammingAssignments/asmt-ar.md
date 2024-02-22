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

## Starter Code

Here is an example for how to detect the ArUCo Pantone Color Cards:

```python
# https://www.pyimagesearch.com/2021/01/04/opencv-augmented-reality-ar/
# pip install opencv-contrib-python imutils

import numpy as np
import argparse
import imutils
import sys
import cv2

# construct the argument parser and parse the arguments
ap = argparse.ArgumentParser()
ap.add_argument("-s", "--source", required=True,
	help="path to input source image that will be put on input")
args = vars(ap.parse_args())

cap = cv2.VideoCapture(0)
#cap = cv2.VideoCapture(0,cv2.CAP_DSHOW)
#cap.set(cv2.CAP_PROP_FRAME_WIDTH, 1920)
#cap.set(cv2.CAP_PROP_FRAME_HEIGHT, 1080)
ret, image = cap.read()

source = cv2.imread(args["source"])

while True:
    ret, image = cap.read()
    
    #image = imutils.resize(image, width=600)
    (imgH, imgW) = image.shape[:2]  
    
    # load the ArUCo dictionary, grab the ArUCo parameters, and detect
    # the markers
    print("[INFO] detecting markers...")
    arucoDict = cv2.aruco.getPredefinedDictionary(cv2.aruco.DICT_ARUCO_ORIGINAL)
    arucoParams =  cv2.aruco.DetectorParameters()
    arucoParams.cornerRefinementMethod = cv2.aruco.CORNER_REFINE_NONE # speed up detection at the cost of precision
    detector = cv2.aruco.ArucoDetector(arucoDict, arucoParams)
    corners, ids, rejected = detector.detectMarkers(image)

    # show the found markers
    cv2.aruco.drawDetectedMarkers(image, corners)

    # if we have not found four markers in the input image then we cannot
    # apply our augmented reality technique
    if len(corners) != 4:
        print("[INFO] could not find 4 corners; found {}... press any key to continue or q to quit".format(str(len(corners))))
        cv2.imshow("Input", image)
        key = cv2.waitKey(1) & 0xFF # 3 ms pause
        if key == ord('q'):
            sys.exit(0)
        else:
            continue
        
    # otherwise, we've found the four ArUco markers, so we can continue
    # by flattening the ArUco IDs list and initializing our list of
    # reference points
    print("[INFO] constructing augmented reality visualization...")
    ids = ids.flatten()
    refPts = []
    # loop over the IDs of the ArUco markers in top-left, top-right,
    # bottom-right, and bottom-left order
    for i in (923, 1001, 241, 1007):
        # grab the index of the corner with the current ID and append the
        # corner (x, y)-coordinates to our list of reference points
        j = np.squeeze(np.where(ids == i))
        corner = np.squeeze(corners[j])
        refPts.append(corner)  

    # unpack our ArUco reference points and use the reference points to
    # define the *destination* transform matrix, making sure the points
    # are specified in top-left, top-right, bottom-right, and bottom-left
    # order
    (refPtTL, refPtTR, refPtBR, refPtBL) = refPts
    dstMat = [refPtTL[0], refPtTR[1], refPtBR[2], refPtBL[3]]
    dstMat = np.array(dstMat)
    # grab the spatial dimensions of the source image and define the
    # transform matrix for the *source* image in top-left, top-right,
    # bottom-right, and bottom-left order
    (srcH, srcW) = source.shape[:2]
    srcMat = np.array([[0, 0], [srcW, 0], [srcW, srcH], [0, srcH]])
    # compute the homography matrix and then warp the source image to the
    # destination based on the homography
    (H, _) = cv2.findHomography(srcMat, dstMat)
    warped = cv2.warpPerspective(source, H, (imgW, imgH))

    # construct a mask for the source image now that the perspective warp
    # has taken place (we'll need this mask to copy the source image into
    # the destination)
    mask = np.zeros((imgH, imgW), dtype="uint8")
    cv2.fillConvexPoly(mask, dstMat.astype("int32"), (255, 255, 255),
        cv2.LINE_AA)
    # this step is optional, but to give the source image a black border
    # surrounding it when applied to the source image, you can apply a
    # dilation operation
    rect = cv2.getStructuringElement(cv2.MORPH_RECT, (3, 3))
    mask = cv2.dilate(mask, rect, iterations=2)
    # create a three channel version of the mask by stacking it depth-wise,
    # such that we can copy the warped source image into the input image
    maskScaled = mask.copy() / 255.0
    maskScaled = np.dstack([maskScaled] * 3)
    # copy the warped source image into the input image by (1) multiplying
    # the warped image and masked together, (2) multiplying the original
    # input image with the mask (giving more weight to the input where
    # there *ARE NOT* masked pixels), and (3) adding the resulting
    # multiplications together
    warpedMultiplied = cv2.multiply(warped.astype("float"), maskScaled)
    imageMultiplied = cv2.multiply(image.astype(float), 1.0 - maskScaled)
    output = cv2.add(warpedMultiplied, imageMultiplied)
    output = output.astype("uint8")    
    
    # show the source image, output of our augmented reality
    cv2.imshow("Input", image)
    cv2.imshow("Source", source)
    cv2.imshow("OpenCV AR Output", output)
    print("press any key to continue or q to quit")
    key = cv2.waitKey(1) & 0xFF
    if key == ord('q'):
        sys.exit(0)
    else:
        continue
```
