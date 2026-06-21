# Gesture Recognition System

Real-time hand gesture recognition in C++ using OpenCV — counts fingers shown to a webcam and triggers corresponding OS-level actions. Built with modular architecture and a full unit test suite.

---

## Overview

This project does two things:

1. **Computer vision pipeline** — detects a hand in a webcam feed, segments it from the background, counts extended fingers using contour and convexity-defect analysis
2. **Action dispatch** — maps each finger count (1–5) to a system action

The codebase was deliberately refactored from a working monolith into modular, testable components with a Google Test suite.

---

## Tech Stack

| | |
|---|---|
| **Language** | C++ |
| **Computer Vision** | OpenCV |
| **Testing** | Google Test |
| **Build System** | CMake |

---

## How It Works

### Detection Pipeline
Webcam frame

→ HSV color space conversion

→ Skin color segmentation (HSV threshold mask)

→ Largest contour extraction (hand region)

→ Convexity defect analysis

→ Finger count from defect angles

→ Action dispatch

### Finger-to-Action Mapping

| Fingers | Action |
|---|---|
| 1 | Open browser |
| 2 | Open calculator |
| 3 | Open file manager |
| 4 | Open terminal |
| 5 | Custom / configurable |

---

## Project Structure
gesture-recognition/

├── CMakeLists.txt

├── src/

│   ├── main.cpp

│   ├── segmentation.cpp

│   ├── contour_analysis.cpp

│   ├── finger_counter.cpp

│   └── action_dispatch.cpp

├── include/

│   ├── segmentation.h

│   ├── contour_analysis.h

│   ├── finger_counter.h

│   └── action_dispatch.h

└── tests/

├── test_segmentation.cpp

├── test_finger_counter.cpp

└── test_action_dispatch.cpp

---

## Build & Run

### Prerequisites
- OpenCV 4.x
- CMake 3.15+
- Google Test
- C++17-compatible compiler

### Build
```bash
mkdir build && cd build
cmake ..
make
```

### Run
```bash
./gesture_recognition
```

### Run Tests
```bash
cd build
ctest --output-on-failure
```

---

## Testing Approach

The test suite covers core detection modules independently — segmentation, contour analysis, and finger counting can each be verified without a live webcam feed by passing in pre-processed image data.

---

**University:** COMSATS University Islamabad, Wah Campus
