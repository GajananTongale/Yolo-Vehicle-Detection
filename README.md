# YOLOv8 Vehicle Detection and Tracking System

A real-time computer vision system that detects and tracks vehicles using YOLOv8 object detection and custom tracking algorithms. This system provides vehicle counting, direction detection, and real-time visualization capabilities.

## Table of Contents

- [Features](#features)
- [Requirements](#requirements)
- [Installation](#installation)
- [Usage](#usage)
- [How It Works](#how-it-works)
- [File Structure](#file-structure)
- [Configuration](#configuration)
- [Output](#output)
- [Troubleshooting](#troubleshooting)
- [Contributing](#contributing)
- [License](#license)

## Features

- **Real-time Vehicle Detection**: Uses YOLOv8 for fast and accurate vehicle detection
- **Object Tracking**: Maintains unique IDs for vehicles across video frames
- **Direction Detection**: Distinguishes between vehicles going in different directions
- **Live Statistics**: Real-time counting and vehicle tracking display
- **Data Recording**: Saves processed frames and output videos
- **Visual Feedback**: Bounding boxes, IDs, and statistics overlay

## Requirements

### System Requirements
- **Python**: 3.8 or higher
- **RAM**: Minimum 4GB (8GB recommended)
- **GPU**: Optional but recommended for faster inference
- **OS**: Windows, Linux, or macOS

### Python Dependencies
```
ultralytics>=8.0.0
opencv-python>=4.5.0
pandas>=1.3.0
numpy>=1.21.0
ipykernel>=6.0.0
matplotlib>=3.5.0
Pillow>=8.0.0
torch>=1.12.0
torchvision>=0.13.0
```

## Installation

### Option 1: Quick Setup (Recommended)

1. **Clone the repository**:
   ```bash
   git clone <repository-url>
   cd Detect--track-and-Count-using-YOLOv8-main
   ```

2. **Create virtual environment**:
   ```bash
   python -m venv yolo
   ```

3. **Activate virtual environment**:
   ```bash
   # Windows
   yolo\Scripts\activate
   
   # Linux/Mac
   source yolo/bin/activate
   ```

4. **Install dependencies**:
   ```bash
   pip install -r requirements.txt
   ```

5. **Install Jupyter kernel**:
   ```bash
   python -m ipykernel install --user --name=yolo --display-name="YOLOv8 Environment"
   ```

### Option 2: Using uv (Faster)

```bash
# Install uv
pip install uv

# Create environment with Python 3.9
uv venv --python=3.9 yolo

# Activate and install
yolo\Scripts\activate  # Windows
pip install -r requirements.txt
```

## Usage

### Running the Application

1. **Start Jupyter Notebook**:
   ```bash
   jupyter notebook
   ```

2. **Open the notebook**:
   - Navigate to `detect_track_count.ipynb`
   - Select the "YOLOv8 Environment" kernel

3. **Prepare your video**:
   - Place your video file in the project directory
   - Update the video path in the notebook if needed:
     ```python
     cap = cv2.VideoCapture('your_video.mp4')
     ```

4. **Run the cells**:
   - Execute all cells in order
   - The system will automatically download YOLOv8 model on first run

### Using Different Videos

To use your own video file:

```python
# Replace 'highway_mini.mp4' with your video file
cap = cv2.VideoCapture('your_video.mp4')
```

## How It Works

### 1. Object Detection
- Uses YOLOv8 to detect vehicles in each frame
- Filters for car class objects only
- Extracts bounding box coordinates

### 2. Object Tracking
- Custom tracker maintains unique IDs for vehicles
- Uses center point distance to match objects across frames
- Prevents ID switching and double counting

### 3. Direction Detection
- Two detection lines: Red (y=198) and Blue (y=268)
- Records when vehicle crosses each line
- Determines direction based on crossing order
- **Going Down**: Red line → Blue line
- **Going Up**: Blue line → Red line

### 4. Visualization
- Green bounding boxes around vehicles
- Red circles at vehicle centers
- Vehicle ID display
- Live statistics dashboard

## File Structure

```
Detect--track-and-Count-using-YOLOv8-main/
├── detect_track_count.ipynb    # Main Jupyter notebook
├── tracker.py                  # Custom object tracking module
├── requirements.txt            # Python dependencies
├── README.md                   # This file
├── highway_mini.mp4           # Sample video (5MB)
├── highway.mp4                # Sample video (22MB)
├── detected_frames/           # Saved frames (created automatically)
├── output.avi                 # Output video (created automatically)
└── yolov8s.pt                 # YOLOv8 model (downloaded automatically)
```

## Configuration

### Detection Lines
```python
red_line_y = 198    # Y-coordinate of first detection line
blue_line_y = 268   # Y-coordinate of second detection line
offset = 6          # Tolerance zone around lines (±6 pixels)
```

### Video Settings
```python
frame_width = 1020  # Output frame width
frame_height = 500  # Output frame height
fps = 20.0         # Output video frame rate
```

## Output

### Real-time Display
- **Live video feed** with detection overlays
- **Vehicle counters**: Going up/down
- **Bounding boxes** and vehicle IDs
- **Statistics dashboard**

### Saved Files
- **`detected_frames/`**: Individual processed frames as JPEG
- **`output.avi`**: Complete processed video
- **Console output**: Detection statistics

### Sample Output
```
Going Down - 15 vehicles
Going Up - 12 vehicles
Vehicle ID 5 detected
Vehicle ID 8 detected
```

## Customization

### Changing Detection Classes
```python
# In the detection loop, modify the class filter:
if 'car' in c or 'truck' in c or 'bus' in c:
    list.append([x1, y1, x2, y2])
```

### Adjusting Detection Lines
```python
# Modify line positions for your video:
red_line_y = 150    # Move red line up
blue_line_y = 300   # Move blue line down
```

### Tracking Parameters
```python
# In tracker.py, adjust the distance threshold:
if dist < 35:  # Increase for more lenient tracking
```

## Troubleshooting

### Common Issues

#### 1. Model Download Error
```
Error: Failed to download YOLOv8 model
```
**Solution**: Check internet connection and try again. The model will download automatically on first run.

#### 2. Video Not Found
```
Error: Could not open video file
```
**Solution**: 
- Ensure video file exists in project directory
- Check video file path in the code
- Verify video format is supported (MP4, AVI, etc.)

#### 3. Performance Issues
```
Slow detection or tracking
```
**Solution**:
- Use GPU if available (CUDA-compatible)
- Reduce frame resolution
- Process every nth frame: `if count % 2 != 0: continue`

#### 4. Memory Issues
```
Out of memory error
```
**Solution**:
- Close other applications
- Reduce video resolution
- Process shorter video clips

#### 5. Tracking Issues
```
Vehicle IDs switching or incorrect counting
```
**Solution**:
- Adjust tracking distance threshold in tracker.py
- Modify detection line positions
- Check video quality and frame rate

### Performance Tips

1. **GPU Acceleration**: Install CUDA and cuDNN for faster inference
2. **Frame Skipping**: Process every 2nd or 3rd frame for better performance
3. **Resolution**: Lower input resolution for faster processing
4. **Model Size**: Use smaller YOLOv8 models (nano, small) for speed

## Contributing

We welcome contributions! Please feel free to submit a Pull Request. For major changes, please open an issue first to discuss what you would like to change.

### How to Contribute

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Acknowledgments

- **Ultralytics**: For the excellent YOLOv8 implementation
- **OpenCV**: For computer vision capabilities
- **PyTorch**: For deep learning framework
- **Community**: For feedback and contributions

## Support

If you encounter any issues or have questions:

1. Check the [Troubleshooting](#troubleshooting) section
2. Search existing [Issues](../../issues)
3. Create a new issue with detailed information

## Updates

- **v1.0**: Initial release with basic detection and tracking
- **v1.1**: Added direction detection functionality
- **v1.2**: Improved tracking algorithm and visualization
- **v1.3**: Enhanced statistics and data recording

---

**Built with YOLOv8 and OpenCV** 