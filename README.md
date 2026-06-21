Gesture Recognition System

Real-time hand gesture recognition in C++ using OpenCV — counts fingers shown to a webcam and triggers corresponding OS-level actions. Built with modular architecture and a full unit test suite.

Overview

This project does two things:


Computer vision pipeline — detects a hand in a webcam feed, segments it from the background, counts extended fingers using contour and convexity-defect analysis
Action dispatch — maps each finger count (1–5) to a system action


The codebase was deliberately refactored from a working monolith into modular, testable components with a Google Test suite — the goal was to apply real software-engineering discipline, not just make something work.


Tech Stack

LanguageC++Computer VisionOpenCVTestingGoogle TestBuild SystemCMake


How It Works

Detection Pipeline

Webcam frame
    → HSV color space conversion
    → Skin color segmentation (HSV threshold mask)
    → Largest contour extraction (hand region)
    → Convexity defect analysis
    → Finger count from defect angles
    → Action dispatch

Finger-to-Action Mapping

FingersAction1Open browser2Open calculator3Open file manager4Open terminal5Custom / configurable


Project Structure

gesture-recognition/
├── CMakeLists.txt
├── src/
│   ├── main.cpp
│   ├── segmentation.cpp      # HSV skin segmentation
│   ├── contour_analysis.cpp  # Contour + convexity defects
│   ├── finger_counter.cpp    # Counting logic
│   └── action_dispatch.cpp   # OS action triggers
├── include/
│   ├── segmentation.h
│   ├── contour_analysis.h
│   ├── finger_counter.h
│   └── action_dispatch.h
└── tests/
    ├── test_segmentation.cpp
    ├── test_finger_counter.cpp
    └── test_action_dispatch.cpp


Build & Run

Prerequisites


OpenCV 4.x
CMake 3.15+
Google Test (fetched automatically via CMake if not installed)
A C++17-compatible compiler


Build

bashmkdir build && cd build
cmake ..
make

Run

bash./gesture_recognition

Run Tests

bashcd build
ctest --output-on-failure


Testing Approach

The test suite covers the core detection modules independently — segmentation, contour analysis, and finger counting can each be tested without a live webcam feed by passing in pre-processed image data. This separation was the main architectural goal of the refactor.

tests/
├── Segmentation tests     — HSV mask output given known input frames
├── Finger counter tests   — convexity defect count → finger count logic
└── Action dispatch tests  — correct action triggered for each count


Notes


Works best under consistent lighting; HSV thresholds may need tuning for different environments
Designed and tested on Linux; OS action commands in action_dispatch.cpp may need adjustment for Windows/macOS



University: COMSATS University Islamabad, Wah Campus
