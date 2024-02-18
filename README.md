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



--------------------------------------------------------------------------------

#  First, the principle of the algorithm 

 Just look at the code. 

#  Code implementation 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574527951
  ```  
#  III. Display of results 

 ![avatar]( 1f96bf5f1f1c4a5eab28542b2ea61c60.png) 



--------------------------------------------------------------------------------

#  First, the principle of the algorithm 

   According to the description in "GB/T36100-2018 Airborne LiDAR Point Cloud Data Quality Evaluation Index and Calculation Method-Specification", the density of airborne point clouds is the number of points per unit area, and its calculation method is as follows: where is the point cloud density, unit: unit/is the total number of point clouds, is the number of point clouds in the first water area, unit: unit, is the number of water areas, unit: unit, is the first water area, unit: 

#  Code implementation 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574542686
  ```  
#  III. Display of results 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574542686
  ```  
 ![avatar]( f7042097b881433ebedd6033ad032482.png) 

#  IV. Test data 

 Link: https://pan.baidu.com/s/1qPJY2usVBWGkdaq8VNoDog extraction code: ftx5 



--------------------------------------------------------------------------------

#  Function overview 

##  1. Algorithm overview 

 ![avatar]( 14eb5fbd625443b295d19a5bd778943b.png) 

   This function uses a beam of light model and then uses a footing algorithm to detect road angles at non-ground points. The Beam Model beam modeling steps are as follows: 

 1. Emit a series of beams of light from a lidar sensor mounted on an ego vehicle. The lidar sensor is the point of emission. 2. Divide the beam of light into beam of light zones according to the angular resolution of the sensor. 3. Determine the beam angle and beam length relative to the point of emission. 4. For each beam zone, determine the distance between the point closest to the point of emission and the point farthest from the point of emission. Calculate the normalized beam of light length as the ratio of the shortest distance to the longest distance. Toe-Finding Algorithm 1. Divide the beam of light zone into sectors according to the length of the normalized beam of light. 2. Update the sector with the specified MinSectorSize and SectorMergeThreshold values. 

##  2. Main functions 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574545575
  ```  
   Detect road angles in point clouds. Point clouds must contain non-ground points. 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574545575
  ```  
 Use one or more name-value parameters to specify options. For example, MinSectorSize = 10 specifies the minimum sector size required to detect road segments to be 10 degrees. 

 input parameter 

 Name-value corresponding parameter 

 output parameter 

##  3. References 

>  [1] YIHUAN ZHANG, JUN WANG, XIAONIAN WANG, et al. Road-Segmentation-Based Curb Detection Method for Self-Driving via a 3D-LiDAR Sensor[J]. IEEE transactions on intelligent transportation systems,2018,19(12):3981-3991. DOI:10.1109/TITS.2018.2789462. 

#  Code implementation 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574545575
  ```  
#  III. Display of results 

 ![avatar]( 72ce05c6b1944989be5ac5ba5ebf0a05.png) 

#  IV. Reference link 

 Matlab Point Cloud Toolbox - detectRoadAngles 



--------------------------------------------------------------------------------

#  I. Explanation 

   Use triangulation to create an in-memory representation of any two- or three-dimensional triangulated data in a matrix format, such as the delaunay function or the matrix output of other software tools. When using triangulation to represent data, you can perform topological and geometric queries that can be used to develop geometric algorithms. For example, you can look up triangles or tetrahedrons that connect to a certain vertex or share a certain edge, find their outer centers, or find other features. 

#  Create objects 

   To create a triangulation object, use the triangulation function and define the points and connections of the triangulation with the input parameters. 

##  1. Main function 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 202402030957458839
  ```  
   Use triangulation to join points in list T and matrix P to create a two- or three-dimensional triangulation representation. 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 202402030957458839
  ```  
   Creates a two-dimensional triangulated representation using the point coordinates specified in the form of column vectors x and y. 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 202402030957458839
  ```  
   Creates a three-dimensional triangulated representation using point coordinates specified in the form of column vectors x, y, and z. 

##  2. Input parameters 

 T - Triangulate join list,, specified as a matrix of m × n, where m is the number of triangles or tetrahedrons and n is the number of vertices per triangle or tetrahedron. Each row of T contains the vertex ID used to define the triangle or tetrahedron. The vertex ID is the line number of the input point. The ID of the triangle or tetrahedron in triangulation is the corresponding line number in T. P - points, specified as a matrix with columns corresponding to the x, y, and (possibly) z coordinates of the triangulation point. The line number of P is the vertex ID in triangulation. X - the x-coordinate of the triangulation point, specified as a column vector. y - the y-coordinate of the triangulation point, specified as a column vector. z - the z-coordinate of the triangulation point, specified as a column vector. 

##  3. Attributes 

 Points - Triangulation points, expressed as matrices with the following characteristics: 

 ConnectivityList - A triangulated list of connections, represented as a matrix with the following characteristics: 

#  III. Code examples 

##  1. Two-dimensional triangulation 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 202402030957458839
  ```  
