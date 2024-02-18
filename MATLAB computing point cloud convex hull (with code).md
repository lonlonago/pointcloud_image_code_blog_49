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

