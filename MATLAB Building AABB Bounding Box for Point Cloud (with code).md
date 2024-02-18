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

