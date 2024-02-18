#  Create a PCD file 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309573751996
  ```  
#  Read point cloud from pcd file 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309573751996
  ```  
#   Point cloud data splicing and field splicing 

 Main function parameter knowledge review: 

>  The specific meaning of argc, argv The argc and argv arguments are useful when compiling a program from the command line. main (int argc, char * argv [], char ** env), the first argument, the int argc, is an integer and is used to count the number of command-line arguments sent to the main function when the program is run. The default value in VS is 1. The second argument, the char * argv [], is a string array, an array of pointers to hold the pointed string argument, each element points to a parameter. The meaning of each member is as follows: argv [0] points to the full path name of the program to run argv [1] points to the first string after the program name is executed on the DOS command line argv [2] points to the second string after the execution program name argv [3] points to the third string after the execution program name argv [argc] is NULL The third parameter, env of char ** type, is a string array. each element of env [] contains a string of the form ENVVAR = value, where ENVVAR is environment variables and value is its corresponding value. Usually used less. 

##   Field splicing: point cloud field connection function concatenateFields () 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309573751996
  ```  
>  Connect two datasets that represent different fields. If the input dataset has overlapping fields (i.e., two containing the same fields), then the data in the second cloud (cloud2 in) will overwrite the data in the first cloud (cloud1 in). Parameters cloud1_in all fields in the connection created by the composite output dataset of the first input dataset parameter cloud2_in the second input dataset (overriding the first dataset of fields for those shared) parameter cloud_out input dataset 

##   Point cloud data splicing: add directly 

>  //cloud_c = cloud_a;

//cloud_c += cloud_b;

//cloud_c = cloud_b + cloud_a;

cloud_c = cloud_a + cloud_b; 

  The splicing result is related to the order of the added data 

##  test 

  Test code, including field stitching and data stitching, by entering the parameter "-f" or "-p", to achieve field stitching and character stitching examples: 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309573751996
  ```  
 Program call method 1, by entering command parameters in VS, to achieve control: 

 ![avatar]( 2021052016260980.png) 

  The second way to call the program is to directly call the generated exe file in the cmd command line: 

 Field stitching: 

 ![avatar]( 20210520162834899.png) 

 Data splicing:  

 ![avatar]( 20210520162930653.png) 