##  2. Results display 

 ![avatar]( 8863e5d3b614471fbf870bf528dd4c80.png) 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 202402030957458839
  ```  


--------------------------------------------------------------------------------

#  First, process analysis 

    This example shows how to use the iterative closest point (ICP) algorithm to register a multi-viewpoint cloud to reconstruct a 3D scene. 

##  1. Overview 

    This example stitches together a collection of point clouds captured from multiple viewpoints by Kinect to construct a larger 3D view of the scene. This example applies ICP to two consecutive point clouds. This type of reconstruction can be used to develop a 3D model of an object or to build a 3D world map for simultaneous localization and mapping (SLAM). 

##  2. Point cloud registration in pairs 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574541665
  ```  
###  2.1. Point cloud downsampling 

    The registration quality depends on the data noise and the initial setting of the ICP algorithm. Preprocessing steps can be applied to filter the noise or set initial attribute values that suit your own data. In this example, the data is downsampled and preprocessed using a voxel filter with a side length of 10cm. The voxel filter divides the point cloud space into cubes, and replaces all points in the cube with the average of the points in each cube through its X, Y, and Z coordinates. 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574541665
  ```  
###  2.2. ICP registration 

    To register the two point clouds, the ICP algorithm is used to perform a three-dimensional rigid transformation of the downsampled data. The first point cloud is used as the reference point cloud, and then the estimated transformation is applied to the original point cloud (which is not downsampled) of the second point cloud. After registration, the joint spot cloud and processing of overlapping points are also required. First, find the rigid transformation that aligns the second point cloud with the first point cloud. Use it to convert the second point cloud into a reference coordinate system defined by the first point cloud. 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574541665
  ```  
###  2.3 Merge point clouds and deduplicate 

    The world scene can now be created with the registered data. Overlapping areas are filtered using a voxel filter with a side length of 1.5cm to reduce the storage requirements of the resulting scene point cloud and reduce the size of the merged point cloud to improve scene resolution. 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574541665
  ```  
 ![avatar]( 29ef9a2d43d247b985403f372637a8ab.png) 

##  3. Multiple point cloud registration 

    To form a larger 3D scene, repeat the same steps above to process the point cloud sequence. Use the first point cloud to establish a reference coordinate system. Convert each point cloud to a reference coordinate system. This transformation is the product of a pair of transformations. 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574541665
  ```  
 ![avatar]( 195597c3c0f04ce99363d9699e0241e2.gif) 

##  4. Adjust the display angle 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574541665
  ```  
#  II. Complete code 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574541665
  ```  
#  III. Reference link 

 Matlab Point Cloud Toolbox - 3-D Point Cloud Registration and Stitching 



--------------------------------------------------------------------------------

#  First, the principle of the algorithm 

 ![avatar]( aaa0a29104e9420882aa5621210654aa.gif) 

   The implementation is relatively simple, call the dialog box function to load the file into the point cloud reading function.  

#  Code implementation 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574541595
  ```  


--------------------------------------------------------------------------------

#  Function overview 

##  1. Algorithm overview 

   Extracting scan context descriptors from point clouds 

##  2. Main functions 

 Overloaded function 1: 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574535876
  ```  
   The scan context descriptor is extracted from the point cloud ptCloud. The scan context descriptor is a two-dimensional global feature descriptor of the point cloud that can be used to detect cyclic closures. The function first divides the points in the 3D point cloud scan into concentric radial and azimuthal bins, and then selects the maximum z height of the midpoints of each bin, thereby computing the descriptor. Overload Function 2: 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574535876
  ```  
   Specify options for parameters using one or more name-values. 

##  3. References 

>  [1] Zhen D, Yang B, Yuan L, et al. A novel binary shape context for 3D local surface description [J]. ISPRS Journal of Photogrammetry and Remote Sensing, 2017, 130:431-452. [2] Zou Xianghong. Correction of location consistency of vehicle point cloud in urban scene [D]. Wuhan University, 2019. [3] Zou Xianghong, Yang Bisheng, Li Jianping, et al. Correction of location consistency of vehicle point cloud in urban scene revisit [J]. Science and Technology of Surveying and Mapping, 2019, 007 (002) 😛. 101-111. Yang Bisheng. Point Cloud Intelligent Processing [M]. Beijing: Science Press, 2020:24-28. 

#  Code example 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574535876
  ```  
