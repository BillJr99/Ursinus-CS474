---
layout: assignment
permalink: /Assignments/Programming/VoicePrompt
title: "CS474: Human Computer Interaction - Voice Prompts"


info:
  coursenum: CS474
  points: 100
  goals:
    - To write a program that uses voice prompts for engagement
    - To consider the affordances and signifiers necessary to implement a voice system
    - To consider and mitigate the accessibility challenges when combining voice and text interaction    
  rubric:
    - weight: 20 
      description: Human-Centric Design
      preemerging: A trivial application of the modality is provided without regard to proper signifiers or affordances to facilitate human interaction
      beginning: Some consideration is given to the manner by which a voice modality is incorporated into the program, but it is not clear at all times to the user what to do and how to interact
      progressing: The user is able to interact with the program using the voice modality in most cases, with a few minor ambiguities that could be identified through additional testing
      proficient: A first-time user can complete the primary task end-to-end using speech alone; every prompt makes clear when to speak and what kinds of responses are expected, recognition errors are detected and re-prompted rather than crashing or silently misfiring, and at least one outside tester's session is documented in the writeup
    - weight: 20
      description: Design Report      
      preemerging: No design report is included
      beginning: A design report is included that describes the approach taken to solving the problem and incorporating the voice modality in a trivial way
      progressing: A design report is included that describes the approach taken to solving the problem and incorporating the voice modality in a manner that carefully considers the problem from the perspective of one stakeholder
      proficient: A design report is included that describes the approach taken to solving the problem and incorporating the voice modality through documented discussions and test cases with a variety of stakeholders
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
    - rtitle: "Modalities - Voice Prompt Activity"
      rlink: "../../Activities/VoicePrompt"
    - rtitle: "ReadSpeaker Debuts Voice User Interface Platform for Nintendo Switch"
      rlink: "https://voicebot.ai/2021/11/16/readspeaker-debuts-voice-user-interface-platform-for-nintendo-switch/"
      
tags:
  - modalities
  - voiceprompt
  
---
## Purpose, Task, and Criteria

**Purpose.**  This assignment builds three skills you will reuse all semester: designing for a modality with *no visual signifiers* (every affordance must be communicated in sound and timing), handling the inevitable errors of a probabilistic input channel gracefully, and running and documenting stakeholder tests of your own design.  These are the same skills your final project's design report will be graded on.

**Task.**  Choose one of the two problems below and implement it as a voice-only application in Python, using the speech recognition and text-to-speech example from the class activity as your starting point.  Accompany the program with a LaTeX design report documenting your design rationale and stakeholder testing.

**Criteria.**  Your work is assessed with the rubric above.  Concretely, a strong submission is one where a classmate who has never seen your program can complete the task by voice alone, and your report shows how testing changed your design.  The milestones at the end of this page describe what should be working at each checkpoint along the way.


In this assignment [[^1]], you will incorporate the [Speech Recognition for Voice Prompts](../../Activities/VoicePrompt) program we explored in class into a user application.  **Be sure to use the first version of this program, which does not run a thread in the background, so that you can continue interacting with the user after processing one iteration of speech**.  Specifically, you will write a program to solve one of two problems:

* Find a common time to meet with a group of people, given a text file containing their weekly availabilities
* Play a role-playing game in which users explore a maze of connected rooms (use a dictionary or hash table structure to manage your collection of rooms), encounter conflicts, and obtain treasure

Your solution should utilize only a voice modality.  In other words, no text should be displayed to the screen (or, if it is, it should not be relied upon by the user to operate the program).  Careful consideration should be given to the workflow of the use case: I suggest creating a flowchart prior to implementing your solution that describes what, how, and when you will obtain feedback from the user at each step in your program.  The goal is to create a seamless experience for the user without requiring a keyboard, mouse, or visual cues.  Specifically, there are a few considerations that you should keep in mind and document:

* How will you indicate to the user that you are ready for some kind of response?  What clear, consise prompts would you give to the user at particular points in the program?
* How will you handle speech recognition errors?  The library we are using allows for probabilistic translation, which you should use to try to automatically resolve ambiguities, but it would be good to re-prompt the user and verify information at each step (especially if the translation has a low confidence).
* The speech recognition software might pick up its own prompts during recognition: how might you address this?
* How should you configure the speech recognition library with appropriate delays to pick up your user's responses, given your expectation of the duration of their input?

I strongly recommend running your program with your classmates to obtain feedback.  Pay particular attention to the way in which they use the program, and look for "mistakes" that they make along the way.  Don't tell them anything, but consider instead that these "mistakes" may be ambiguities in your program that you can address.  Obtain feedback from them at the end, and document and consider it in any revisions you might make.

