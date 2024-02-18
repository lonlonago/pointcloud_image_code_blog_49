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
