# Facial Recognition Research

## Introduction

This document describes my research into building a real-time attention and presence detection system using computer vision and lightweight AI models. The goal of this work was to understand whether it is technically feasible to detect how many people are present in front of a screen, how long they remain there, and whether they are directing their attention toward a large display. Although this document describes a hypothetical setup, it reflects a realistic research and development process based on tools and constraints.

I focused on solutions that could run locally, without relying on cloud services or specialized hardware, because the target environment is a standard computer with a regular camera and was meant for testing. The approach of not having to pay for hosting or hardware such as Raspberry Pi or Arduino, sounded appealing to me.

## Research Question

The question guiding this work was: *How can I build a lightweight, local, real-time attention detection system using only a standard camera from scratch?* From this, several questions followed. I needed to know which computer-vision models could reliably detect people and faces in real time, how I could estimate whether someone was actually looking at the screen, and how to track the same person over multiple frames so that I could measure the person's dwell time. I was also concerned about robustness/fallbacks: the system needed to work across different lighting conditions, viewing distances, and skin tones.

## Initial Exploration

I started by researching and exploring the available tools for real-time computer vision. My focus was laid on libraries that were well documented, mondern-ish, and easy to integrate into a Python workflow. I spent time reading documentation, reviewing tutorials, and examining open-source examples, while also experimenting with AI-assisted exploration of the problem.

The main resources I relied on were:

- https://github.com/ultralytics/ultralytics  
- https://docs.opencv.org  
- https://huggingface.co  
- https://github.com/opencv/opencv  

During this phase, it became clear that full facial recognition systems were far too heavy for my intended setup. They require too much computation and memory to run reliably on consumer hardware. Because of this, I shifted my focus toward efficient models that prioritize speed and low resource usage while still being accurate enough for presence and attention tracking.

## Real-Time Person Detection

To detect whether people were present in front of the screen, I evaluated several object-detection models. **YOLOv8 Nano** stood out as the best fit for this project. It offered a strong balance between performance and speed, making it suitable for real-time use on a CPU setup. It also integrates through the **Ultralytics Python API** and can achieve 30 frames per second.

The implementation of this detection system requires a Python environment, ideally, isolated in a virtual environment so that model and library dependencies remain stable and easy to manage.

## Face Detection

Once a person is detected, the next step is to locate their face so that attention can be estimated. I tested several face-detection approaches, including **OpenCV Haar Cascades**, **MediaPipe Face Detection**, and **OpenCV’s DNN-based SSD face detector**. Haar Cascades is fast but unreliable at larger distances. MediaPipe produced high-quality facial landmarks, but it was not available for Python 3.13 at the time of testing, which made it impractical for this setup.

For that reason, I chose the OpenCV DNN SSD-based face detector. It seemed efficient, stable, and performs well across a range of lighting conditions. I downloaded the required model files (`deploy.prototxt` and the `res10_300x300` SSD model) and confirmed that they worked correctly within my Python environment.

## Eye Detection and Attention Estimation

To estimate whether someone is paying attention to the screen, I added a simple form of eye detection using **OpenCV’s built-in Haar Cascade for eyes**. While this method is basic, it provides a useful approximation of whether a person is facing the camera or display.

The logic I used is straightforward. First, a face is detected. Then, the system searches for eyes inside that face region. If eyes are found, the person is probably looking roughly toward the screen/target. This approach avoids the need for gaze-tracking models while still providing attention signals.

## Tracking People Over Time

In order to calculate how long someone stays in view, I needed a way to track individuals across frames. I implemented a simple centroid-based tracking system that assigns an ID to each detected person. When a person enters the frame, they receive a new ID. As long as their detected position remains close to a previous location, that ID keeps existing. If the person leaves the frame or moves too far from their previous position, the track is ended.

Using timestamps with the first and last time each ID appears, I can estimate dwell time. I considered more advanced tracking systems such as **ByteTrack** or **DeepSORT**, but for the goals of this prototype, the simpler centroid-based approach was sufficient enough.

## System Architecture

The final prototype consists of several lightweight components into a real-time pipeline. **YOLOv8 Nano** is used for person detection, **OpenCV’s DNN model** handles face detection, and **Haar Cascades** are used for eye detection. A **centroid-based tracker** keeps track of individuals over time, while OpenCV provides visualization and camera access. Everything runs inside a Python virtual environment, keeping the setup clean and save for future iterative versions.

The entire system operates offline and can run in real time on a standard laptop using either an integrated or external camera.

## Conclusion

Through this research, I found that it is entirely doable to build a local, real-time system capable of detecting people, measuring how long they stay, and estimating whether they are paying attention to a screen. By considering and selecting lightweight models and simple tracking techniques, it is possible to achieve results without relying on expensive hardware or cloud services. This work provided valuable insight into model selection, performance, and the challenges of building camera-based attention systems as a side project.