#  III. Display of results 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574535876
  ```  
#  IV. Parameter analysis 

##  input parameter 

##  Name-value corresponding parameter 

##  output parameter 

#  V. Reference links 

>  Matlab point cloud toolbox - scanContextDescriptor matlab point cloud toolbox - scanContextDistance 



--------------------------------------------------------------------------------

#  First, the principle of the algorithm 

##  1. AABB bounding box 

   AABB is the earliest bounding box. It is defined as the smallest hexahedron containing the object with edges parallel to the coordinate axis. Therefore, to describe an AABB, only six scalars are required. The AABB structure is relatively simple, the storage space is small, but the compactness is poor. Especially for irregular geometric shapes, the redundancy space is large, and when the object rotates, it cannot be rotated accordingly. The processing object is rigid and convex, which is not suitable for complex virtual environment situations involving software deformation. 

>  Quote from: Baidu Encyclopedia 

##  2. The implementation process 

#  Code implementation 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574545656
  ```  
#  III. Display of results 

 ![avatar]( 7203d682ba5642f6bafff0fe285fffe5.png) 

#  IV. Reference link 

 [1] matlab 点云可视化(4)——可视化点云包围框 



--------------------------------------------------------------------------------

#  First, the principle of the algorithm 

##  1. Implementation process 

    See the code 

##  2. References 

>  Shi Wen, Li Bijun, Li Qingquan. Image segmentation method of vehicle laser scanning distance based on projection point density [J]. Chinese Journal of Surveying and Mapping, 2005 (02): 95-100. 

#  Code implementation 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574592725
  ```  
#  III. Display of results 

 ![avatar]( e6801f0cd9b74930b186105e7e3be3b7.png) 



--------------------------------------------------------------------------------

#  First, the principle of the algorithm 

#  Code implementation 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574539094
  ```  
#  III. Display of results 

 ![avatar]( ecff8f954f6e4ed088781d9e486a62eb.png) 



--------------------------------------------------------------------------------

#  First, the calculation method 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574564630
  ```  
   Returns a matrix that stores the Normal values for each point in the input ptCloud. The function uses 6 adjacent points to fit a local plane to determine each normal vector. 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574564630
  ```  
 Also specify the number of points k for the local plane fit. 

#  Code implementation 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574564630
  ```  
#  III. Display of results 

 ![avatar]( 20210605110337590.png) 

#  IV. Reference link 

 [1] matlab点云工具箱——Estimate normals for point cloud [2] Matlab三维离散点云法向量与特征值的PCA计算方法 



--------------------------------------------------------------------------------

#  First, the principle of the algorithm 

##  1. Overview of the principle 

 ![avatar]( a707adf13e014978b9adb721ed74ba4d.png) 

   The covariance matrix of a point cloud coordinate is represented by the principal component of its eigenvectors, which form an orthogonal basis. The associated eigenvalues correspond to the variance in the direction of the eigenvectors. Assuming the eigenvalues are arranged in descending order, the third eigenvector is the least squares estimate of the normal vector of the adjusted plane. The square root of the third eigenvalue can be used as a measure of the reliability of the normal vector. This value corresponds to the standard deviation of the selected point from the estimated plane, and can therefore be interpreted as a measure of the roughness of the adjusted plane.  

##  2. References 

>  [1] Glira P , Pfeifer N , Briese C , et al. A Correspondence Framework for ALS Strip Adjustments based on Variants of the ICP Algorithm[J]. Photogrammetrie - Fernerkundung - Geoinformation, 2015, 2015(4):275-289. 

#  Code implementation 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574580157
  ```  
#  III. Display of results 

 ![avatar]( df97120aa5524dcf91fd00869d27b76c.png) 



