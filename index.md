# NTU Motion Capture Dataset
This dataset is created as a part of a research project that aims to improve the accuracy of Kinect V2 upper-body skeleton tracking.

## Specifications
- 6 subjects (3 males, 3 females)
- 6 movement sequences
- 39,311 depth frames (~22 minutes of record at 30 fps)
- Data from Kinect V2 
    - Ensure data from hips and above (usually get cropped at the knees)
    - Depth frame (transformable to 3D point cloud)
    - Body index frame (which depth pixel is a part of human body)
    - Kinect skeleton from Kinect SDK 2.0
    - 30 fps
    - Frame timestamp
- Data from 3 nine-axis inertial measurement units (IMU)
    - Raw data from a 3-axis accelerometer, a 3-axis gyroscope, a 3-axis magnetometer
    - 2 IMUs are on the subject's wrists, 1 IMU are mounted regidly on the Kinect. (see [our paper]() for more details)
    - 80 fps
    - Sample timestamp (transformable to Kinect timestamp)
- Data from a marker-based multi-camera system (Vicon)
    - 8 cameras
    - 100 fps
    - 27 marker positions from hip and above (Plug-in Gait model)
    - come with anthropometric measurements that allow the calculation of joint centers (shoulder, elbow, wrist)
    - Frame timestamp
- Time offset between Kinect and Vicon system is provided in all records for synchronization
- Transformation between Kinect and Vicon reference frame is measured and provided
    
## Organization


## Citation
If you gain something from our data, please cite our publication (to be updated soon).

## Download
You can download them [here](https://drive.google.com/drive/folders/0Bz8_iLTGY2o4b25FYWkwUU9BWjA). 
**WARNING**: All the files are 27.3GB in size. Try not to downlod all of them at once. 

## Want to visualize the dataset quickly?
You can download an executable program [here]() (Windows only).
The source code are also available [on GitHub](). This code should allow you to understand our binary file structure to build your own file reader in the case you are not going to use C#.

## Contact Us
My name is Prayook Jatesiktat. Feel free to contact me at prayook001@e.ntu.edu.sg
I'm from Robotics Research Center, Nanyang Technological University.
