---
layout: assignment
permalink: /Assignments/Programming/Tutor
title: "CS474: Human Computer Interaction - An Online Tutor"


info:
  coursenum: CS474
  points: 100
  goals:
    - To write a program that builds habits to serve as an online tutor
  rubric:
    - weight: 20 
      description: Human-Centric Design
      preemerging: A trivial application of the modality is provided without regard to proper signifiers or affordances to facilitate human interaction
      beginning: Some consideration is given to the manner by which the modality is incorporated into the program, but it is not clear at all times to the user what to do and how to interact
      progressing: The user is able to interact with the program using the modality in most cases, with a few minor ambiguities that could be identified through additional testing
      proficient: A first-time user can begin a tutoring session and reach their first success without verbal coaching; the trigger-action-reward-investment loop is identifiable in the running program, and a timed session with at least one outside tester is documented in the writeup
    - weight: 20
      description: Design Report      
      preemerging: No design report is included
      beginning: A design report is included that describes the approach taken to solving the problem and incorporating the modality in a trivial way
      progressing: A design report is included that describes the approach taken to solving the problem and incorporating the modality in a manner that carefully considers the problem from the perspective of one stakeholder
      proficient: A design report is included that describes the approach taken to solving the problem and incorporating the modality through documented discussions and test cases with a variety of stakeholders
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
      
tags:
  - psychology
  
---
## Purpose, Task, and Criteria

**Purpose.**  This assignment asks you to *apply* the psychology we have been studying - triggers, action, variable reward, and investment from Eyal's Hooked model - to a system whose engagement loop serves the user's own goals (learning) rather than exploiting them.  You will practice designing an engagement loop deliberately, measuring engagement empirically, and reflecting on the ethical line between motivating and manipulating.

**Task.**  Build an online tutoring system in the subject of your choice, structured around the Hooked model, and measure how long test users stay engaged.  Accompany the program with a LaTeX design report documenting your strategic use of each psychological mechanism, your stakeholder testing, and your revisions.

**Criteria.**  Your work is assessed with the rubric above.  Concretely, a strong submission has an identifiable trigger-action-reward-investment loop you can point to in the running program, a first-time user who reaches an early success without coaching, and timed test sessions documented in the report.  The milestones at the end of this page describe what should be working at each checkpoint.


In this assignment, you will develop a habit-leveraging online tutoring system.  You may choose your tutoring subject from this non-exhaustive list of possibilities:

* A tutor for Introduction to Java students
* A video game that does not feature text-based signifier instructions
* Learning another language

Utilize the psychological triggers in the Nir Eyal book Hooked to develop your system, and document your strategic approach.  Test your program with classmates and time how long they are incentivized to remain in the system.

I strongly recommend running your program with your classmates to obtain feedback.  Pay particular attention to the way in which they use the program, and look for "mistakes" that they make along the way.  Don't tell them anything, but consider instead that these "mistakes" may be ambiguities in your program that you can address.  Obtain feedback from them at the end, and document and consider it in any revisions you might make.

In addition to your implementation, be sure to include a LaTeX design report in academic journal format (you can use [Overleaf](https://www.overleaf.com/) for this purpose) that describes your initial design, rationale, stakeholder evaluation, and any subsequent revisions you made from your stakeholder input.

## Getting Started

Design the psychology first; the code follows from it:

1. **Map the Hooked loop on paper.**  For your chosen subject, write one sentence for each stage: What *trigger* brings the learner back (and is it external or internal)?  What is the smallest *action* they take?  What is *variably rewarding* about the feedback (vary the reward, not just the schedule - consider rewards of the tribe, the hunt, and the self)?  What *investment* do they make that improves the next session?  This table goes straight into your design report.
2. **Build a content bank.**  A dozen questions/exercises with answers, difficulty levels, and encouraging feedback messages - a simple list of dictionaries or a JSON file is fine.  Design so adding content is trivial.
3. **Build the plain loop first.**  Present an exercise, accept an answer, give feedback, repeat.  No psychology yet - just a working tutor with a clear, friendly interface (this is also your Human-Centric Design foundation).
4. **Layer in the mechanisms one at a time.**  Add streaks or progress that persists between runs (investment), variable praise/bonus challenges (variable reward), and a session-start hook that references the user's past progress (trigger).  Adding them one at a time lets you say in your report what each one changed.
5. **Time your testers.**  Recruit classmates, start a timer when they begin, and note when (and why) they choose to stop.  Their engagement duration is your primary measurement; their confusion is your primary design feedback.

## Milestones

- **Checkpoint 1 (end of the first few days): the design exists.**  Subject chosen, Hooked-loop table written, content bank drafted, and interface sketched.  You can explain to a classmate exactly which feature will implement which psychological mechanism.
- **Checkpoint 2 (roughly halfway): the plain tutor works.**  A user can complete a full practice session - exercises presented, answers checked, feedback given - and their progress persists between runs.
- **Checkpoint 3 (several days before the deadline): the engagement loop works.**  Triggers, variable rewards, and investment are all implemented and observable in a session.  You have timed at least two classmates using the system, documented and acted on their feedback, and drafted the design report including your ethical reflection on where motivation would shade into manipulation.
