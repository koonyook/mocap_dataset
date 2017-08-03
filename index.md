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
- There are 3 male subjects with name MA, MB, MC and 3 female subjects with name FA, FB, FC
- There are 4 folders at the top level
    - **measure/** contains anthropometric measurements from each subjects. These info are needed to calculate shoulder, elbow, and wrist joint centers from marker positions. All files are in text form. All values are in mm unit.
    - **beta/** contains 10-dimensional shape vector form each subjects. These values are the result of model personalization process described in the main paper. All files are in text form.
    - **lowResolutionSmplTemplate/** contains 2 fsmpl files for a male model and a female model. The *fsmpl* format is designed specificly for this task. For more details, please look at the code.
    - **mocapRecord/** contains 2 subfolders
        - **fullbody/** contains full-body records from 6 subjects. They are used in the personalization process to search for the shape vector (beta). The records contain depth frame from Kinect only.
        - **upperbody/** contains the actual dataset for evaluation with data from Kinect, IMUs, and Vicon.

## Structure of One Record


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
