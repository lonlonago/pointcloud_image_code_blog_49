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

