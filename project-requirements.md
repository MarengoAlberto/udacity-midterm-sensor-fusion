# 3D Object Detection Project Requirements

## Table of Contents
1. [Compute Lidar Point-Cloud from Range Image](#1-compute-lidar-point-cloud-from-range-image)
2. [Create Birds-Eye View from Lidar PCL](#2-create-birds-eye-view-from-lidar-pcl)
3. [Model-based Object Detection in BEV Image](#3-model-based-object-detection-in-bev-image)
4. [Performance Evaluation for Object Detection](#4-performance-evaluation-for-object-detection)

## 1. Compute Lidar Point-Cloud from Range Image

### Task 1.1: Visualize range image channels (ID_S1_EX1)
- Convert range image "range" channel to 8bit
- Convert range image "intensity" channel to 8bit
- Crop range image to +/- 90 deg. left and right of the forward-facing x-axis
- Stack cropped range and intensity image vertically and visualize the result using OpenCV

### Task 1.2: Visualize point-cloud (ID_S1_EX2)
- Visualize the point-cloud using the open3d module

### Task 1.3: Write-up Requirements
- Find 10 examples of vehicles with varying degrees of visibility in the point-cloud
- Identify vehicle features that appear stable in most of the inspected examples and describe them

## 2. Create Birds-Eye View from Lidar PCL

### Task 2.1: Convert sensor coordinates to bev-map coordinates (ID_S2_EX1)
- Convert coordinates in x,y [m] into x,y [pixel] based on width and height of the bev map

### Task 2.2: Compute intensity layer of bev-map (ID_S2_EX2)
- Assign lidar intensity values to the cells of the bird-eye view map
- Adjust the intensity in such a way that objects of interest (e.g. vehicles) are clearly visible

### Task 2.3: Compute height layer of bev-map (ID_S2_EX3)
- Make use of the sorted and pruned point-cloud `lidar_pcl_top` from the previous task
- Normalize the height in each BEV map pixel by the difference between max. and min. height
- Fill the "height" channel of the BEV map with data from the point-cloud

## 3. Model-based Object Detection in BEV Image

### Task 3.1: Add a second model from a GitHub repo (ID_S3_EX1)
- In addition to Complex YOLO, extract the code for output decoding and post-processing from the GitHub repo

### Task 3.2: Extract 3D bounding boxes from model response (ID_S3_EX2)
- Transform BEV coordinates in [pixels] into vehicle coordinates in [m]
- Convert model output to expected bounding box format [class-id, x, y, z, h, w, l, yaw]

## 4. Performance Evaluation for Object Detection

### Task 4.1: Compute intersection-over-union (IOU) between labels and detections (ID_S4_EX1)
- For all pairings of ground-truth labels and detected objects, compute the degree of geometrical overlap
- The function `tools.compute_box_corners` returns the four corners of a bounding box which can be used with the Polygon structure of the Shapely toolbox
- Assign each detected object to a label only if the IOU exceeds a given threshold
- In case of multiple matches, keep the object/label pair with max. IOU
- Count all object/label-pairs and store them as "true positives"

### Task 4.2: Compute false-negatives and false-positives (ID_S4_EX2)
- Compute the number of false-negatives and false-positives based on the results from IOU and the number of ground-truth labels

### Task 4.3: Compute precision and recall (ID_S4_EX3)
- Compute "precision" over all evaluated frames using true-positives and false-positives
- Compute "recall" over all evaluated frames using true-positives and false-negatives