# Sports Ball Detection Pipeline

## Project Overview

This project implements an iterative learning pipeline for detecting sports balls in video footage, using the Sports-1M dataset and YOLOv8 object detection model.

## Repository Contents

- `sports_ball_detection.ipynb`: Main Jupyter notebook with the complete project implementation
- `results/`: Example visualisations of results
  - `detection_videos/`: Annotated videos showing ball detection, with bounding boxes highlighting the model's detection capabilities
  - `metrics/`: Performance metrics plotted across iterations
  - `visualisations/`: Representative single-frame snapshots demonstrating the model's detection performance across different video scenarios

## Key Features

### 1. Dynamic Dataset Creation
- Filters and downloads sports-related videos from the Sports-1M dataset
- Extracts frames at configurable sampling rates - reduces the storage size of the original video data
- Focuses on videos with ball-related labels - currently, we filter for labels with 'ball' in the title. This could be improved by creating a list of all ball-related sports, including those without 'ball' in their name, like Tennis, Golf, etc.
- Deletes videos once frames have been extracted to manage storage efficiently

### 2. Pseudo-Annotation Generation
- Uses pre-trained YOLOv8 model to generate initial annotations
- Automatically identifies and labels sports balls across video frames
- Implements confidence thresholding to ensure annotation quality

### 3. Iterative Dataset Improvement
- Implements a multi-iteration training approach
- Augments high-confidence detections to expand training data and to help reduce overfitting
- Splits dataset into training and validation sets each iteration
- Tracks model performance metrics across iterations

### 4. Comprehensive Visualisation
- Generates individual frame ball detection visualisations
- Creates annotated detection videos - view the whole video with ball detections overlayed
- Plots performance metrics over training iterations

## Future Improvements
- Expand video labels to include all ball sports, not just those with 'ball' in the name
- Increase the number of training and validation videos and the number of frames extracted per second - currently constrained by resources and time
- Increase iterations and epochs to better analyse the models performance
- Tune the confidence thresholds
- Implement further features and visualisation techniques
  - Calculate ball trajectories based on detection box centres
  - Visualise frames in a highest to lowest confidence to examine the scenarios where the model is most and least confident
  - 

## Technical Design Decisions

### Model Selection
- **YOLOv8x**: Chosen for its:
  - High accuracy in object detection
  - Comes with pre-trained weights on large datasets (COCO)
  - Excellent for domain-specific transfer learning
  - Built-in sports ball class (class 32) in a pre-trained model

### Annotation Strategy
- Pseudo-labeling with pre-trained model
- Confidence-based filtering
- Data augmentation to improve model generalisation

### Performance Tracking
- Calculates mAP (mean Average Precision) metrics
- Tracks performance across different iterations
- Visualises metric progression

## Technical Requirements

### Dependencies
- Python (Tested on 
- Libraries:
  - ultralytics (YOLO)
  - OpenCV
  - PyTorch
  - Pandas
  - Numpy
  - Matplotlib
  - yt-dlp

Included in the notebook, to download the dependencies to Colab:
```bash
!pip install ultralytics yt-dlp opencv-python pillow matplotlib pandas numpy requests
```

### Computational Resources
- **Developed & Tested on:** Google Colab - due to limited resources locally, chose to develop on Google's cloud platform Colab

## Limitations & Considerations

- Currently built for Google Colab environment

## Running the Project

### Google Colab Setup
1. Upload notebook to Colab
2. Enable GPU in Runtime settings
3. Install required dependencies
4. Run cells sequentially
