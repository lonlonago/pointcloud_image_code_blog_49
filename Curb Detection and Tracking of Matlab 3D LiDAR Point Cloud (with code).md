 ![avatar]( 1c402d73a46f49c6a7c11ff4d82e74b4.png) 

   This example shows how a curb can be detected and tracked in a LiDAR point cloud. A curb is a stone or concrete line that connects a road to a sidewalk. A curb is a dividing line between the driveable areas of a road. In the absence of a GPS signal, detecting curb position is important for path planning and safe navigation in autonomous driving applications. This example uses a subset of the PandaSet dataset from Hesai and Scale. The PandaSet contains LiDAR point cloud scans of various urban scenes captured using Pandar64 sensors. 

##  Introduction 

   Curb detection of a LiDAR point cloud involves detecting the left and right curbs of the road relative to the self-vehicle. The LiDAR sensor is mounted on the top of the vehicle. Detect curbs in the point cloud data captured by the LiDAR sensor using the following steps: 1. Extract Region of Interest (ROI) 2. Classify ground points and non-ground points 3. Determine road angles using non-ground points 4. Detect candidate curb points using points on the road 

##  Download Lidar Data Set 

   The dataset is 109 MB in size and contains 50 preprocessed organized point clouds. Each point cloud is specified as a 64 × 1856 × 3 array. The ground truth data contains semantic segmentation labels for 13 classes. The point clouds are stored in PCD format and the ground true value data is stored in PNG format. Download the PandaSet dataset using the helperDownloadPandasetData help function, defined at the end of this example. 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574511657
  ```  
 Select the first frame of the dataset for further processing. Visualize the point cloud. 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574511657
  ```  
 ![avatar]( 90d47fb9aa0f4b0f86e2ee7e69855878.png) 

##  Preprocess Data 

   As a pre-processing step to detect roadside points, an area of interest is first extracted from the point cloud and the points within it are classified as either road points or non-road points. Based on where the LiDAR sensor is installed, the point cloud data is sparse beyond a certain distance. To ensure that the point cloud you extract is dense enough for further processing, specify the ROI within a limited distance of the sensor. 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574511657
  ```  
 ![avatar]( 11197cfdf27c457cb55fef15afa0c58c.png) 

 Use the following labels to divide the point cloud into road points and non-road points:  

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574511657
  ```  
 ![avatar]( 064b0e2290494c4cb0286b4754cd5837.png) 

##  Detect Road Shape 

 ![avatar]( 03000518c87d46b3b1027bf9a96cbe84.png) 

   Use the detectRoadAngles function to detect the road angle in the off-road point cloud. This function applies the beam model to non-ground points. For more information on the beam of light model, see [1] and [2]. Then, a customized version of the footing algorithm [3] is applied to the normalized beam of light length to find the road angle.  

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574511657
  ```  
##  Detect Road Curbs 

   Use the segmentCurbPoints function to segment curb points from the road point cloud. The steps for this function to calculate constraint points are as follows: 1. Extract feature curb points from points on the road. To identify curb points in the point cloud on the road, model the road curb using the following spatial features: 

 Smoothness Feature - This feature checks the smoothness of the area around a point. Higher smoothness values indicate that the point is an edge point, and lower smoothness values indicate that the point is a plane point. Height Difference Feature - This feature checks the standard deviation and maximum height difference around a point. Horizontal and Vertical Continuity Feature - This feature checks the horizontal and vertical continuity of a point with respect to its neighbors. The function calculates these features for each point on each scan line. Points that meet the above feature thresholds are called feature suppression points. 2. Compute candidate edge points from feature edge points. There may be erroneous feature suppression points. To remove false feature points, the function uses a quadratic polynomial fitting based on RANSAC to further process the feature suppression points to extract candidate suppression points. 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574511657
  ```  
 ![avatar]( c4bc9b16f72b4eb6a56b4cbb417e7303.png) 

##  Track Curb Points 

   Cyclic processing of LiDAR data to extract and track candidate curb points. Tracking of suppression points improves the robustness of suppression detection. You can stop curb tracking on a segmented road and start again when the self-vehicle leaves the segmented road. Curb tracking involves a polynomial fit to the x-point, expressed using a 2-degree polynomial as, where are the polynomial parameters. Curb tracking is divided into two steps: 1. Tracking constraint polynomial parameters a and b to control the curvature of the polynomial. 2. Tracking suppression polynomial parameters c to control the drift of the polynomial. 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574511657
  ```  
 ![avatar]( d9a86b8183e244ab81b1065d4e8487f2.png) 

##  Analyze Drift and Smoothness of Curb Tracking 

   To analyze the curb detection results, compare them with the tracked curb polynomials, plotting them as graphs. Each graph compares the parameters with no Kalman filter. The first graph compares the roadside drift along the y-axis and the second compares the smoothness of the roadside polynomials. The smoothness is the rate of change of the slope of the roadside polynomials. 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574511657
  ```  
 ![avatar]( 3c972f92fce043048997984ba0a3cefc.png) 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574511657
  ```  
 ![avatar]( 15f178ab7d6f44ca96e27d9c3a362262.png) 

##  Helper Functions 

 helperDownloadPandasetData auxiliary function loads the lidar dataset into the MATLAB workspace. 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574511657
  ```  
 helperTrackCandidateCurbs auxiliary function uses a Kalman filter to track candidate suppression points. 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574511657
  ```  
##  References 

>  [1]Zhang, Yihuan, Jun Wang, Xiaonian Wang, and John M. Dolan. “Road-Segmentation-Based Curb Detection Method for Self-Driving via a 3D-LiDAR Sensor.” IEEE Transactions on Intelligent Transportation Systems 19, no. 12 (December 2018): 3981–91. https://doi.org/10.1109/TITS.2018.2789462.

[2] Wang, Guojun, Jian Wu, Rui He, and Bin Tian. “Speed and Accuracy Tradeoff for LiDAR Data Based Road Boundary Detection.” IEEE/CAA Journal of Automatica Sinica 8, no. 6 (June 2021): 1210–20. https://doi.org/10.1109/JAS.2020.1003414.

[3] Hu, Jiuxiang, Anshuman Razdan, John C. Femiani, Ming Cui, and Peter Wonka. “Road Network Extraction and Intersection Detection From Aerial Images by Tracking Road Footprints.” IEEE Transactions on Geoscience and Remote Sensing 45, no. 12 (December 2007): 4144–57. https://doi.org/10.1109/TGRS.2007.906107. [4] Curb Detection and Tracking in 3-D Lidar Point Cloud 

