#  I. Introduction 

 Tensorflow1.x is through tf.data. Dataset and tf.data. Iterator to continuously organize the data to be entered into the model, a bit like torch's Dataset and Datasetloader. As a torch user, debugging tensorflow code is a headache, especially the 1.x version of the code. Before seeing this code, I reviewed the operation flow of the data processing part of tf1.x. The general order is as follows. Create a generator that reads data, create a dataset according to the generator, set the batch_size of the dataset, set the map operation of the preprocessing, and initialize the iterator. For details, see the two links given in the reference. 

#  RandLA-Net dataset 

 In the data stream of randlanet, I think there are two key parts, the generator function that reads the original data source get_batch_gen and the map function that preprocesses the data, because my own data set is similar to Semantic3D, so I use Semantic3D's data stream source code to interpret. Semantic3D's data stream operation is in the Semantic3D class, this class contains initialization (__init__), data loading (load_sub_sampled_clouds), data reading generator (get_batch_gen), preprocessing operation (get_tf_mapping), data enhancement (tf_augment_input), data stream initialization (init_input_pipeline) and other parts. We explain each specific operation in sequence. 

 Initialization: __init__ 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309573748265
  ```  
 The initialization part is to divide the dataset into training dataset, validation set, and test set. The one without label label file is the test set. Two of the label files are used as validation sets. The others are training datasets. The last line calls the function to load the data. Data loading: load_sub_sampled_clouds 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309573748265
  ```  
 Load the downsampled point cloud file, kdtree file and proj file by training dataset, validation set and test set. 

 Data Read Generator: get_batch_gen 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309573748265
  ```  
 The data reading generator function is to start reading the point cloud according to the set number of points (65536). Simply put, it is to find the file with the lowest probability value first, and then find the point with the lowest probability value in this file. With this point as the center, search for the nearest 65536 points. As the data of the point input model once, we will talk about the detailed process in the visualization part. Preprocessing operation: get_tf_mapping 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309573748265
  ```  
 1 point cloud data (65536 points) read by the generator needs to be preprocessed before entering the network training, such as enhancement, coordinates of points retained by each layer, etc. We will put the same detailed process in the visualization part. Data enhancement: tf_augment_input 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309573748265
  ```  
 The first step in the map operation is to enhance it first, including rotation, scaling, and other operations. We will discuss it in detail in the visualization section. 

 Data stream initialization: init_input_pipeline: 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309573748265
  ```  
 This part is to initialize the data stream. In the preface part, we introduce the initialization process of tensorflow1.x, which is to create a generator, create a dataset, set the batchsize, set the map, and initialize the iterator. 

#  III. Data flow visualization 

 In this part, we save a piece of point cloud (65536) data that we read each time, and also save the corresponding map-transformed data. 

 First look at the generator 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309573748265
  ```  
 In order to fully understand what the data flow part actually does, and how our entire point cloud data is fed into the model for training step by step, I plan to visualize this content. 

 First of all, we don't train the model here, we just look at the processing of the dataset, so we need to modify the main () function of the main_semantic3D.py. 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309573748265
  ```  
 In the above code, we only use to read the data, epoch represents how many rounds to read, the yield keyword in spatially_regular_gen () is used to return the data, we mentioned before that tf1.x iterates through the iterator iter.get_next () to continuously traverse the data, and this method of RandLAnet is implemented in init_input_pipeline (). 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309573748265
  ```  
 So we need to run the dataset.flat_inputs operation by calculating the graph sess, in each round of operation, continuously execute the dataset.flat_inputs to obtain a set of data, and trigger OutOfRangeError when the number of iterations exceeds the set number of iteration steps per round, so that we know that one round of operation has been completed, and then re-initialize the train_init_op to proceed to the next round of operation. 

 Next, we will save the point cloud read in each step. First, we set epoch = 1. At the same time, we only perform a few steps in the round. We need to modify it in the help_tool.py, and change the batch_size to 1 and train_steps to 3. This way, each round is only iterated 3 times. At the same time, for easier comparison, we only take one data to compare. I am using bildstein_station3_xyz_intensity_rgb this point cloud file here. 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309573748265
  ```  
 To save the data before the generator returns it, add a save statement at the end of spatially_regular_gen (). 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309573748265
  ```  
 After main_Semantic3D.py, you can see that there are 3 files in the current folder, but these 3 files are superimposed and cannot be compared with the original file. 

 ![avatar]( da98e8fb64454d8a94811202ea922e7f.png) 

 In fact, when we introduced spatially_regular_gen above, we mentioned that randlanet translated the coordinates of the read point cloud, and translated the center point (x, y) to (0,0). In order to compare the read sample data with the overall point cloud, we can first comment out this sentence. 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309573748265
  ```  
 Execute main_Semantic3D.py again 

 ![avatar]( 4f74d20c12be41e1ac6e0ec4a9fa7529.png) 

 Turn off the entire point cloud and only see the three small point clouds extracted. 

 ![avatar]( 9aeb4be71c4a4f048c65ec5aa0264494.png) 

 It can be found that the read point cloud data can be superimposed on the entire point cloud. In this way, we can know the reading mechanism of RandLANet for large point clouds. 

 Let's take a look at the map operation again. This step is to preprocess the data read by the generator (that is, the data we saved in the previous step). Similarly, we also save the operation in this step to make a visual comparison with the data saved by the generator. 

 First, let's go through the source code 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309573748265
  ```  
 We will also save the final output here, including the enhanced result, the result after each layer is sampled. Modify the main function of the main_Semantic3D.py as follows 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309573748265
  ```  
 ![avatar]( b01c7f1f2fcb423180a4b69db3640587.gif) 

 Enhance the before and after comparison, and you can see that the original point cloud has been rotated. Visualize the saved points after downsampling  

#  summarize 

 We learned about the dataset mechanism of RandLANet through visualization. The general process is as follows: 1. Load the point cloud, kdtree, and proj file 2. Randomly initialize a probability value for each point 3. Find the point with the smallest probability value (first find the large point cloud, and then find the point in the point cloud) 4. Continuously read the information of 65536 points through the generator and return it. 5. Realize the enhancement of the point cloud and the position of the points sampled at each layer through the map operation. 

 A torch deep user to see the source code of tf1.x is really too painful, who has a better tf1.x debugging method please teach me. 

#  reference 

 TensorFlow Efficient Pipeline Datasets and Iterators in TensorFlow Data Processing 

