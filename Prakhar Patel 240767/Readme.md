# Advanced Driver Assistance System (ADAS) Simulation

## About the Project
This project simulates an Advanced Driver Assistance System in real-time using dashcam footage. By integrating traditional computer vision (OpenCV) with modern deep learning models (YOLOv8), the system successfully identifies lanes, detects surrounding vehicles, and issues critical safety alerts.

## Project Journey & Documentation
- **What I have done:** I implemented an Advanced Driver Assistance System (ADAS) capable of real-time lane tracking and vehicle detection using dashcam footage. I used OpenCV for geometric lane detection (Canny edge detection and Hough transforms) and YOLOv8 for recognizing vehicles on the road.
- **What I tried:** I experimented with combining traditional computer vision and modern deep learning. I initially looked at relying purely on edge detection for obstacles, but found that YOLOv8 provided significantly more robust vehicle recognition.
- **Why I did it:** I chose this hybrid approach because OpenCV is highly efficient and precise for fixed geometric structures like road lanes, while YOLOv8 is state-of-the-art for dynamic object classification, making the system both fast and accurate.

## Key Features
- **Lane Tracking:** Detects lane boundaries and estimates the drivable area.
- **Vehicle Recognition:** Identifies vehicles on the road, drawing bounding boxes and displaying confidence levels.
- **ROI Masking:** Focuses computational analysis strictly on the road ahead.
- **Traffic Counting:** Tracks and counts vehicles that enter the current lane.
- **Collision Alerts:** Triggers a warning if a forward collision is imminent.
- **Lane Departure:** Warns the driver if the vehicle begins to drift out of the center lane.

## How It Works (Frame-by-Frame)

### 1. Lane Identification
- Converts the frame to grayscale and applies Gaussian smoothing.
- Detects edges using the Canny algorithm.
- Applies a geometric mask to isolate the region of interest (ROI).
- Uses the Hough Transform to find lane markings.
- Calculates the center of the lane and creates a visual polygon.
*Visual Result:* The drivable lane is highlighted with a yellow overlay.

### 2. Forward Safety Zone
- Establishes a trapezoidal monitoring area directly in front of the vehicle.
- Uses background subtraction (MOG2) to detect movement in this zone.
- Evaluates contour areas to determine obstacle risk.
- Displays an alert when an obstacle is too close.
*Visual Result:* A red warning zone appears, accompanied by text alerts and screen tinting.

### 3. Object Detection & Tracking
- Employs the YOLOv8 neural network to recognize cars, buses, trucks, and motorcycles.
- Assigns a unique ID to each detected vehicle for continuous tracking.
- Computes the center point of each vehicle.
- Updates the total vehicle count only when a vehicle's center enters the lane polygon.
- Utilizes a unique registry to prevent duplicate counting.
*Visual Result:* Bounding boxes (Green for in-lane, Red for out-of-lane) with labels and a live count on the screen.
