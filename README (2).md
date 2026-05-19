# 🏋️ Exercise Analysis System — GIU Image Processing & Computer Vision Project

> **Course:** Introduction to Image Processing and Computer Vision — Spring 2026
> **Institution:** German International University (GIU), Faculty of Informatics and Computer Science
> **Instructor:** Dr. Maggie Shammaa
> **Deadline:** May 19, 2026

---

## 📋 Table of Contents

- [Project Overview](#project-overview)
- [Team Information](#team-information)
- [Architecture Comparison Track](#architecture-comparison-track)
- [Exercise Analysis System](#exercise-analysis-system)
- [Installation](#installation)
- [Usage](#usage)
- [Output Format](#output-format)
- [Project Structure](#project-structure)
- [Deliverables](#deliverables)

---

## 🔍 Project Overview

This project has two components:

1. **Architecture Comparison** — A comparative study of three architectures from a chosen track (Object Detection, Segmentation, or Vision Backbone).
2. **Exercise Analysis System** — A Python-based system that uses YOLOv8 pose estimation to analyze exercise videos (squats and push-ups), count repetitions, assess form quality, and output structured JSON results.

---

## 👥 Team Information

| Field         | Details                          |
|---------------|----------------------------------|
| Team Members  | _(Add names here)_               |
| Tutorial Group| _(Add tutorial group here)_      |
| Team Size     | _(2–4 members, same tutorial)_   |

> **Note:** All team members must be from the **same tutorial group**. Register your team via the [Team Registration Form](https://docs.google.com/forms/d/e/1FAIpQLSd3uLbqNgAg_q0YndDgflMFPjCzpRWYDYowUJMj4AugArmjUQ/viewform?usp=dialog).

---

## 🏗️ Architecture Comparison Track

**Selected Track:** _(Fill in: Object Detection / Segmentation / Vision Backbone)_

### Track Options

| Track | Architectures |
|-------|--------------|
| Object Detection | YOLOv8, Faster R-CNN, SSD |
| Segmentation | U-Net, DeepLabV3, Mask R-CNN |
| Vision Backbone | ResNet, Vision Transformer (ViT), Swin Transformer |

### Comparison Criteria

The presentation covers each architecture across the following dimensions:

- **Internal structure** — How the architecture is designed
- **Prediction mechanism** — How it produces its output
- **Advantages** — Strengths and ideal use cases
- **Limitations** — Weaknesses and failure modes
- **Applications** — Real-world domains where it excels

---

## 🤸 Exercise Analysis System

### Overview

The system processes short video clips containing squats and/or push-ups and performs:

1. **2D Pose Estimation** using YOLOv8 small pose model
2. **Keypoint Smoothing** via Exponential Moving Average (EMA)
3. **Repetition Counting** for squats and push-ups
4. **Form Assessment** via joint-angle analysis
5. **JSON Output Generation** with summary statistics

### Supported Exercises

#### Squats
- Repetition counting
- Form quality evaluation
- Squat depth validation (based on knee/hip angle thresholds)

#### Push-ups
- Repetition counting
- Form quality evaluation
- Body-line alignment and/or elbow-angle validation

---

## ⚙️ Installation

### Prerequisites

- Python 3.9+
- pip

### Steps

```bash
# 1. Clone the repository
git clone <your-repo-url>
cd exercise-analysis

# 2. Create a virtual environment (recommended)
python -m venv venv
source venv/bin/activate        # On Windows: venv\Scripts\activate

# 3. Install dependencies
pip install -r requirements.txt
```

### `requirements.txt`

```
ultralytics
opencv-python
numpy
```

---

## 🚀 Usage

```bash
python main.py --video path/to/your/video.mp4
```

### Optional Arguments

| Argument | Default | Description |
|----------|---------|-------------|
| `--video` | `input.mp4` | Path to input video file |
| `--output` | `output.json` | Path for the JSON output file |
| `--ema-alpha` | `0.5` | EMA smoothing factor (0–1) |
| `--show` | `False` | Display annotated video while processing |

### Example

```bash
python main.py --video workout.mp4 --output results.json --show
```

---

## 📤 Output Format

The system generates a structured JSON file:

```json
{
  "video_id": "a3f2c1d4-...",
  "summary": {
    "squats": {
      "total_reps": 12,
      "good_form_reps": 10
    },
    "pushups": {
      "total_reps": 8,
      "good_form_reps": 7
    }
  }
}
```

---

## 🗂️ Project Structure

```
exercise-analysis/
│
├── main.py                  # Entry point
├── pose_estimator.py        # YOLOv8 pose estimation wrapper
├── smoother.py              # EMA keypoint smoothing
├── rep_counter.py           # Repetition counting logic
├── form_assessor.py         # Joint angle analysis & form rules
├── output_generator.py      # JSON output generation
│
├── requirements.txt
├── README.md
│
├── presentation/
│   └── architecture_comparison.pptx
│
└── samples/
    └── sample_video.mp4     # Example input video
```

---

## 📦 Deliverables Checklist

- [ ] PowerPoint presentation (architecture comparison)
- [ ] Source code implementing:
  - [ ] Pose estimation (YOLOv8)
  - [ ] Keypoint smoothing (EMA)
  - [ ] Repetition counting (squats + push-ups)
  - [ ] Form assessment (joint angles)
  - [ ] JSON output generation
- [ ] This README

---

## 📚 References

- [Ultralytics YOLOv8 Documentation](https://docs.ultralytics.com/)
- [OpenCV Documentation](https://docs.opencv.org/)
- _(Add any papers or resources cited in your presentation)_