--------------------------------------------------------------------------------

#  First, the principle of the algorithm 

##  1. Calculation process 

#  Code implementation 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574528189
  ```  
#  III. Display of results 

 ![avatar]( 1a061a19655a41f7ae7fde2c2ab31e7f.png) 



--------------------------------------------------------------------------------

##  First, the principle of the algorithm 

   Different sampling devices and different distances from the scene will cause differences in point cloud density. Existing methods for estimating point cloud density include distance-based methods and block-based methods. The distance-based average distance density representation method is to estimate the distribution density of point clouds by calculating the average distance of each point in the point cloud. The distance of a point is generally the distance between a point in the point cloud and the point closest to the point in the point cloud. In a point cloud with a number of points, the distance between a point and any other point is expressed, and the minimum distance between a point and other points is expressed. Then the average distance density of the point cloud is: the smaller the average distance, the denser the point cloud distribution, and the greater the density; the larger, the sparser the point cloud distribution, and the smaller the density. Therefore, it is feasible to estimate the point cloud density by the average distance. 

##  Code implementation 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574523305
  ```  
##  III. Display of results 

 ![avatar]( 20210707204128269.png) 

##  C++ version of the calculation results 

 ![avatar]( 20210302200048192.png) 

  Consistent result 



--------------------------------------------------------------------------------

#  I. Overview 

##  1. Algorithm overview 

   Mean: Used to calculate the mean of an array. 

##  2. Main functions 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574596219
  ```  
 Returns the mean of the elements of A along the first array dimension of size not equal to 1. 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574596219
  ```  
 Calculates the mean of all elements of A. This syntax works with MATLAB ® R2018b and later. 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574596219
  ```  
 Returns the mean on dimension dim. For example, if A is a matrix, then mean (A, 2) is the column vector containing the mean for each row. 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574596219
  ```  
 Computes the mean over the dimensions specified by the vector vecdim. For example, if A is a matrix, then mean (A, [1 2]) is the mean of all elements in A, because each element of the matrix is contained in an array slice defined by dimensions 1 and 2. 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574596219
  ```  
 Returns the mean of the specified data type using any of the input arguments in the previous syntax. The outtype can be'default ',' double ', or'native'. 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574596219
  ```  
 Specifies whether to include or ignore NaN values in the evaluation of any of the above syntax. Mean (A, 'includenan') includes all NaN values in the evaluation, while mean (A, 'omitnan') ignores these values. 

#  Code implementation 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574596219
  ```  
#  III. Display of results 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574596219
  ```  
 ![avatar]( caa2a1944ef04f099a1a923c7ba17748.png) 



--------------------------------------------------------------------------------

#  First, the principle of the algorithm 

##  1. Calculation process 

 The smaller the neighborhood, the flatter it is, and the larger the neighborhood, the greater the fluctuation. 

##  2. References 

>  Yu Wenli, Zhou Mingquan, Shi Wuyang, Wu Zhongke. Automatic registration method of point cloud based on curvature [J]. Journal of System Simulation, 2015, 27 (10): 2374-2379 + 2386. DOI: 10.16182/j.cnki.joss. 2015.10.022. 

#  II. SVD 

##  1. Main function 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574562431
  ```  
    Returns the singular values of a matrix, in descending order. 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574562431
  ```  
    Perform a singular value decomposition of the matrix, therefore. 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574562431
  ```  
    Generate a reduced decomposition for the matrix. 

    Reduced decomposition removes additional zero-valued rows or columns from the singular-valued diagonal matrix S, as well as columns in U or V that are multiplied by those zero-valued columns in the expression A = USV '. Removing these zero-valued columns and columns reduces execution time and storage requirements without affecting the accuracy of the decomposition. 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574562431
  ```  
    Generate another reduced decomposition for the m × n matrix A: 

