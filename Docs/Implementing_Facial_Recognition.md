# Facial Recognition Report

## Introduction

This document describes the complete process of designing, building, and
refining a computer‑vision driven attention‑tracking system. The goal of
this system is to determine whether users are looking at a designated
display, how long they remain present, and how their attention behaves
over time. I created the system by combining multiple scripts, models,
and detection techniques, gradually improving accuracy through iterative testing.

## Project Overview

The system uses a live camera feed to detect people, track them across
frames, estimate how long they remain in view, and determine whether
each individual is actively looking at the monitored screen. To
accomplish this, I integrated multiple technologies and model files:

-   A lightweight YOLOv8 detection model (`yolov8n.pt`) for person
    detection.
-   A DNN-based OpenCV face detector using a `.caffemodel` file and a
    matching `deploy.prototxt` descriptor file.
-   An OpenCV Haar-cascade eye detector to validate whether a detected
    face includes visual evidence of visible eyes.
-   Custom tracking logic that assigns unique IDs, computes dwell time,
    and determines whether a person is paying attention.

Each component was added deliberately as part of a step‑by‑step
refinement process. Going from mere person tracking to refined facial/eye tracking resulted by iterated versions.

## Installation and Environment Setup

I began by preparing an isolated Python environment using a virtual
environment inside the project directory. This ensured all dependencies
were contained locally and that package versions would remain stable.
The system uses Python 3.x (in my case, Python 3.13.x), OpenCV, NumPy,
and the Ultralytics YOLO package.

A consistent file structure became essential as additional scripts and
model files were added. The resulting folder layout included:

-   `attention_tracking.py`
-   `camera_test.py`
-   `people_detection.py`
-   `yolov8n.pt`
-   `deploy.prototxt`
-   `res10_300x300_ssd_iter_140000_fp16.caffemodel`

Maintaining these files in the same directory allowed the scripts to
reference them consistently, especially when using absolute file path
logic.

## Integrating YOLO for Person Detection

The first major component was YOLOv8 (from Ultralytics). This model
performed fast and reliable person detection. I used it to extract
bounding boxes around individuals in the frame. The ultralytics YOLO
package was installed through pip, and the `yolov8n.pt` model file was
downloaded as the lightweight backbone for the system.

This stage focused purely on identifying and tracking the presence of
people. The output of this step was a stable stream of bounding box
coordinates representing each detected person.

## Adding Face Detection with OpenCV DNN

To determine whether a person was paying attention to the screen, it
became necessary to identify their faces. The original Haar-based
cascade detector was insufficient for distance and lighting conditions,
so I added a more modern, DNN‑based face detector provided by OpenCV.

This required two external files:

-   `deploy.prototxt`
-   `res10_300x300_ssd_iter_140000_fp16.caffemodel`

The prototxt file describes the model structure, while the caffemodel
file contains the trained weights. I placed both files in the project
directory and referenced them using absolute paths to ensure OpenCV
could load them consistently. The caffemodel file was retrieved from a
HuggingFace repository: -
https://huggingface.co/Durraiya/res10_300x300_ssd_iter_140000_fp16.caffemodel

The prototxt file was retrieved from the official OpenCV GitHub: -
https://raw.githubusercontent.com/opencv/opencv/master/samples/dnn/face_detector/deploy.prototxt

The combination of these files enabled high‑quality face detection,
significantly improving the reliability of attention estimation.

## Eye Detection for Attention Validation

The next improvement involved determining whether a detected face should
be considered "looking at the screen." Face detection alone is not
enough, particularly when the head is angled or partially visible. To
improve accuracy, I added the OpenCV Haar-cascade for eye detection:

-   `haarcascade_eye_tree_eyeglasses.xml`

This model is bundled by default with OpenCV and is accessed
programmatically through:

    cv2.data.haarcascades

I used the eye detector only within the face bounding box, reducing
false positives and increasing speed. This allowed me to evaluate
whether a detected face contained recognizable eyes. If no eyes were
detected, the system interpreted this as the person not looking at the
screen. This created a more natural definition of "attention."

## Person Tracking and Dwell Time

To understand user behavior over time, I implemented a lightweight
tracking system. Each detected person receives a unique ID. For each ID,
I store:

-   The center point of their bounding box
-   The timestamps at which they were first and last detected
-   Whether they were looking at the screen during the current frame
-   Their current bounding box

This allows the system to calculate dwell time (how long each person
remains in view). I also implemented a cleanup system that removes IDs
when a person leaves the frame for longer than a defined threshold. (Data can later be stored in a database, if needed)

## Why These Components Are Important

Each technology plays a specific role in producing a usable and
meaningful attention‑tracking system:

-   YOLO provides fast and reliable person detection.
-   The DNN face detector identifies faces at greater distances and in
    varied lighting conditions.
-   Eye detection adds an additional layer of validation, ensuring that
    "attention" is based on visible cues.
-   The tracker maintains continuity and allows the computation of
    time‑based metrics.
-   The combined system gives a realistic approximation of viewer
    engagement with the display.

This layered approach avoids overreliance on any single detection method
and produces results that are interpretable and actionable.

## What We Expect to Achieve

\[Writing...\]

## Notes on Future Improvements

Future refinements could include: 
- Head pose estimation for more
precise gaze direction. 
- Digital calibration of expected viewing
areas. 
- Integration with Supabase for real-time data logging. 
- A web
dashboard for analytics and visualization to further challenge myself.

These improvements would make the system even more accurate and useful
in real‑world deployment scenarios.

## Written Code

\[Link to code base\]