In addition to your implementation, be sure to include a LaTeX design report in academic journal format (you can use [Overleaf](https://www.overleaf.com/) for this purpose) that describes your initial design, rationale, stakeholder evaluation, and any subsequent revisions you made from your stakeholder input.

## Scrutinizing the Code Example

The code example to get started is reproduced below; however, it features several protocol issues that you will want to experiment with (among others!).  For example, should certain code be executing where it is to set various thresholds?  Should you be more judicious about catching exceptions so that the program does not quit over a trivial error?  How can you use the return values (and potential return values) of these functions to help determine what the user said?  How might you create a generic function to prompt the user in a natural way, and confirm their response every time?  How will you handle small mistakes in what you hear?  The goal is not to aim for perfection, but rather to experiment with many different ideas, to observe their results, and to document the process.

```python
        # https://github.com/acgrissom/courses/blob/master/2020-hci/hw1_voiceui.md
        # https://github.com/acgrissom/courses/blob/master/2020-hci/code/recognize_speech.py
        # on linux: sudo apt install portaudio19-dev libespeak-dev libespeak1
        # on mac: brew install portaudio
        # on linux/windows: pip3 install git+https://github.com/BillJr99/pyttsx3.git
        # on mac: pip3 install py3-tts (pip3 install pyobjc followed by pyttsx3 might also work)
        # pip3 install pyaudio speechrecognition disutils setuptools
        # alternatively: pip3 install pipwin pypiwin32 && python -m pipwin install pyaudio
        # Install Visual C++ Tools on Windows https://visualstudio.microsoft.com/visual-cpp-build-tools/
          
        import speech_recognition as sr
        import pyttsx3
        import sys
        import time
          
        tts = pyttsx3.init() # pass 'dummy' to this constructor if this call fails due to a lack of voice drivers (but will disable speech)
          
        def speak(tts, text):
            tts.say(text)
            tts.runAndWait()
          
        def main():
            # get audio from the microphone                                                                       
            listener = sr.Recognizer()                                                                                   
            with sr.Microphone() as source:
                listener.adjust_for_ambient_noise(source) # used to detect silence to stop listening after a phrase is spoken
                while True:
                    print("Listening.")
                    speak(tts, "listening") # how do we prevent this from being spoken every time an exception is thrown?
                    time.sleep(1) # used to prevent hearing any spoken text; what else could we do?
                    user_input = None
                    sys.stdout.write(">")
                    #record audio
                    listener.pause_threshold = 0.5 # how long, in seconds, to observe silence before processing what was heard
                    audio = listener.listen(source, timeout=5) #, timeout = N throws an OSError after N seconds if nothing is heard.  can also call listen_in_background(source, callback) and specify a function callback that accepts the recognizer and the audio when data is heard via a thread
                    try:
                        #convert audio to text
                        #user_input = listener.recognize_sphinx(audio) #requires PocketSphinx installation
                        user_input = listener.recognize_google(audio, show_all = False) # set show_all to True to get a dictionary of all possible translations
          
                        print(user_input)
                        speak(tts, user_input)
                    except sr.UnknownValueError:
                        print("Could not understand audio")
                    except sr.RequestError as e:
                        print("Could not request results; {0}".format(e))
                    except OSError:
                        print("No speech detected")
                          
                    sys.stdout.write("\n")
          
          
        if __name__ == "__main__":
            main()
```

[^1]: Adapted from Dr. Alvin Grissom's 2020 HCI course

## Getting Started

Don't start by writing your application - start by making the pipeline work, then grow it:

1. **Run the class example unmodified.**  Get the microphone, recognizer, and text-to-speech working on your machine first (the install commands are in the comments at the top of the example).  Debugging your environment and your design at the same time is miserable; separate them.
2. **Sketch the conversation.**  Draw the flowchart of your whole interaction *before* coding it: every prompt the system speaks, every response class you expect, and what happens on a misrecognition at each step.  This flowchart becomes a figure in your design report.
3. **Wrap the messy parts in one function.**  Write a helper like `ask(prompt_text) -> str` that speaks the prompt, listens, handles the three exception types, and re-prompts on failure.  Add a `confirm(value) -> bool` helper next.  Your application logic should never call the recognizer directly.
4. **Build the logic with a keyboard stub.**  Temporarily implement `ask` with `input()` so you can build and test your scheduling or maze logic quickly; swap the voice implementation back in once the logic works.  (The finished program must be voice-only - the stub is scaffolding, not the product.)
5. **Test with a human early.**  Even a two-minute hallway test after Checkpoint 2 will reveal prompts that made sense only to you.

## Milestones

Pace yourself against these checkpoints; each is an observable state of your program, not a promise:

- **Checkpoint 1 (end of the first few days): the pipeline works.**  The unmodified class example runs on your machine: it hears you, prints what you said, and speaks it back.  You have chosen your problem and drafted your conversation flowchart.
- **Checkpoint 2 (roughly halfway): the application works, the voice layer works - separately.**  Your core logic (finding a common meeting time, or navigating the room graph) runs correctly with the keyboard stub, and your `ask`/`confirm` helpers work reliably in isolation, including re-prompting after a deliberate mumble.
- **Checkpoint 3 (several days before the deadline): end-to-end by voice.**  The full task can be completed without keyboard, mouse, or screen.  You have run at least one classmate through it, recorded what confused them, made at least one revision, and drafted the design report.  The remaining days are for polish, not construction.
