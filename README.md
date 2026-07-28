# Squat Detection & Rep Counter using Pose Estimation

A computer vision system that detects squats and counts repetitions from video, built using **MediaPipe Pose Landmarker**, joint-angle geometry, and a hysteresis-based state machine. Works across multiple camera angles (front-facing and side profile).

![Python](https://img.shields.io/badge/Python-3.10-blue) ![OpenCV](https://img.shields.io/badge/OpenCV-CV-green) ![MediaPipe](https://img.shields.io/badge/MediaPipe-Pose-orange)

## 🎥 Demo

Check out the project demo on LinkedIn: [LinkedIn Post]([https://www.linkedin.com/posts/your-post-link-here](https://www.linkedin.com/posts/hamza-asif-b84523325_computervision-machinelearning-python-activity-7487692116987596800-JfVE?utm_source=share&utm_medium=member_desktop&rcm=ACoAAFIgCNQBYNOMlVuv_ZciAeFswE8CI2V8LlY))

## 📌 Overview

This project takes a workout video as input and produces an annotated output video with a live on-screen dashboard showing:
- **State** — Standing or Squatting
- **Rep Count** — auto-incremented on every completed squat
- **Joint Angles** — Knee, Hip, and Elbow angles updated frame by frame

## ⚙️ How It Works

1. **Pose Extraction** — MediaPipe's Pose Landmarker detects 33 body landmarks per frame (shoulder, hip, knee, ankle, elbow, wrist).
2. **Smoothing** — A Savitzky-Golay filter is applied to the raw landmark coordinates to remove frame-to-frame jitter.
3. **Angle Calculation** — Joint angles (knee, hip, elbow) are computed geometrically from the smoothed landmark positions.
4. **State Classification** — A hysteresis-based threshold system (squat below 110°, stand above 150°) classifies each frame as *Standing* or *Squatting*, avoiding flicker at the boundary.
5. **Rep Counting** — A rep is counted every time the person completes a full Standing → Squatting → Standing cycle.
6. **Video Rendering** — The skeleton, joint angles, current state, and rep count are overlaid onto the original video frame by frame.

## 📊 Results

| Metric | Value |
|---|---|
| Total Reps Detected | 17 |
| Accuracy | 63.67% |
| Precision | 43.91% |
| Recall | 58.05% |
| F1-Score | 50.00% |

> **Note:** Ground-truth labels mark the *entire* descent-to-ascent motion as "Squatting," while the classifier only flags frames where the knee angle drops below 110°. This affects the frame-level precision/recall balance but does not affect rep-counting accuracy.

## 🛠️ Tech Stack

- Python
- OpenCV
- MediaPipe Pose Landmarker
- NumPy / Pandas
- SciPy (Savitzky-Golay smoothing)
- Matplotlib (angle tracking & confusion matrix plots)

## 🚀 Usage

1. Open `Squat_Detection_Rep_Counter.ipynb` in Google Colab
2. Run the cells in order
3. Upload your squat video when prompted
4. Download the annotated output video (`ready_output.mp4`) at the end

## 🔮 Future Improvements

- Extend to bilateral (left + right side) tracking for angled/rotated camera views
- Support additional exercises (push-ups, lunges) using the same pipeline
- Real-time webcam inference instead of offline video processing

## ✍️ Author

Hamza Asif — BS Artificial Intelligence, Dawood University of Engineering and Technology (DUET)
