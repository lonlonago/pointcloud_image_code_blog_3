 The Dataset class of KPConv records the key execution process of the Dataset class of KPConv. Here we verify the main operations of the Dataset class through visual means. 

#  First, the main function modification 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309573724097
  ```  
 Add traversal of the dataset in the main function, mainly using the session to execute the dataset. flat_inputs this sentence, the dataset class will iteratively perform data reading operations, in order to facilitate further visualization, I have only selected one training data here, 

 ![avatar]( 6bba0b94ef974f7ca389a75c06f49add.png) 

 There are also some other code modifications, as follows: The init_input_pipeline () method of the dataset class is modified, because there is only one training data, so the initialization of the verification operation needs to be commented out. The code location is in datasets\ common.py 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309573724097
  ```  
 Also because there is no validation data, the relevant part needs to be commented out in the load_subsampled_clouds () method. The code is in datasets\ Semantic3D.py 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309573724097
  ```  
 Let's do it. 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309573724097
  ```  
 ![avatar]( af0dc883a28d4bb887697fda25253901.png) 

#  get_batch_gen () visualization 

 In order to better understand the data reading mechanism of KPConv, we will save the data. First configure the modification, in the training_dataset.py Semantic3DConfig class, change the number of threads and iterations to 1. 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309573724097
  ```  
 get_batch_gen () is a generator that obtains point cloud data iteratively and returns the read data through the yield keyword. The main implementation code is in the spatially_regular_gen () in datasets\ Semantic3D.py. The approximate process is to randomly assign a probability value to each point of each point cloud file, find the point with the smallest probability value among all points, and then use the nearest neighbor search to select all points within the r radius. It should be noted that KPConv's strategy for selecting points is radius search. Since the density of points is inconsistent, the number of points searched at different points is different each time. Therefore, it is impossible to organize the points searched for multiple times into a three-dimensional format of [B, P, C] (B: batch_size, P: the number of points per sample, C: the number of features of a point). Only the points searched for multiple times can be stacked, which is [sum ( 

            p 

            i 

          p_i 

      The two-dimensional form of pi), C]. In order to distinguish which points belong to the same sample, it is recorded with an array, such as [200, 100, 300] means that the first 100 points belong to the first sample, the middle 100 points belong to the second sample, and the last 300 points belong to the third sample. corresponding to the following code 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309573724097
  ```  
 Then when the number of points obtained meets the requirements, through the yield function to return, you can see that the return uses numpy's concatenate () method to stack a batch_size points together. 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309573724097
  ```  
 In order to see each searched point, we save the points we read each time, and in order to stack with the entire point cloud file, we remove the operation of zero coordinates. 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309573724097
  ```  
 Execute the program, you can see that the txt file has been saved. 

 Let's check it in cloudpoint. 

 ![avatar]( 5e5525d2abd64e9abd77a355e7588161.gif) 

#  Visualization of dataset output 

 Now we visualize the output of the dataset, which is the out in the main function. 

 The key part of the whole dataset is two parts, get_batch_gen () is a generator, responsible for obtaining samples, return to get_tf_mapping () through yield, the second section mentioned KPConv's data reading strategy, KPConv will be batch_size search results stitched together, organized into a two-dimensional form of [sum (), C], and will also save the number of points searched for each batch for easy analysis, corresponding to the following code. 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309573724097
  ```  
 get_tf_mapping () is responsible for preprocessing the obtained sample, mainly including data enhancement and network input preparation. This part of the code is in the get_tf_mapping () function of datasets\ Semantic3D.py. 

##  data augmentation 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309573724097
  ```  
##  Network input preparation 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309573724097
  ```  
 The input_list here is the output result after executing sess.run (dataset.flat_inputs), which is a list, containing 29 arrays. The meaning of each array is introduced in the last section. We only use the first array (the coordinates of the points), the 21st array (the color of the points), and the 25th array (the labels of the points) here. Since KPConv stacks all the points of a batch_size together, we directly save the points that will only be stacked together, and cannot be compared with the data read in the second section of get_batch_gen (). Here we modify the input_list and add a stacks_lengths. This array saves the number of points read each time. 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309573724097
  ```  
 Remember to modify the operation of zero coordinates in get_batch_gen () 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309573724097
  ```  
 Finally, we modify the main function as follows. 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309573724097
  ```  
 Result saved by the generator 

 ![avatar]( d302fd5392c84cdc8e443a1ce91c8a7e.png) 

 Dataset. flat_inputs saved results 

 ![avatar]( 973479d6ce534e08838a1069cc871b58.png) 

 By the number of last dots in the file name, the same sample can be preprocessed before and after corresponding. 

 ![avatar]( 1c00d428fa1947b688eb572234667308.gif) 

