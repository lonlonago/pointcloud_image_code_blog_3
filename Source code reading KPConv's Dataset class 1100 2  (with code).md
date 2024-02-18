 Code address: KPConv Here we take the tensorflow version of the KPConv training Semantic3D dataset as an example to record the training process of the network step by step. The code is in the training_Semantic3D.py. First look at the main function 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309573770872
  ```  
 You can see that the main process is to configure the config, create a dataset, create a model, create a trainer, and finally call the train () method to start training. Here we mainly look at the network configuration and data preprocessing. 

#  I. config 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309573770872
  ```  
#  Ii. dataset 

 Semantic3D dataset class in datasets\ Semantic3D.py, mainly including initialization (__init__), prepare data (prepare_data), loading the sampling point cloud (load_subsampled_clouds), obtain the generator (get_batch_gen), data enhancement (get_tf_mapping), and finally after the dataset is created there is an operation to initialize the pipline, this part is in datasets\ common.py, Semantic3DDataset inherits the dataset in common. 

 Note: In order to save space, I have only marked the key parts of the code for individuals here, and omitted the parts of the code that are easier to understand. 

##  2.1、__init__ 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309573770872
  ```  
 Semantic3Ddataset mainly defines the division criteria of training data and validation data, and performs preprocessing operations. 

##  2.2、prepare_data 

 Semantic3Ddataset initialization performed a pre-processing operation, I think this step is easier to understand, mainly is to read txt and label, according to whether the label file exists to distinguish between training and test data, training data txt format point cloud data first size is 0.01 under the grid sampling, and then saved as ply format. Training data is stored in ply_subsampled\ train, there are 15 ply point cloud files; test data is directly stored in ply_full\ reduced-8 without sampling, there are 4 point cloud files. 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309573770872
  ```  
##  2.3、load_subsampled_clouds 

 This step starts to load the data into the memory. First, the ply format point cloud saved by the prepare_data is sampled according to the size of 0.06m. The sampled data is established as kdtree, and then the projection file needs to be established for the validation set and test set data. For the function of the projection file, please refer to the data preprocessing source code interpretation of randlanet written by me before. 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309573770872
  ```  
##  2.4、get_batch_gen 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309573770872
  ```  
##  2.5、get_tf_mapping 

 It mainly performs data enhancement operations (tf_augment_input) on the data returned by the generator, and then obtains the input information of each layer of the network encoder (tf_segmentation_inputs). 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309573770872
  ```  
 tf_augment_input and tf_segmentation_inputs are implemented in datasets\ common.py. The data enhancement part is relatively simple, we will skip it here and mainly look at tf_segmentation_inputs part. 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309573770872
  ```  
 The next article will visualize the entire process, so that you can intuitively understand the process of obtaining data through the Dataset. Source code reading: KPConv's Dataset class visualization test 

