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

