 tensorflow: 2.2.0 python:3.7 cuda:10.1 cudnn:7.6 GPU:2080TI 

#  1. Compile the cpp module 

##  1.1. Compile the downsampling module 

 In cmd enter cpp_wrappers\ cpp_subsampling execute the command 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309573799302
  ```  
 grid_subsampling .cp37-win_amd64 .pyd file is generated after compilation. 

 ![avatar]( 8299ed7136f946f9a1dd44d80b0440cc.png) 

##  1.2. Compiling the nearest neighbor search module 

 In cmd enter nearest_neighbors execute the command 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309573799302
  ```  
 After compilation, the nearest_neighbors .cp37-win_amd64 .pyd file will be generated. Although we were able to compile successfully, the nearest neighbor searched by the module is wrong in actual use, which also leads to the problem of training randlanet model under windows system with particularly low accuracy. 

 In nearest_neighbors folder there is a test.py script that we can use to test whether our compiled module is correct. 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309573799302
  ```  
 The code automatically generates 16x81920 points, 16 is batch_size, and then use the compiled nearest neighbor search module nearest_neightbors search for the nearest 16 points around each point, and return the ID number of the nearest 16 points around each point. After printing, we can find obvious errors. 

 ![avatar]( c5a31a17929b4fbe98bffbf8d90ae47b.png) 

 The reason for this problem is explained in this issue of the RandLANet github project. 

 ![avatar]( 71a825e0e7f741b89de54aa0f429b656.png) 

 The general meaning is that the long in windows is 32-bit, while the long in Ubuntu is 64-bit, so you need to change the np.long in knn.pyx to np.longlong, and the long in knn.pyx, knn_, knn_ all change to long long, and then recompile. 

 After compiling, we execute test.py script again, and we can find that the ID numbers of the nearest 16 searched are within 81920, indicating that the nearest_neightbors module compiled at this time is correct. 

 ![avatar]( e4600d1f72184c109694f246a3bb43fa.png) 

 I uploaded the modified code and compiled files to the network disk. Link: https://pan.baidu.com/s/14hI_IsrRY_4Q2qhex14MSQ Extraction code: 8rjk 

#  2. Data preprocessing 

 The main thing to do in this step is to down-sample, build a kdtree, and generate a projection proj file. Before running the code, you need to modify two places. The first is to modify the script helper_tool.py 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309573799302
  ```  
 The second is to modify the script utils\ data_prepare_semantic3d.py (take the semantic3d dataset as an example) 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309573799302
  ```  
 Finally, modify the data path to its own data storage path and execute the script to preprocess the data 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309573799302
  ```  
#  3. Training and testing 

 Refer to previous blog: Training Semantic3D dataset with RandLA-Net in tensorflow 2.0 environment 

