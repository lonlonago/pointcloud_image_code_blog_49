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

