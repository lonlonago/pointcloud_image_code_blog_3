#  environment 

 系统:Ubuntu18.04.4 tensorflow：2.2.0 python:3.7.6 cuda:10.2.89 cudnn:7.6.5 

#  Compile 

##  1.1 Compiling tf_custom_ops 

 The author's environment is tensorflow1.x, directly using the author's compile_op.sh script compilation will prompt can not find ltensorflow_framework 

 ![avatar]( 2d444e088fc941bb878cb8406909b4d8.png) 

 The problem lies in the - ltensorflow_framework parameter in the compile command line, and the author also pointed out that if the system is using Ubuntu 18.04, the parameter - D_GLIBCXX_USE_CXX11_ABI = 0 needs to be removed, but I can execute it normally without going. 

 Let's talk about how to modify it. First, check the links and compilation parameters in your own environment 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309573731003
  ```  
 ![avatar]( c6fc56abe79c4742b26fddba57ae3c6c.png) 

 It can be seen that the corresponding link parameter in tf2.x is -l: libtensorflow_framework.so, and the corresponding compilation parameter is D_GLIBCXX_USE_CXX11_ABI = 0. the corresponding link parameter in the tf2.x environment is different from that in the 1.x environment (-ltensorflow_framework), and the corresponding compilation parameter is the same. Therefore, we only need to modify the - ltensorflow_framework in the compile_op.sh to -l: libtensorflow_framework.so. 

 ![avatar]( 670a7ad11e204846a9d61db13f1a46fb.png) 

 Modify compile_op.sh and re-execute,  

 After recompilation, four .so files are generated 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309573731003
  ```  
 We can take one of them to test if it works. 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309573731003
  ```  
 ![avatar]( cf98322d4e544b91bd3145f98a346447.png) 

 You can see that the op operation can be loaded normally.  

##  1.2 Compilation cpp_warpper 

 Just run compile_wrappers.sh directly, I didn't encounter any problems when compiling. 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309573731003
  ```  
 ![avatar]( 734a5644de324f6aa0193ebb8ee16d77.png) 

 cpp_subsampling folder to generate the corresponding compilation file.  

#  II. Training 

 Modify the data path, on line 136 of datasets\ Semantic3D.py, modify self.path to your dataset. The way to import tensorflow is changed to 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309573731003
  ```  
 train 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309573731003
  ```  
 ![avatar]( 1d9e7d2f18f54a70a26f4beefc3e719b.png) 

#  IV. Testing 

 Use test set reduce-8 to test and test_any_model.py 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309573731003
  ```  
 Modify to 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309573731003
  ```  
 execute 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309573731003
  ```  
 ![avatar]( e5c731af905348e68e5bb352e3ca8b48.png) 

 The test results of reduce-8 will be generated in the test folder, and the predicted labels will be uploaded to the official website of semantic3D. The accuracy of the test set is as follows.  

#  reference 

 https://tensorflow.juejin.im/extend/adding_an_op.html https://stackoverflow.com/questions/48189818/undefined-symbol-ztin10tensorflow8opkernele 