#  get_tf_mapping () visualization 

 In this section, we mainly introduce the meaning of the 29 arrays in the dataset.flat_inputs output list of KPConv. It includes the return result of tf_segmentation_inputs, and then adds 4 arrays: scales (zoom parameter), rots (rotation parameter), point_inds (point id), cloud_inds (point cloud file id). The code is as follows 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309573724097
  ```  
 Let's take a look at what tf_segmentation_inputs returned. 

##  Network input data lake visualization 

 Code in datasets\ common.py 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309573724097
  ```  
 object_labels is None, tf_segmentation_inputs () returns results including input_points, input_neighbors, input_pools, input_upsamples, stacked_features, stacked_weights, stacked_batch_inds_0, stacked_batch_inds_1, point_labels. input_points, input_neighbors, input_pools, input_upsamples are lists of 5 arrays, tf_segmentation_inputs () returns 4 * 5 + 5 = 25 arrays, so there are 29 arrays in the dataset.flat_inputs output list. 

 In this section we mainly introduce the meaning of input_points, input_neighbors, input_pools, input_upsample. This part mainly involves the coordinates of the input points of different layers in the network, and the id of the points within the r radius around the points. Let's take a look at the network structure first, the code is in the training_Semantic3D.py. The elements in the list are the names representing each layer. 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309573724097
  ```  
 It is important to resnetb_strided layer, similar to the downsampling operation, but instead of using pooling to downsample, it simulates the convolution of increasing step size to downsample. The corresponding code is in tf_segmentation_inputs (). The code comments for tf_segmentation_inputs () have been read in the source code: KPConv's Dataset class. Here are a few key places to focus on. 

 Nearest neighbor search, get conv_i 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309573724097
  ```  
 This step uses tf_batch_neighbors to search for the id of points in the r neighborhood around the input point. 

 Downsample to get pool_p, pool_b 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309573724097
  ```  
 pool_p record the id of the sampled points, poo_b record the number of points after each sample is sampled. We said before that the number of points searched by KPConv is inconsistent each time. Therefore, some points in a batch_size are stacked together. In order to distinguish which points belong to a sample, it is recorded with an array alone. For specific explanations, please refer to the data reading strategy. Then when downsampling, this array also needs to be downsampled, indicating which points in the sampled points belong to the same sample. We need to use this array to parse when visualizing the points of different layers later. 

 Upsampling, get pool_i, in the encoding - decoding network architecture because the encoder will reduce the amount of data, the decoder to restore the original amount of data need to do the sampling operation, and the two-dimensional image is different, the point cloud is used to sample the nearest neighbor search. For example, if there is only one layer in the encoding and decoding part, the encoder becomes 786 points after downsampling from 1000 points, and then needs to resample back to 1000 points in the decoder. In fact, these 1000 points are still 1000 points of the input, and the position remains unchanged. What the upsampling in the point cloud does is how to assign the characteristics of 786 points to these 1000 points. I need to know which of these 1000 points is the closest point to the 786 points, assuming it is, and then assign the feature value to. This completes the upsampling operation. It should be noted that although the upsampling is used in the decoder, pool_i calculation is done in the encoder, because here only involves the operation of coordinates, the pool_i can be calculated immediately after downsampling, and then used in the corresponding upsampling layer. So we can see that the nearest neighbor search tf_batch_neighbors () is used here, but the input part becomes the point pool_p after downsampling and the corresponding upsampling point stacked_points. 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309573724097
  ```  
 Update 4 lists after completing a layer. 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309573724097
  ```  
 The network structure has a total of 5 layers, so there are 5 arrays in each list, so there are 20 arrays in total. Let's visualize the points of each layer. Since the points are stacked together, we need to make the following modifications to resolve the points of different layers of each sample. Add a input_batches_len to the return list. This data records the sample attribution of the points in each layer. 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309573724097
  ```  
 Then save the samples in the main function 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309573724097
  ```  
 The result is as follows. Layer in the output file name represents the layer, and batch actually represents the serial number of sample in a batch_size, so that we can compare the number of points in different layers in a sample, and we can see that from the first layer to the fifth layer is the most recent decrease. 

 ![avatar]( a451e0c124e8490bb3c4357f044a13fd.gif) 

 Ah, I'm finally done. There may be some omissions in some details. If there are any problems, you can point them out in the comments. 

