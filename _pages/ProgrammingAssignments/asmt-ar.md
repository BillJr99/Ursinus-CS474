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

## Example Code for ArUCo Card Detection and Image Overlay

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
ret, image = cap.read()

source = cv2.imread(args["source"])

# Initialize a dictionary to store the last known corners for each ArUco marker
cached_corners = {}

while True:
    ret, image = cap.read()
    
    (imgH, imgW) = image.shape[:2]  
    
    print("[INFO] detecting markers...")
    arucoDict = cv2.aruco.getPredefinedDictionary(cv2.aruco.DICT_ARUCO_ORIGINAL)
    arucoParams = cv2.aruco.DetectorParameters()
    corners, ids, rejected = cv2.aruco.detectMarkers(image, arucoDict, parameters=arucoParams)

    cv2.aruco.drawDetectedMarkers(image, corners)
    
    # Update cached corners if new ones are found
    if ids is not None:
        for id_val, corner in zip(ids.flatten(), corners):
            cached_corners[id_val] = corner  # Update or add the corner for this ID
    
    # Check if we have all four required corners in the cache
    all_corners_found = all(id_val in cached_corners for id_val in [923, 1001, 241, 1007])
    
    if all_corners_found:
        # If all corners are found, update 'corners' to use the cached corners in order
        corners = [cached_corners[id_val] for id_val in [923, 1001, 241, 1007]]
        ids = np.array([923, 1001, 241, 1007]).reshape(-1, 1)  # Reshape for compatibility with later code
    else:
        print("[INFO] could not find 4 corners; found {}... press any key to continue or q to quit".format(len(cached_corners)))
        cv2.imshow("Input", image)
        key = cv2.waitKey(1) & 0xFF
        if key == ord('q'):
            break
        continue
    
    # Construct augmented reality visualization only if all corners are found
    print("[INFO] constructing augmented reality visualization...")
    refPts = [np.squeeze(corner) for corner in corners]  # Flatten corner arrays

    # Define the *destination* transform matrix, ensuring points are in the correct order
    dstMat = np.array([refPts[0][0], refPts[1][0], refPts[2][0], refPts[3][0]])

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

## Example Code for Measuring WiFi Signal Strength

Below is starter code to return a dictionary of WiFi names (SSID's) and their signal strengths:

```python
import subprocess
import re
import platform

def get_wifi_info(os_name):
    wifi_info = {}

    # Function to parse Linux Wi-Fi information
    def parse_linux(output):
        networks = {}
        current_ssid = None
        for line in output.split('\n'):
            ssid_match = re.search(r'SSID: (.+)$', line)
            signal_match = re.search(r'signal: (-\d+) dBm', line)
            if ssid_match:
                current_ssid = ssid_match.group(1)
                networks[current_ssid] = None  # Initialize the SSID with no signal strength
            elif signal_match and current_ssid:
                networks[current_ssid] = int(signal_match.group(1))
        return networks

    # Function to parse macOS Wi-Fi information
    def parse_mac(output):
        networks = {}
        lines = output.split('\n')
        for i, line in enumerate(lines):
            if 'SSID' in line:
                ssid = line.split(': ')[1]
                signal_strength = int(re.search(r'(-\d+) dBm', lines[i + 1]).group(1))
                networks[ssid] = signal_strength
        return networks

    # Function to parse Windows Wi-Fi information
    def parse_windows(output):
        networks = {}
        # Windows netsh command has a different output format
        for block in output.split('\n\n'):
            ssid_match = re.search(r'SSID\s+\d+\s+:\s(.+)', block)
            signal_match = re.search(r'Signal\s+:\s(\d+)%', block)
            if ssid_match and signal_match:
                networks[ssid_match.group(1)] = int(signal_match.group(1))  # Assuming % as signal 'strength'
        return networks

    if os_name.lower() == 'linux':
        result = subprocess.run(['nmcli', '-t', 'device', 'wifi', 'list'], capture_output=True, text=True)
        wifi_info = parse_linux(result.stdout)
    elif os_name.lower() == 'mac' or os_name.lower() == 'darwin' or os_name.lower() == 'macos':
        result = subprocess.run(['/System/Library/PrivateFrameworks/Apple80211.framework/Versions/Current/Resources/airport', '-s'], capture_output=True, text=True)
        wifi_info = parse_mac(result.stdout)
    elif os_name.lower() == 'windows':
        result = subprocess.run(['netsh', 'wlan', 'show', 'networks', 'mode=Bssid'], capture_output=True, text=True, shell=True)
        wifi_info = parse_windows(result.stdout)
    else:
        raise ValueError("Unsupported operating system")

    return wifi_info

# Example usage:
os_name = platform.system()  # Automatically detect the OS
wifi_info = get_wifi_info(os_name)
print(wifi_info)
```

## Example Code for Determining the GPS Coordinates Corresponding to Your Location

Below is a function that returns your approximate latitude and longitude if geocoding services are available on your device:

```python
# pip install geocoder
import geocoder

def get_current_location():
    # Attempt to get the user's location using their IP address
    location = geocoder.ip('me')
    
    if location.ok:
        # Return a dictionary containing the latitude and longitude
        return {
            'latitude': location.lat,
            'longitude': location.lng
        }
    else:
        # Return a message indicating that the location could not be determined
        return "Location information is not available."

# Example usage:
print(get_current_location())
```
