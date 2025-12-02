# Facial Recognition Research

## Introduction

This document describes research about implementing a real-time attention and presence detection system using
computer vision and lightweight AI models. The goal of the research is
to investigate whether it is technically feasible to detect how many
people are present, how long they remain in view, and whether they
direct their attention toward a large screen installation. All findings
in this document are hypothetical but reflect a realistic research
process.

## Research Question

The central question was: *How can we build a lightweight, local,
real-time attention detection system using a standard camera, without
relying on heavy cloud services or expensive hardware?* This led to
several sub-questions: 
- Which vision models are suitable for detecting
people and faces in real-time? 
- How can we estimate whether someone is
looking at the screen? 
- How can we track unique individuals over
time? 
- How do we ensure that the solution works at different distances, lighting conditions and for different tones of skin?

## Initial Exploration

I began by exploring various approaches to real-time computer vision. Focusing on tools that were simple to use, actively maintained, and
well-documented. The initial research included reading documentation,
tutorials, and open-source examples. As well as taking a shot at AI on this matter. 

Links: 
- https://github.com/ultralytics/ultralytics 
- https://docs.opencv.org 
- https://huggingface.co 
- https://github.com/opencv/opencv

I determined that running heavy models such as full facial
recognition or neural gaze estimation would be too expensive (running) for our target setup. Instead, focusing on efficient models
with low memory usage and fast inference times is a must.

## Real-Time Person Detection

Multiple options for detecting human presence were evaluated. YOLOv8 Nano proved to be a strong candidate. 

The benefits included: 
- Fast inference on CPU 
- Accurate bounding box detection for persons 
- Easy integration through the Ultralytics Python API 
- Ability to run at 30+ FPS on consumer hardware

The implementation probably requires installing Python (script) and setting up a virtual environment for protection.

## Face Detection Approaches (testing)

Face detection technologies: 
1. Haar Cascades (OpenCV) 
2. OpenCV DNN SSD-based face detector 
3. MediaPipe Face Detection

The Haar Cascade approach was lightweight but inaccurate at larger
distances. MediaPipe provided superior facial landmark detection but was not available for Python 3.13 at the time of testing. Therefore, we
analyzed the SSD-based OpenCV DNN model. This model is efficient,
stable, and performs well in varied lighting conditions.

The necessary model files were gathered (deploy.prototxt and the
res10_300x300 SSD model) and validated that they worked inside the
Python environment.

## Eye Detection for Attention Estimation

Discrete eye detection was added using OpenCV's built-in eye detection
cascade. Although basic, this method allowed us to approximate whether
someone might be facing the camera or screen.  

The logic:
- Detect a face 
- Detect eyes within that face 
- Determine that the person is likely "looking" if the eyes are visible inside the face region

This approach avoids heavier gaze estimation models while still offering useful attention approximations.

## Tracking Individuals Over Time

To estimate dwell time and track unique individuals, we implemented a
simple centroid-based tracker. 

For each detected person: 
- A new ID is created when a person enters the frame 
- The ID persists as long as the person remains visible 
- Distance thresholds determine whether detections match previous positions 
- Dwell time is calculated using timestamps assigned on first and last frame detection

More advanced tracking solutions (ByteTrack or DeepSORT) were
considered but deemed unnecessary at this time.

## System Architecture Summary

The final prototype integrates several components: 
- YOLOv8 Nano for person detection 
- OpenCV DNN for face detection 
- Eye detection using Haar Cascades 
- Centroid tracking for ID persistence 
- Real-time visualization through OpenCV 
- A structured codebase running inside a Python virtual environment

This pipeline runs completely offline and in real-time on a standard
laptop with an integrated or external webcam.

## Conclusion

Through this research we concluded that real-time person tracking, dwell time measurement, and attention estimation are achievable using
lightweight AI models and standard computer vision techniques. A lot of knowledge was gained on model selection, tracking strategies, performance considerations, and the practical challenges of working with camera-based attention systems.