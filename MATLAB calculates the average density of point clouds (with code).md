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

