Recently, I have been doing point cloud semantic segmentation. RandLA-Net is a relatively new semantic segmentation network for large-scale point clouds. I have been using the torch version of the code to train my own dataset, and the training results have been poor. At the same time, my training results on the Semantic 3D dataset are also very poor. There are several types of accuracy that are always 0, and the final average iou is only more than 20%, which is very different from the experimental results given in the author's paper. 

 In order to verify whether it is a problem with the pytorch project code I use, I plan to test the Semantic3D dataset on the code provided by the author himself. The author of RandLA-Net published the tensorflow version of the code on github, and it is tensorflow 1.11. I trained the model before. It has always been torch, cuda installed 10.2, and the 1.0 version of tensorflow cannot use the gpu in the cuda10.2 environment (someone on the Internet has succeeded, but I have never succeeded 😭, and then I don't really want to lower my cuda version, because my torch version is also relatively high), so I tried to train the 1.0 version of the code in the 2.0 environment. The following is the training process record. 

###  Modification method 

 Since the author did not use a more complex method, to train the code of tensorflow 1.0 in the tensorflow 2.0 environment, you only need to make the following modifications when importing tensorflow. The code used in the project 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309573766452
  ```  
 Replace with 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309573766452
  ```  
 The scripts that need to be modified are main_Semantic3D.py, RandLANet.py, helper_tf_util.py. 

###  Training Semantic3D dataset steps 

 1, compile C++ code, data preprocessing used for downsampling and nearest neighbor search using C++ code to write the program, to use python call need to compile first. 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309573766452
  ```  
 2. Data preparation. This step is to save the point cloud in ply format first, then downsample and save the kdtree and projection files. 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309573766452
  ```  
 Running data_prepare_semantic3d.py 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309573766452
  ```  
 3. Train the model, preferably on the command line. I run the program directly in pycharm without calling the GPU. 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309573766452
  ```  
 The average IOU obtained after 100 rounds of training was 70.3%, and the best IOU recorded was 70.632%, which was the result of the 87th round of training. 

 ![avatar]( 2058b9d6d0e644dea574764ea897a678.png) 

 ![avatar]( 2b8d2493f7904b6aaddc5c5c509836bf.png) 

###  Reduce-8 test results 

 There are a total of four test data for reduce-8, and the test set is tested with the trained model 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309573766452
  ```  
 ![avatar]( 60122400b38843fc90f362e493cb6c49.png) 

 ![avatar]( 063f58a26ae24c1f90fb30bac06a8be2.png) 

 Test set official evaluation results, upload the test set results to the official website of Semantic3D, and the accuracy of the test results given is as follows: 

 ![avatar]( 4629701e016245b48be2f62ff114b4fb.png) 

 We can see that the model I trained myself ended up with 74.8% miou on the reduce-8 test set, and the best miou given in the author's article was 77.4%. 

