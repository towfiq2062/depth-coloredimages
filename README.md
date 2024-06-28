# Depth image processing:
This code colorizes the depth image file to Jetcolormap
Depth images from Kinect V2 have a resolution of 512 x 414. These depth images can be converted using the following steps: 
![image](https://github.com/towfiq2062/depth-coloredimages/assets/66333754/82263efa-5dfb-4edb-87e5-227896bc5421)

Here is the raw data from the Kinect V2 camera that was imported, ROI selected and clipped the image with the threshold limit. This limit is defined after measuring the z-values of the object (from floor to the highest position of the object).

The following code will work in the TensorFlow GPU 2.9 (python version 3.9.13) platform
Library requirement: OpenCV (Version 4.9.0), NumPy (Version 1.23.3), Pandas (Version 2.1.0), and Matplotlib (Version 3.5.3) 


