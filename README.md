# Lane Keeping Assistant 

## Overview
This repository contains the code for a Lane Keeping Assistant (LKA) system. The LKA system uses computer vision techniques to detect and track road lanes to assist in maintaining the vehicle's position within the lanes. This project showcases the LEFT and RIGHT Lane separately.

## Demo Video: 
[![Alt text](https://img.youtube.com/vi/foQegbsFQmo/0.jpg)](https://www.youtube.com/watch?v=foQegbsFQmo)



## Get This Project Up and Running

### Setting up a Python Virtual Environment for "LKAS-LANE KEEPING ASSISTANT"
To maintain a clean and isolated Python environment for your "LKAS Project" project, follow these steps in your terminal:

#### Navigate to the Project Directory
```sh
cd Lane-keeping-assiatnce/

Create a Virtual Environment
sh
Copy
python -m venv venv
Activate the Virtual Environment
On Windows:

cmd
Copy
.\venv\Scripts\activate
On macOS and Linux:

sh
Copy
source venv/bin/activate
Install Project Dependencies from requirements.txt
sh
Copy
pip install -r requirements.txt
Running the Project
This project follows a simplistic approach in terms of how to run it. Only 2 files are needed to get it running:

laneDetection.py: The Python script that performs image processing and lane detection.
test1.mp4: The video file on which image processing is performed.
Ensure that the files provided are in the same directory.

Cloning the Repository
Simply clone this repository to your desired path by launching the command prompt and running:

sh
Copy
git clone https://github.com/imdiora/Lane-keeping-assistance-
Usage
After setting up your environment and cloning the repository, ensure that the provided files are in the same directory.

## How the Code Works

### 1. Image Processing
The foundation of the LKA system is image processing. Since a video is a collection of sequential images, the system processes each image to detect lane lines.

- **readVideo()**: This function is responsible for loading the video file `test1.mp4` from the same directory.

- **Canny Edge Detection**: This is a multi-step process used to detect the edges within an image, which correspond to lane markings. The process involves:
  - **Grayscale Conversion**: Using `cv2.cvtColor` to convert the image to grayscale reduces complexity and simplifies subsequent operations.
  - **Gaussian Blur**: The `cv2.GaussianBlur` function is applied to smooth the image, which helps to diminish noise and irrelevant details.
  - **Canny Method**: The `cv2.Canny` function detects edges by highlighting regions with a high gradient in brightness.

  These steps are integrated into a single function named `canny` to facilitate their collective use.

### 2. Region of Interest
The system must focus on a specific section of the image where lane lines are expected to be. This is referred to as the region of interest (ROI).

- **Region of Interest**:
  To define the ROI, we first establish the area we aim to scan for lane lines. This is often aided by using the Matplotlib library for visualization purposes during development.
  
  After determining the dimensions, we implement a function named `region_of_interest`:

    ```python
    def region_of_interest(image):
        height = image.shape[0]
        polygons = np.array([
        [(200, height), (1200, height), (800, 400)]
        ])
        mask = np.zeros_like(image)
        cv2.fillPoly(mask, polygons, 255)
        masked_image = cv2.bitwise_and(image, mask)
        return masked_image
    ```

### 3. Hough Transform
The Hough Transform is employed to discern prominent lines and to connect the dots of edge points in the image, which allows us to infer the presence of lane lines.

    ```python
    lines = cv2.HoughLinesP(cropped_image, 2, np.pi/180, 100, np.array([]), minLineLength=40, maxLineGap=5)
    ```

### 4. Coordinates and Display Lines
The final step in the image processing stage is to calculate the coordinates of the detected lines and display them on the image. This is accomplished with a function called `display_lines`:

    ```python
    def display_lines(image, lines):
        # Logic for drawing lines on the image will be implemented here.
        pass
    ```

### Video Processing
The image processing routines are then applied frame-by-frame to the video stream, resulting in real-time lane detection. This is crucial for an LKA system, which relies on continuous feedback to maintain the vehicle within the lane boundaries.

---

For detailed implementation and instructions on how to use the LKA system, please see the source code and additional documentation within this repository.
