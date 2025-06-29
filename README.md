# Vehicle Detection and Traffic Analysis System

A real-time computer vision system that detects and tracks vehicles using YOLOv8 object detection and custom tracking algorithms.

## Features

- Real-time vehicle detection using YOLOv8
- Object tracking with unique vehicle IDs
- Direction detection and traffic flow counting
- Real-time visualization with bounding boxes

## Technologies

- Python
- YOLOv8
- OpenCV
- Computer Vision
- Object Detection & Tracking

## Installation

```bash
pip install -r requirements.txt
```

## Usage

1. Open `detect_track_count.ipynb` in Jupyter Notebook
2. Run all cells to start the detection system
3. The system will process video and display real-time results

## Project Structure

```
├── detect_track_count.ipynb    # Main application
├── tracker.py                  # Custom tracking algorithm
├── requirements.txt            # Dependencies
└── README.md                   # This file
``` 