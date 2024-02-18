#  I. main 

 Let's first look at the test section of the main () function in main_Semantic3D.py. 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 202402030957378309
  ```  
#  Second, the test method 

 The general process of the test is to continuously send samples to the model prediction on the test dataset, and then obtain the minimum probability of all points in the entire dataset. When the minimum value is greater than 3.5, the inference ends. The predicted results of each step will be merged into the corresponding point cloud file according to the weight. 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 202402030957378309
  ```  
#  III. Explanation of several important issues 

##  1. How to stitch the test results of each step into the entire point cloud file 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 202402030957378309
  ```  
 Each step is completed, this part of the point cloud prediction result is added to the corresponding overall point cloud, the corresponding overall point cloud file is found by c_i, and the position of the predicted point on the overall point cloud is corresponding to the inds, and the test score is added to the output result of the previous step by weighted average. 

##  2. When will the entire test stop? 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 202402030957378309
  ```  
 After each round of testing is completed, the minimum value of all point probability values is counted, and if the minimum value is greater than 3.5, the inference is completed. 

##  3. Invalid value processing 

 Since 0 is an invalid value in the Semantic3D data, and points labeled 0 do not participate in the training when the model is trained, the probability of the column corresponding to 0 predicted by the model corresponds to the actual label of 1. In order to correspond to the actual label, the author adds a column to the predicted probability value, and the probability output value corresponding to the invalid value is set to 0. 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 202402030957378309
  ```  
 To illustrate with an example, suppose there are 3 points, there are 4 categories, and 0 is an invalid value, so the probability value output by each point model is 3, assuming that it is a 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 202402030957378309
  ```  
 The category labels of the 3 points we obtained through argmax () are 2, 0, 2, because 0 is an invalid value, and the label of the actual prediction result should be added by 1, so the final corresponding category labels of these 3 points are 3, 1, 3. Let's take a look at the author's thinking 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 202402030957378309
  ```  
 Use insert () to add a value of 0 to the first column, and then use argmax () to calculate the label of the predicted result. 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 202402030957378309
  ```  
 In this way, the label of the predicted result corresponds to the actual situation. In comparison, we can see that the author's method is more general, and it is also applicable to cases where the invalid value is not 0. 

##  4. How to upsample the model inference results back to the original point cloud 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 202402030957378309
  ```  
 The point cloud file is downsampled during preprocessing, so the test results need to be upsampled to the point cloud before interpolation. The proj file generated during preprocessing is used here. For the specific usage method, see the tf1.x version of RandLA-Net source code interpretation (1): Data preprocessing 

