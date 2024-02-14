---
layout: assignment
permalink: /Assignments/Programming/EyeTracking
title: "CS474: Human Computer Interaction - Eye Tracking"


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

## Analyzing Eye Movements

There are a few possible approaches to detecting eye movements using the example we considered in class (reproduced below from [https://gist.githubusercontent.com/vardanagarwal/6e0d62f244d9d3280379689499bf990c/raw/7505fedc8cfaefbc8f26d8b6f506e2c66e2873ec/eye_tracking.py](https://gist.githubusercontent.com/vardanagarwal/6e0d62f244d9d3280379689499bf990c/raw/7505fedc8cfaefbc8f26d8b6f506e2c66e2873ec/eye_tracking.py)):

```python
import cv2
import dlib
import numpy as np

def shape_to_np(shape, dtype="int"):
	# initialize the list of (x, y)-coordinates
	coords = np.zeros((68, 2), dtype=dtype)
	# loop over the 68 facial landmarks and convert them
	# to a 2-tuple of (x, y)-coordinates
	for i in range(0, 68):
		coords[i] = (shape.part(i).x, shape.part(i).y)
	# return the list of (x, y)-coordinates
	return coords

def eye_on_mask(mask, side):
    points = [shape[i] for i in side]
    points = np.array(points, dtype=np.int32)
    mask = cv2.fillConvexPoly(mask, points, 255)
    return mask

def contouring(thresh, mid, img, right=False):
    cnts, _ = cv2.findContours(thresh, cv2.RETR_EXTERNAL,cv2.CHAIN_APPROX_NONE)
    try:
        cnt = max(cnts, key = cv2.contourArea)
        M = cv2.moments(cnt)
        cx = int(M['m10']/M['m00'])
        cy = int(M['m01']/M['m00'])
        if right:
            cx += mid
        cv2.circle(img, (cx, cy), 4, (0, 0, 255), 2)
    except:
        pass

detector = dlib.get_frontal_face_detector()
predictor = dlib.shape_predictor('shape_68.dat')

left = [36, 37, 38, 39, 40, 41]
right = [42, 43, 44, 45, 46, 47]

cap = cv2.VideoCapture(0)
ret, img = cap.read()
thresh = img.copy()

cv2.namedWindow('image')
kernel = np.ones((9, 9), np.uint8)

def nothing(x):
    pass
cv2.createTrackbar('threshold', 'image', 0, 255, nothing)

while(True):
    ret, img = cap.read()
    gray = cv2.cvtColor(img, cv2.COLOR_BGR2GRAY)
    rects = detector(gray, 1)
    for rect in rects:

        shape = predictor(gray, rect)
        shape = shape_to_np(shape)
        mask = np.zeros(img.shape[:2], dtype=np.uint8)
        mask = eye_on_mask(mask, left)
        mask = eye_on_mask(mask, right)
        mask = cv2.dilate(mask, kernel, 5)
        eyes = cv2.bitwise_and(img, img, mask=mask)
        mask = (eyes == [0, 0, 0]).all(axis=2)
        eyes[mask] = [255, 255, 255]
        mid = (shape[42][0] + shape[39][0]) // 2
        eyes_gray = cv2.cvtColor(eyes, cv2.COLOR_BGR2GRAY)
        threshold = cv2.getTrackbarPos('threshold', 'image')
        _, thresh = cv2.threshold(eyes_gray, threshold, 255, cv2.THRESH_BINARY)
        thresh = cv2.erode(thresh, None, iterations=2) #1
        thresh = cv2.dilate(thresh, None, iterations=4) #2
        thresh = cv2.medianBlur(thresh, 3) #3
        thresh = cv2.bitwise_not(thresh)
        contouring(thresh[:, 0:mid], mid, img)
        contouring(thresh[:, mid:], mid, img, True)
        # for (x, y) in shape[36:48]:
        #     cv2.circle(img, (x, y), 2, (255, 0, 0), -1)
    # show the image with the face detections + facial landmarks
    cv2.imshow('eyes', img)
    cv2.imshow("image", thresh)
    if cv2.waitKey(1) & 0xFF == ord('q'):
        break
    
cap.release()
cv2.destroyAllWindows()
```

### Tracing Eye Center Movement over Time

You can call the function below from your processing loop, which will return an array of numbers representing the x and y coordinate of the detected center of the eye gaze.  This gaze is defined as the mean of the predicted left and right eye positions.

You could store this value in each iteration, and compare it to the value you observed in the prior iteration.  If the x or y coordinate has increased or decreased, you can infer that the eye gaze has moved up or down the screen.  You might play with the thresholds by which these values have changed: for example, you wouldn't want to decide that the eye has moved up the screen if the pixel value changed by 1 or 2.  You can experiment with a threshold value for this purpose.

Your predictions won't be perfect, so don't expect perfection!  Rather, experiment with different possibilities and document what you find.

```python
def get_eye_center(shape, left, right):
    # Calculate the center of the left eye
    left_eye_center = np.mean(shape[left], axis=0).astype(int)
    # Calculate the center of the right eye
    right_eye_center = np.mean(shape[right], axis=0).astype(int)
    # Calculate the midpoint between the two eyes
    eye_center = ((left_eye_center[0] + right_eye_center[0]) // 2, 
                  (left_eye_center[1] + right_eye_center[1]) // 2)
    return eye_center # [0] is x coordinate, [1] is y coordinate
```    

### Measuring Relative Eye Contour Brightness

Another approach is to compare the detected eye brightness on the left side of the eye versus the right side (and the top versus the bottom).  The briger portion of the eye indicates that more of that part of the eye was detected and visible, and thus you are looking in the opposite direction.  Here is a function you can call from your loop to do this:

```python
def analyze_gaze_direction(eye_region):
    # Split the eye region into left and right for horizontal analysis
    h, w = eye_region.shape[:2]
    left_side = eye_region[:, 0:w//2]
    right_side = eye_region[:, w//2:]
    
    # Split the eye region into upper and lower for vertical analysis
    upper_side = eye_region[0:h//2, :]
    lower_side = eye_region[h//2:, :]
    
    # Calculate the average brightness of each section
    left_brightness = np.mean(left_side)
    right_brightness = np.mean(right_side)
    upper_brightness = np.mean(upper_side)
    lower_brightness = np.mean(lower_side)
    
    # Determine the horizontal direction based on brightness
    horizontal_direction = "left" if left_brightness > right_brightness else "right"
    
    # Determine the vertical direction based on brightness
    vertical_direction = "up" if upper_brightness > lower_brightness else "down"
    
    print(f"Looking {vertical_direction} and {horizontal_direction}")

    return vertical_direction, horizontal_direction
```

You can pass `eyes` or `eyes_grey` to this function for the color or greyscale contours, respectively..  You could use either or both of these in tandem, or something else entirely!  Experimentation is the important thing here.

## Mirroring your Webcam

If (and only if) you need to mirror your webcam horizontally using OpenCV, you can add this line:

```python
img = cv2.flip(img, 1) # 1 = flip horizontally
```

after:

```python
ret, img = cap.read()
```

The second parameter to `flip` indicates how to flip:

* 0: Flips around the x-axis (vertical flip).
* > 0: Flips around the y-axis (horizontal flip).
* < 0: Flips around both axes.

## Printing Words to the Screen

You can display words on the screen using OpenCV with the following code.  You can make this into a function and call it from your processing loop (perhaps before you check the eye position):

```python
import numpy as np
import cv2

# Create a blank canvas (image) of size 800x600 with 3 channels (RGB), filled with black (0)
canvas = np.zeros((600, 800, 3), dtype="uint8")

# Text properties
text = "Hello, World!"
font = cv2.FONT_HERSHEY_SIMPLEX  # Font type
font_scale = 1.5  # Font scale (size)
thickness = 3  # Thickness of the text

# Color and location
color = (0, 255, 0)  # Text color in BGR (green)
position = (50, 300)  # Bottom-left corner of the text in the canvas

# Draw
cv2.putText(canvas, text, position, font, font_scale, color, thickness)

# Show 
cv2.imshow("Canvas with Text", canvas)
cv2.waitKey(0)
cv2.destroyAllWindows()
```

If you are timing eye movements to a certain location, you can use `time.time()` after importing the `time` package to take the time before displaying the window to the time your processing loop detects the presence of the eyes in that quadrant, or you can time this manually.