#  First, the preprocessing steps 

 1.1, according to the distance of 0.01 sampled once, the point cloud is saved as a ply file, stored in the origin_ply folder 1.2, according to the distance of 0.06 and then sampled, point cloud information is saved as a ply file, saved in the input_0 folder. 1.3, according to the second step after the sampling point to establish kdtree, named point cloud name _KDTree .pkl, saved in the input_0 folder. 1.4, using the generated kdtree, query out the point cloud in the origin_ply point distance input_0 point in the nearest point of the serial number, saved as point cloud name _proj .pkl file, saved in the input_0 .06 file. 

#  Code analysis 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309573750435
  ```  
#  III. Description of kdtree file and proj file 

 The preprocessing operation generates a downsampling file, a kdtree file, and a proj file based on each point cloud file. Here we mainly explain the functions of the kdtree and proj files. 

##  3.1. Instructions for using the kdtree file 

 In the point cloud semantic segmentation model, the nearest N (such as 8192) points around each point will be searched as an input sample. Establishing a kdtree file is convenient for this step. First, we define several points, create a kdtree, and then save the kdtree as a pkl file. 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309573750435
  ```  
 Here, the generated kdtree will be saved as a binary file, using the kdtree file 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309573750435
  ```  
 output result 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309573750435
  ```  
##  3.2. Instructions for using the proj file 

 The amount of raw point cloud data collected by the device is very large. Generally, the amount of data in the point cloud will be reduced by downsampling without affecting the shape characteristics of the point cloud. Therefore, we need to restore the original point cloud after semantic segmentation of the downsampled point cloud. This step requires a proj file. In fact, this step of recovery uses nearest neighbor interpolation, that is, I want to know the category label of each point in the original point cloud. I need to find the point in the original point cloud that is the closest point in the downsampled point cloud that has been semantically segmented, and use the label of this point as the label of the point in the original point cloud. 

 Here we define two point clouds a and b, assuming that a is the original point cloud and b is the sampled and labeled point cloud, and create a proj file according to kdtree 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309573750435
  ```  
 Using the proj file 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309573750435
  ```  
 output result 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309573750435
  ```  
 B is the sampled point, b_label is the label of each point, a is the original point, we want to know the label of each point in a, such as the first point in a [2,2,2], first find [2,2,2] The closest point to the point in b, proj [0] = 1, indicating that the point in a [2,2,2] is the closest to the second point in b [1,1], assign the label 2 of [1,1,1] to a, so the first value of the output label is 2, the other points in a and so on. 

 The next blog post will introduce the data flow operation of RandLANet: RandLA-Net source code interpretation (2): Dataset in tf1.x. 

