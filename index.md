# NTU Motion Capture Dataset
This dataset is created as a part of a research project that aims to improve the accuracy of Kinect V2 upper-body skeleton tracking.

## Specifications
- 6 subjects (3 males, 3 females)
- 6 movement sequences
- 39,311 depth frames (~22 minutes of record at 30 fps)
- Data from Kinect V2 
    - Ensure data from hips and above (usually get cropped at the knees)
    - Depth frame with 424x512 resolution (transformable to 3D point cloud)
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
<!---    - **lowResolutionSmplTemplate/** contains 2 fsmpl files for a male model and a female model. The *fsmpl* format is designed specificly for this task. For more details, please look at the code. (cannot publish becaused of the license -->
    - **mocapRecord/** contains 2 subfolders
        - **fullbody/** contains full-body records from 6 subjects. They are used in the personalization process to search for the shape vector (beta). The records contain depth frame from Kinect only.
        - **upperbody/** contains the actual dataset for evaluation with data from Kinect, IMUs, and Vicon.

## Structure of One Record
In a record folder (such as publishedDataset/mocapRecord/upperbody/FA2/), there are 4 files and 5 subfolders.
   - **kinectBaseQuaternion.bin** (binary) contains an orientation quaternion (4 floats in WXYZ sequence) that represent the orientation of the mounting base on the IMU in the Kinect reference frame. These values are from a calibration process.
   - **setting.SettingProto** (binary) contains some configurations about IMUs and Kinect.
   - **subject.name** (text) contains the name code of the subject.
   - **result.SessionProto** (binary) contains results from our implementation of shape fitting process.
   - **imu1/** contains information from IMU that is mounted on top of Kinect.
       - **gyroBiasStarter.bin** (binary) contains 3 gyroscope bias values at the starting point.
       - **magCalibrationParameters.bin** (binary) contains calibration parameters for magnetometer.
       - **RawSample.RawSampleListProto** (binary) contains the timestamp and the raw value from accelerometer, gyroscope, magnetometer.
   - **imu17/** contains information from IMU that is on the subject's right wrist. Forearm pointing direction is along IMU's Y axis.
   - **imu9/** contains information from IMU that is on the subject's left wrist. Forearm pointing direction is along IMU's -Y axis.
   - **kinect/** contains information from Kinect V2 sensor
       - **timestamp.bin** (binary) contains an array of timestamp for each frame in ms unit (double)
       - **depthBuffer.bin** (binary) contains depth images frame-by-frame. As one pixel takes 2 byte, each frame occupies 2x424x512 bytes.
       - **bodyIndexBuffer.bin** (binary) contains body index at every depth pixel. As one pixel takes 1 byte, each frame occupies 424x512 bytes.
       - **OfflineBodyframe.protobuf** (binary) contains the skeleton tracking results from Kinect SDK 2.0.
       - **cameraIntrinsics.bin** (binary) contains the focal lengths, principal points, and radial distortion coefficients of the used Kinect.
       - **depthToCameraSpaceTable.bin** (binary) contains the pre-calculated information that can be used to back-project any depth pixel into a 3D position in Kinect reference frame.
   - **vicon/** contains information from Vicon system
       - **viconRecord.TRC** (text) contains 3D position of 27 markers captured by Vicon system.
       - **viconPanelFile.TRC** (text) contains 3D positions of 4 markers on the calibration panel in the Vicon reference frame.
       - **kinectPanelFile.bin** (binary) contains 3D positions of 4 marekers on the calibration panel in the Kinect reference frame. With both *viconPanelFile.TRC* and *kinectPanelFile.bin*, the transormation between Kinect and Vicon reference frame can be calculated.
       - **marker.measure** (text) contains the diameter and the base thickness of the marker in mm.
       - **viconStartOffset.bin** (binary) contains a floting point number telling that at which frames in Kinect that the first vicon frame should start.
    
## Cite Us
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
