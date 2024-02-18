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

