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

