# Law Breaking Recognition (Traffic Signal Violation Detection)

A traffic signal violation detector built on YOLOv8 (Ultralytics) and OpenCV. The script runs object detection on a traffic video, checks whether the traffic light region is bright (treated as a red light being active), and flags vehicles (bicycle, car, motorcycle, bus, truck) that fall inside a fixed region of interest (ROI) while the signal is red.

## Features

- YOLOv8 detection of vehicle classes (COCO labels) with a confidence threshold of 0.75
- Red light state estimated from mean brightness of a polygon over the red lamp
- ROI polygon check; vehicles inside the ROI during red are highlighted and labelled as violators
- Live OpenCV window showing boxes, polygons and text overlays; press ESC to exit

## Project structure

- `Traffic-Signal-Violation-Detection-main/` - bundled code folder (third-party "-main" repository copy, adapted; its own README is kept)
  - `Traffic Signal Violation Detection.py` - main script: detection, red light check, ROI violation logic, display
  - `requirements.txt` - pinned dependencies
  - `yolov8m.pt` - YOLOv8 medium COCO weights (loaded by the script)
  - `tr.mp4`, `tv.mp4` - sample traffic videos (the script reads `tr.mp4`)
  - `README.md` - original README from the bundled repository

## Requirements

Pinned in `requirements.txt`:

- opencv-python==4.7.0.68
- ultralytics==8.0.26
- numpy==1.24.2

Packages imported by the script: `cv2`, `numpy`, `ultralytics`, plus standard library `os`, `time`.

## Installation

```bash
cd Traffic-Signal-Violation-Detection-main
pip install -r requirements.txt
```

## Usage

The script reads a video file, not a webcam:

```bash
python "Traffic-Signal-Violation-Detection-main/Traffic Signal Violation Detection.py"
```

- Input: `tr.mp4` (hard-coded in the script; the video is resized to 1100x700)
- Output: a display window only; the script does not save an output video
- The red light polygon, green light polygon and ROI are hard-coded pixel coordinates tuned for `tr.mp4`. For a different camera or video, these must be re-measured.

## Notes

- The script calls `os.chdir(...)` with a hard-coded Windows path from the original author's machine. This must be removed or edited before the script will run elsewhere.
- Coordinates for the red/green lights and ROI are fixed to the sample video.
- Red light detection is a simple brightness threshold (mean gray value > 128) and does not identify colour; it can misfire under different lighting.
- `tv.mp4` is included but not referenced by the script.
- Model and video files are included in the folder (`yolov8m.pt`, `tr.mp4`, `tv.mp4`).