##  2. Input and output parameters 

    For m > n m × n matrix A, the reduced factorizations svd (A, 'econ') and svd (A, 0) compute only the first n columns of U. In this case, the columns of U are orthogonal, and U is an m × n matrix that satisfies. For complete factorizations, svd (A) returns U in the form of a satisfied m × m unitary matrix. The range of columns A with corresponding non-zero singular values in U forms a set of standard orthogonal basis vectors. Different computers and versions ® MATLAB can generate different singular vectors that remain numerically accurate. The corresponding columns in U and V can be flipped over, as this does not affect the value of the expression A = USV '. 

 - For an m × n matrix A, the reduced decomposition svd (A, 'econ') will return S as a square of order min ([m, n]). - For a complete decomposition, svd (A) will return S of the same size as A. - If m > n, svd (A, 0) will return S as a square of order min ([m, n]). - If m < n, svd (A, 0) will return S of the same size as A. 

    For an m × n matrix A with m < n, the reduced decomposition svd (A, 'econ') computes only the first m columns of V. In this case, the columns of V are orthogonal, and V is an n × m matrix that satisfies. For a complete decomposition, svd (A) returns V in the form of an n × n unitary matrix that satisfies. Zero spaces with no corresponding non-zero singular values in V form a set of standard orthogonal basis vectors. Different computers and MATLAB versions can generate different singular vectors, which remain numerically accurate. The corresponding columns in U and V can be flipped over, as this does not affect the value of the expression A = USV '. 

#  III. Code implementation 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574562431
  ```  
#  IV. Display of results 

 ![avatar]( 830937b4edc84da7841d0547d49f79cf.png) 



--------------------------------------------------------------------------------

#  First, the principle of the algorithm 

   The formula for calculating a point outside the plane to the plane is: 

 Detailed derivation process see: point to plane distance. 

#  Code implementation 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 202402030957458607
  ```  
#  III. Display of results 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 202402030957458607
  ```  
 ![avatar]( cce1e39b544e42a1bcb069081bb54d5d.png) 



--------------------------------------------------------------------------------

#  First, the principle of the algorithm 

##  1. Algorithm overview 

   Calculating the maximum distance between points in the same point cloud is an important step to estimate the overlap degree in the 4PCS registration algorithm, and is the basis for realizing handwritten 4PCS and improving it. 

##  2. Main functions 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574548419
  ```  
   Returns the distance between each pair of observations in the X and Y directions using the metric specified by distance. 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574548419
  ```  
   Returns the distance using the metric specified by distance and DistParameter. DistParameters can only be specified if the Distance is'seuclidean ',' minkowski ', or'mahalanobis'. 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574548419
  ```  
   For any previous parameters, use the name-value parameter to modify the calculation. 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574548419
  ```  
   Also returns matrix I. Matrix I contains the index of the observed value in X corresponding to the distance in d. 

#  Code implementation 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574548419
  ```  
#  III. Display of results 

 ![avatar]( fb57b1b04c51467c8789b261cd77d313.png) 

#  IV. Reference link 

 [1] Pairwise distance between two sets of observations 



--------------------------------------------------------------------------------

#  I. Overview 

##  1. Convex hull 

   The convex hull (Convex Hull) is a concept in computational geometry (graphics). In a real vector space, for a given set, the intersection of all contained convex sets is called the convex hull. The convex hull of can be constructed by the convex combination of all the points in the interior. In two-dimensional Euclidean space, a convex hull can be imagined as a rubber band that just surrounds all the points. In loose terms, given a set of points on a two-dimensional plane, a convex hull is a convex polygon formed by connecting the outermost points, which can contain all the points in the point set. 

##  2. Main functions 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574552585
  ```  
 Compute the two- or three-dimensional convex hull of the points in the matrix P. 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574552585
  ```  
 Compute the column vector, and the midpoint of the two-dimensional convex hull. 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574552585
  ```  
  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574552585
  ```  
 Specifies whether to remove vertices that do not affect the area or volume of the convex hull. By default, tf is false. 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574552585
  ```  
 Also calculate the area or volume of the convex hull. 

#  Code example 

##  1. 2D point cloud convex hull 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574552585
  ```  
##  2. Results display 

 ![avatar]( feff9a222c564784a527bb005f0e837c.png) 

##  3. 3D point cloud convex hull 

 The three-dimensional convex hull is simplified by removing points that do not affect its volume. 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574552585
  ```  
##  4. Display of results 

 ![avatar]( 2faaff2c80694d44bd5c9b321a0601b2.png) 

 Primitive point cloud, 3D convex hull, simplified convex hull  

#  III. Parameter analysis 

##  input parameter 

##  output parameter 

>  To plot the output of convhull in two dimensions, use the plot function. To plot the output of convhull in three dimensions, use the trisurf or trimesh functions. 

#  III. Reference link 

 convhull 



--------------------------------------------------------------------------------

