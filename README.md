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



--------------------------------------------------------------------------------

SLAM consists of two main tasks: localization and composition. In mobile robots or autonomous driving, this is a very important problem: for the robot to move accurately, it must have a map of the environment, so to build a map of the environment, it needs to know the robot's location. This series of articles is mainly divided into four parts: In the first part, we will introduce Lidar SLAM, including Lidar sensors, open source Lidar SLAM systems, deep learning in Lidar, and challenges and the future. The second part focuses on Visual SLAM, including camera sensors, open source visual SLAM systems for different dense SLAMs. The third part introduces visual inertial mileage method SLAM, deep learning in visual SLAM, and the future. In the fourth part, we will introduce the integration of lidar and vision. 

 Abstract, With the development of CPUs and GPUs, graphics processing power has become more and more powerful. Camera sensors have simultaneously become cheaper, lighter, and more versatile. In the past decade, visual SLAM has developed rapidly. Visual SLAM using cameras also makes the system cheaper and smaller compared to Lidar systems. Today SLAM visualization systems can run in miniature PCs and embedded devices, and even in mobile devices such as smartphones [1], [2]. 

 Visual SLAM usually involves the processing of sensor data, including cameras or inertial measurement units, visual odometry at the front end or odometry with visual inertial navigation fusion, optimization at the back end, closed loop at the back end, and map construction [3]. And relocation is another very important module of stable and accurate visual SLAM [4]. In the process of visual odometry, in addition to methods based on feature or template matching or related methods for determining camera motion, there is another method that relies on the Fourier-Mellin transform [5]. [6] and [7] give examples in environments where there are no obvious visual features when using ground cameras 

 Vision sensor 

 The most commonly used sensors based on vision SLAM are cameras, which can be divided into monocular cameras, stereo cameras, RGB-D cameras, event cameras, and others. 

 Monocular camera: Monocular camera-based visual slam has a scale problem corresponding to the actual trajectory and map size, which is what we often say, the monocular camera cannot obtain the true depth, which is the so-called scale uncertainty [8]. Monocular camera-based SLAM must be initialized and faces drift problems. 

 Stereo camera: Stereo camera is a combination of two monocular cameras, but the baseline distance between the two monocular cameras is known. Although depth can be obtained based on calibration, correction, matching, and calculation, the process is resource-intensive. 

 RGB-D Camera: An RGB-D camera is also known as a depth camera because a depth camera can directly output depth in pixels. A depth camera can be implemented through stereo, structured light and TOF technology. The theory of structured light is that the infrared laser emits some kind of pattern with structural features to the surface of the object. The infrared camera will then collect the pattern changes due to the different surface depths. The TOF will measure the laser's flight time to calculate the distance. 

 Event cameras: [9] illustrate that instead of capturing images at a fixed rate, event cameras measure the brightness change of each pixel asynchronously. Event cameras have high dynamic range (140 dB vs. 60 dB), high temporal resolution (by orders of magnitude), low power consumption, and are not affected by motion blur. Therefore, event cameras perform better than traditional cameras at high speed and high dynamic range. Examples of event cameras are dynamic vision sensors [10], dynamic line sensors [11], dynamic and dynamic active pixel vision sensors [12], and asynchronous time-based image sensors [13]. 

 Vision sensor products and companies 

 Microsoft: Kinectc v1 (Structured Lightweight), Kinect v2 (TOF), Azure Kinect (with microphone and IMU). 

 Intel: 200 Series, 300 Series, Module D400 Series, D415 (Active IR Stereo, Roller Shutter), D435 (Active IR) Stereo, Global Shutter), D435i (D435 with IMU). 

 • Stereolabs ZED: ZED stereo camera (up to 20m depth). 

 • MYNTAI: D1000 series (depth camera), D1200 (for smart phones), S1030 series (standard stereo camera). (Note: Xiaomi camera has cooperated with the official account, as long as you consult and buy on this platform, you can get a coupon of 100 yuan on the basis of the original price.) 

 • Occipital Structure: Structural sensor (for iPad). • Samsung: 2nd and 3rd generation dynamic vision sensors and event-based vision solutions [65]. Other depth cameras can be listed as follows, but are not limited to Leap Motion, Orbbec Astra, Pico Zense, DUO, Xtion, Camboard, IMI, Humanplus, PERCIPIO.XYZ, PrimeSense. Other event cameras can be listed as follows, but are not limited to: Innovation, AIT (AIT Austria TechAcademy), SiliconEye, Prophesee, CelePixel, Dilusense. 

 Image-based SLAM methods can be divided into direct methods and feature-based methods. Direct methods are methods for constructing semi-dense and dense maps, while feature-based methods are methods for constructing sparse feature points. 

 • Sparse Vision SLAM • MonoSLAM: (Monocular Camera) is the first real-time single SLAM system based on EKF [14]. • PTAM: (Monocular Camera) is the first SLAM system to track and build maps in parallel. It first employs bundle adjustment to optimize the concept of keyframes [15]. Higher versions support simple and efficient retargeting [16]. • ORB-SLAM: It (Monocular) uses three threads: tracking, building maps, and closed-loop detection [17]. ORBSLAM v2 [18] supports monocular, stereo, and RGB-D cameras. CubemapSLAM [19] is a monocular fisheye lens SLAM system based on ORB-SLAM. • Visual inertia ORB-SLAM [20] explains the initialization process of the IMU as well as joint optimization using visual information. • proSLAM: (Stereo Camera) is a lightweight visual SLAM system and is easy to understand [21]. • ENFT-sfm: (Monocular Camera) is a feature tracking method that efficiently matches feature point correspondence between one or more video sequences [22]. The newer version ENFT-SLAM can be run at scale. • OpenVSLAm: (supports all types of cameras) [23] is based on an indirect SLAM algorithm with sparse features. The advantage of OpenVSLAM is that the system supports perspective views, fisheye diagrams and isometric rectangles, and even supports any user-designed camera model. • TagSLAM: It implements SLAM via the AprilTag benchmark [24]. Moreover, it provides a front-end to the GTSAM factor graph optimizer that can design a large number of experiments. Other similar efforts can be listed below, but are not limited to UcoSLAM [25]. 

 Semi-Dense Visual SLAM 

 • LSD-SLAM: (monocular camera) presents a novel direct tracking method that can be run on Lie algebra and direct methods [26]. [27] Makes it support stereo cameras. • SVO: (monocular camera) is a semi-direct vision Odoemtry [28]. It uses image alignment based on sparse models for faster speeds. This updated version is extended to multiple cameras, including fisheye lenses and catadiopic cameras. CNN-SVO [29] is a version of SVO with depth predictions from a single-image depth prediction network. • DSO: (monocular camera) [30] is a new work by the authors of LSD-SLAM. This work creates a visual odemtry based on both the direct method and the sparse method without the need to detect and describe feature points. • EVO: It (Event Camera) [31] is an event-based visual ranging algorithm. Our algorithm is not affected by motion blur and performs well under challenging high dynamic range conditions as well as under intense lighting changes. Other SemiDense SLAMs based on event cameras can be seen in [32]. Other VO (Visual Ranging) systems based on event cameras can be seen in [33]. 

 • Dense visual SLAM • DTAM: It (monocular) can rebuild 3D models in real time based on minimizing the energy function of global spatial regularization in a novel non-convex optimization framework, which is called the direct method [34]. • MLM SLAM: It (monocular) can rebuild dense 3D models online without the need for a graphics processing unit (GPU). The key contribution lies in the multi-resolution depth estimation and spatial smoothing process. • Kinect Fusion: (RGB-D) is the first 3D reconstruction system with a depth camera [35]. • DVO: It (RGB-D) proposes a dense visual SLAM approach, an entropy-based similarity metric for keyframe selection and closed-loop detection based on the g2o framework [36]. • RGBD-SLAM-V2: An accurate 3D dense model can be reconstructed using the (RGB-D) depth camera [37]. • Kintinuous: It (RGB-D) is a visual SLAM system with real-time globally consistent point and mesh reconstruction [38]. • RTAB-MAP: It (RGB-D) supports simultaneous localization and mapping, but is difficult to use as a basis for developing advanced algorithms [39]. The latter supports both visual and lidar SLAM [40]. • Dynamic Fusion: It (RGB-D) presents the first dense SLAM system capable of reconstructing non-rigid deformed scenes in real time based on Kinect Fusion [41]. VolumeDeform [42] also implements real-time non-rigid reconstruction, but is not open source. Similar work can be seen in Fusion4D [43]. • Elastic Fusion: It (RGB-D) is a real-time dense visual SLAM system capable of capturing comprehensive, dense, globally consistent room-scale-based maps of environments explored using RGB-D cameras, [44]. • InfiniTAM: It (RGB-D) is a real-time 3D reconstruction system with CPU on Linux, IOS, Android platforms [45]. • Bundle Fusion: It (RGB-D) supports powerful tracking capabilities to recover from severe tracking failures and re-estimate 3D models in real time to ensure global consistency [46]. • KO-Fusion: It (RGB-D) [47] proposes a dense RGB-D SLAM system with kinematics and mileage measurements from wheeled robots. • SOFT-SLAM: It (stereo) [48] can create dense maps and has a large closed-loop effect for pose estimation based on SOFT [49]. Other works can be listed below, but are not limited to SLAMRecon, RKD-SLAM [50] and RGB-D SLAM [51]. 

 References 

 [1] Raul Mur-Artal, Jose Maria Martinez Montiel, and Juan D Tardos. Orb-slam: a versatile and accurate monocular slam system. IEEE transactions on robotics, 31(5):1147–1163, 2015. [2] Tong Qin, Peiliang Li, and Shaojie Shen. Vins-mono: A robust and versatile monocular visual-inertial state estimator. IEEE Transactions on Robotics, 34(4):1004–1020, 2018. 

 [3] Xiang Gao, Tao Zhang, Yi Liu, and Qinrui Yan. 14 Lectures on Visual SLAM: From Theory to Practice. Publishing House of Electronics Industry, 2017. 

 [4] Takafumi Taketomi, Hideaki Uchiyama, and Sei Ikeda. Visual slam algorithms: A survey from 2010 to 2016. IPSJ Transactions on Computer Vision and Applications, 9(1):16, 2017. 

 [5] B Srinivasa Reddy and Biswanath N Chatterji. An fft-based technique for translation, rotation, and scale-invariant image registration. IEEE transactions on image processing, 5(8):1266–1271, 1996. 

 [6] Tim Kazik and Ali Haydar G ¨okto ˘gan. Visual odometry based on the fourier-mellin transform for a rover using a monocular ground-facing camera. In 2011 IEEE International Conference on Mechatronics, pages 469–474. IEEE, 2011. 

 [7] Merwan Birem, Richard Kleihorst, and Norddin El-Ghouti. Visual odometry based on the fourier transform using a monocular groundfacing camera. Journal of Real-Time Image Processing, 14(3):637–646, 2018. 

 [8] Liu Haomin, Zhang Guofeng, and Bao hujun. A survy of monocular simultaneous localization and mapping. Journal of Computer-Aided Design & Computer Graphics, 28(6):855–868, 2016. 

 [9] Guillermo Gallego, Tobi Delbruck, Garrick Orchard, Chiara Bartolozzi, and Davide Scaramuzza. Event-based vision: A survey. 2019. 

 [10] Patrick Lichtsteiner, Christoph Posch, and Tobi Delbruck. A 128x128 120db 15us latency asynchronous temporal contrast vision sensor. IEEE journal of solid-state circuits, 43(2):566–576, 2008. 

 [11] Christoph Posch, Michael Hofstatter, Daniel Matolin, Guy Vanstraelen, Peter Schon, Nikolaus Donath, and Martin Litzenberger. A dual-line optical transient sensor with on-chip precision time-stamp generation. In 2007 IEEE International Solid-State Circuits Conference. Digest of Technical Papers, pages 500–618. IEEE, 2007. 

 [12] Christian Brandli, Raphael Berner, Minhao Yang, Shih-Chii Liu, and Tobi Delbruck. A 240× 180 130 db 3 µs latency global shutter spatiotemporal vision sensor. IEEE Journal of Solid-State Circuits, 49(10):2333–2341, 2014. 

 [13] Christoph Posch, Daniel Matolin, and Rainer Wohlgenannt. A qvga 143 db dynamic range frame-free pwm image sensor with lossless pixel-level video compression and time-domain cds. IEEE Journal of Solid-State Circuits, 46(1):259–275, 2010. 

 [14] Andrew J Davison, Ian D Reid, Nicholas D Molton, and Olivier Stasse. Monoslam: Real-time single camera slam. IEEE Transactions on Pattern Analysis & Machine Intelligence, (6):1052–1067, 2007. 

 [15] Georg Klein and David Murray. Parallel tracking and mapping for small ar workspaces. In Proceedings of the 2007 6th IEEE and ACM International Symposium on Mixed and Augmented Reality, pages 1– 10. IEEE Computer Society, 2007. 

 [16] Georg Klein and David Murray. Improving the agility of keyframebased slam. In European Conference on Computer Vision, pages 802– 815. Springer, 2008. 

 [17] Ethan Rublee, Vincent Rabaud, Kurt Konolige, and Gary R Bradski. Orb: An efficient alternative to sift or surf. In ICCV, volume 11, page 2. Citeseer, 2011. 

 [18] Raul Mur-Artal and Juan D Tard ´os. Orb-slam2: An open-source slam system for monocular, stereo, and rgb-d cameras. IEEE Transactions on Robotics, 33(5):1255–1262, 2017. 

 [19] Yahui Wang, Shaojun Cai, Shi-Jie Li, Yun Liu, Yangyan Guo, Tao Li, and Ming-Ming Cheng. Cubemapslam: A piecewise-pinhole monocular fisheye slam system. In Asian Conference on Computer Vision, pages 34–49. Springer, 2018. 

 [20] Ra´ul Mur-Artal and Juan D Tard ´os. Visual-inertial monocular slam with map reuse. IEEE Robotics and Automation Letters, 2(2):796– 803, 2017. 

 [21] D. Schlegel, M. Colosi, and G. Grisetti. ProSLAM: Graph SLAM from a Programmer’s Perspective. In 2018 IEEE International Conference on Robotics and Automation (ICRA), pages 1–9, 2018. 

 [22] Guofeng Zhang, Haomin Liu, Zilong Dong, Jiaya Jia, Tien-Tsin Wong, and Hujun Bao. Efficient non-consecutive feature tracking for robust structure-from-motion. IEEE Transactions on Image Processing, 25(12):5957–5970, 2016. 

 [23] Shinya Sumikura, Mikiya Shibuya, and Ken Sakurada. Openvslam: a versatile visual slam framework, 2019. 

 [24] Bernd Pfrommer and Kostas Daniilidis. Tagslam: Robust slam with fiducial markers. arXiv preprint arXiv:1910.00679, 2019. 

 [25] Rafael Munoz-Salinas and Rafael Medina-Carnicer. Ucoslam: Simultaneous localization and mapping by fusion of keypoints and squared planar markers. arXiv preprint arXiv:1902.03729, 2019. 

 [26] Jakob Engel, Thomas Sch ¨ops, and Daniel Cremers. Lsd-slam: Largescale direct monocular slam. In European conference on computer vision, pages 834–849. Springer, 2014. 

 [27] Jakob Engel, J ¨org St ¨uckler, and Daniel Cremers. Large-scale direct slam with stereo cameras. In 2015 IEEE/RSJ International Conference on Intelligent Robots and Systems (IROS), pages 1935–1942. IEEE, 2015. 

 [28] Christian Forster, Zichao Zhang, Michael Gassner, Manuel Werlberger, and Davide Scaramuzza. Svo: Semidirect visual odometry for monocular and multicamera systems. IEEE Transactions on Robotics, 33(2):249–265, 2016. 

 [29] Shing Yan Loo, Ali Jahani Amiri, Syamsiah Mashohor, Sai Hong Tang, and Hong Zhang. Cnn-svo: Improving the mapping in semi-direct visual odometry using single-image depth prediction. arXiv preprint arXiv:1810.01011, 2018. 

 [30] Jakob Engel, Vladlen Koltun, and Daniel Cremers. Direct sparse odometry. CoRR, abs/1607.02565, 2016. [91] Jakob Engel, Vladlen Koltun, and Daniel Cremers. Direct sparse odometry. IEEE transactions on pattern analysis and machine intelligence, 40(3):611–625, 2017. 

 [31] Henri Rebecq, Timo Horstsch¨afer, Guillermo Gallego, and Davide Scaramuzza. Evo: A geometric approach to event-based 6-dof parallel tracking and mapping in real time. IEEE Robotics and Automation Letters, 2(2):593–600, 2016. 

 [32] Yi Zhou, Guillermo Gallego, Henri Rebecq, Laurent Kneip, Hongdong Li, and Davide Scaramuzza. Semi-dense 3d reconstruction with a stereo event camera. In Proceedings of the European Conference on Computer Vision (ECCV), pages 235–251, 2018. 

 [33] David Weikersdorfer, Raoul Hoffmann, and J ¨org Conradt. Simultaneous localization and mapping for event-based vision systems. In International Conference on Computer Vision Systems, pages 133–142. Springer, 2013. 

 [34] Javier Civera, Andrew J Davison, and JM Martinez Montiel. Inverse depth parametrization for monocular slam. IEEE transactions on robotics, 24(5):932–945, 2008. 

 [35] Richard A Newcombe, Shahram Izadi, Otmar Hilliges, David Molyneaux, David Kim, Andrew J Davison, Pushmeet Kohli, Jamie Shotton, Steve Hodges, and Andrew W Fitzgibbon. Kinectfusion: Realtime dense surface mapping and tracking. In ISMAR, volume 11, pages 127–136, 2011. 

 [36] Frank Steinbr ¨ucker, J ¨urgen Sturm, and Daniel Cremers. Real-time visual odometry from dense rgb-d images. In 2011 IEEE International Conference on Computer Vision Workshops (ICCV Workshops), pages 719–722. IEEE, 2011. 

 [37] Christian Kerl, J ¨urgen Sturm, and Daniel Cremers. Robust odometry estimation for rgb-d cameras. In 2013 IEEE International Conference on Robotics and Automation, pages 3748–3754. IEEE, 2013. [38] Thomas Whelan, Michael Kaess, Maurice Fallon, Hordur Johannsson, John J Leonard, and John McDonald. Kintinuous: Spatially extended kinectfusion. 2012. 

 [39] Mathieu Labbe and Franc¸ois Michaud. Online global loop closure detection for large-scale multi-session graph-based slam. In 2014 12 IEEE/RSJ International Conference on Intelligent Robots and Systems, pages 2661–2666. IEEE, 2014. 

 [109] MM Labb´e and F Michaud. Appearance-based loop closure detection in real-time for large-scale and long-term operation. IEEE Transactions on Robotics, pages 734–745. 

 [40] Mathieu Labb´e and Franc¸ois Michaud. Rtab-map as an open-source lidar and visual simultaneous localization and mapping library for large-scale and long-term online operation. Journal of Field Robotics, 36(2):416–446, 2019. 

 [41] Richard A Newcombe, Dieter Fox, and Steven M Seitz. Dynamicfusion: Reconstruction and tracking of non-rigid scenes in real-time. In Proceedings of the IEEE conference on computer vision and pattern recognition, pages 343–352, 2015. 

 [42] Matthias Innmann, Michael Zollh ¨ofer, Matthias Nießner, Christian Theobalt, and Marc Stamminger. Volumedeform: Real-time volumetric non-rigid reconstruction. In European Conference on Computer Vision, pages 362–379. Springer, 2016. 

 [43] Mingsong Dou, Sameh Khamis, Yury Degtyarev, Philip Davidson, Sean Ryan Fanello, Adarsh Kowdle, Sergio Orts Escolano, Christoph Rhemann, David Kim, Jonathan Taylor, et al. Fusion4d: Real-time performance capture of challenging scenes. ACM Transactions on Graphics (TOG), 35(4):114, 2016. 

 [44] Thomas Whelan, Stefan Leutenegger, R Salas-Moreno, Ben Glocker, and Andrew Davison. Elasticfusion: Dense slam without a pose graph. Robotics: Science and Systems, 2015. 

 [45] V A Prisacariu, O K¨ahler, S Golodetz, M Sapienza, T Cavallari, P H S Torr, and D W Murray. InfiniTAM v3: A Framework for Large-Scale 3D Reconstruction with Loop Closure. arXiv pre-print arXiv:1708.00783v1, 2017. 

 [46] Angela Dai, Matthias Nießner, Michael Zoll ¨ofer, Shahram Izadi, and Christian Theobalt. Bundlefusion: Real-time globally consistent 3d reconstruction using on-the-fly surface re-integration. ACM Transactions on Graphics 2017 (TOG), 2017. 

 [47] Charlie Houseago, Michael Bloesch, and Stefan Leutenegger. Kofusion: Dense visual slam with tightly-coupled kinematic and odometric tracking. In 2019 International Conference on Robotics and Automation (ICRA), pages 4054–4060. IEEE, 2019. 

 [48] Igor Cviˇsic, Josip Cesic, Ivan Markovic, and Ivan Petrovic. Softslam: Computationally efficient stereo visual slam for autonomous uavs. Journal of field robotics, 2017. 

 [49] Igor Cviˇsi´c and Ivan Petrovi´c. Stereo odometry based on careful feature selection and tracking. In 2015 European Conference on Mobile Robots (ECMR), pages 1–6. IEEE, 2015. 

 [50] Haomin Liu, Chen Li, Guojun Chen, Guofeng Zhang, Michael Kaess, and Hujun Bao. Robust keyframe-based dense slam with an rgb-d camera. arXiv preprint arXiv:1711.05166, 2017. 

 [51] Weichen Dai, Yu Zhang, Ping Li, and Zheng Fang. Rgb-d slam in dynamic environments using points correlations. arXiv preprint arXiv:1811.03217, 2018. 

 resource 

 CVPR2020 Paper CenterMask Interpretation 

 3D object detection: MV3D-Net 

 3D-MiniNet: Learning 2D Representations from Point Clouds for Fast and Efficient 3D LIDAR Semantic Segmentation (2020) 

 Use QT to add VTK plug-in under win to realize point cloud visualization GUI 

 JSNet: Joint Instances and Semantic Segmentation for 3D Point Clouds 

 A Survey of Semantic Segmentation of 3D Point Cloud in Large Scene 

 The outofcore module in PCL - Display of large-scale point clouds based on out-of-core octree 

 Target Segmentation Based on Local Convex 

 Point cloud labeling based on 3D convolutional neural networks 

 SuperVoxel of Point Cloud 

 Large-scale point cloud segmentation based on hyperdot graph 

 SLAM Method Based on Fisheye Camera 

 ![avatar]( 20200508212543645.png) 

 A summary of historical articles on point cloud learning  



--------------------------------------------------------------------------------

SLAM involves two main tasks: localization and mapping. In mobile robots or autonomous driving, this is a very important issue: if the robot wants to move accurately, it must have a map of the environment, and then to build a map of the environment, it needs to know the location of the robot. 

 This series of articles is mainly divided into four parts: 

 In the first part, we will introduce Lidar SLAM, including Lidar sensors, open-source Lidar SLAM systems, deep learning in Lidar, and challenges and the future. 

 The second part focuses on Visual SLAM, including camera sensors and open-source visual SLAM systems for different dense SLAMs. 

 The third part introduces visual inertial mileage SLAM, deep learning in visual SLAM, and the future. 

 In the fourth part, we will introduce the integration of lidar and vision. 

 The stability of visual SLAM is a technical challenge. Because of the problems of initialization, scale uncertainty and scale drift based on single-purpose visual SLAM [1]. Although stereo cameras and RGB-D cameras can solve the problems of initialization and scaling, there are also some problems that cannot be ignored, such as fast motion speed, small viewing angle, large computation, occlusion, feature loss, dynamic scene and lighting transformation. The fusion scheme of sensors for the above problems has gradually become popular, and the visual odometry of IMU and camera fusion has become a research hotspot. 

 Vision and inertial navigation 

 ![avatar]( 20200524215820141.JPG) 

 The paper [2] [3] [4] is a comparison of some earlier studies on VIO. [5] [6] gives a mathematical proof of the visual inertial odometer. The paper [7] uses the bundle constraint algorithm to robustly initialize VIO. In particular, tango [8], Dyson 360 Eye and hololens [9] can be regarded as real products of VIO and have received good feedback. In addition, Apple's ARkit (filterbase), Google's ARcore (filterbase), and uSens' Insideout are all VIO technologies. Here are some open-source VIO systems [10]:  

 • SSF: (Loosely Coupled, Filter-Based Approach) is a single-sensor and multi-sensor fusion framework for delay compensation based on EKF [11]. 

 ![avatar]( 20200524215849917.JPG) 

 • MSCKF: (tightly coupled, filter-based approach) was adopted by Google Tango and is based on the extended Kalman filter [12]. Similar work has MSCKF-VIO [13] and the code is open-sourced.  

 • ROVIO: (tightly coupled, filter-based approach) is an extended Kalman filter-based VIO method that tracks 3D features and image block features [14]. 

 • OKVIS: (Tightly Coupled, Optimization-Based Approach) is a classic keyframe-based visual inertial SLAM [15] open source solution. Supports sliding window estimators for monocular and stereo cameras. 

 • VINS: VINS Mono (tightly coupled, optimization-based approach), paper [16] is a real-time SLAM framework for monocular vision inertial navigation. Open source code runs on Linux and integrates ROS. 

 VINS Mobile [17] [18] is a real-time monocular vision inertial odometer that runs on compatible iOS devices. In addition, VINS Fusion supports multiple visual inertial sensor types (GPS, single camera + IMU, stereo camera + IMU, and even stereo camera only). It has modules for position calibration, time alignment, and closed-loop detection. 

 ![avatar]( 20200524215921971.JPG) 

  ICE-BA: (tightly coupled, optimization-based method) provides an incremental, consistent, and effective bundle adjustment algorithm for visual inertial SLAM, performs local BA on the basis of sliding window algorithm, parallels global BA on all key frames, and outputs the camera pose and updated map points for each frame in real time [19]. 

 Maplab:: (tightly coupled, optimization-based approach) is an open, research-oriented visual inertial SLAM framework written in C++ that supports the creation and processing of multiple SLAM schemes. On the one hand, maplab can be seen as an off-the-shelf visual inertial mapping and localization system. On the other hand, maplab provides the research community with a range of multi-window SLAM tools, including map merging, visual inertial batch optimization, loop closure, and 3D intensive reconstruction [20]. 

 ![avatar]( 20200524220056858.JPG) 

 Of course, there are other solutions, such as ORB-SLAM-based VI-ORB [21], an optimized tight-coupling scheme based on StructVIO [22], which is better able to cope with the rapid movement and rotation of cameras in AR applications. Other systems such as event camera-based VIO will not be listed here.  

 Deep learning and visual SLAM 

 ![avatar]( 20200524220145305.JPG) 

 At present, deep learning plays a crucial role in computer vision. With the development of visual SLAM, more and more researchers have begun to pay attention to the research of SLAM based on deep learning. A typical example is semantic SLAM. "Semantic SLAM" refers to the inclusion of semantic information into SLAM systems to improve the performance and representation of SLAM processes by providing high-level understanding, robust performance, environmental awareness, and task-driven awareness. Next, we will introduce the solution of SLAM with semantic information from the following aspects:  

 Features and Detection: 

 Monocular vision-based Pop-up SLAM [23] proposes a real-time monocular planar SLAM to demonstrate that in low-texture environments, semantic understanding can improve the accuracy of state estimation and dense reconstruction. 

 The semantic keypoints predicted by convolutional networks are obtained. 

 LIFT [25] can obtain more dense feature points than SIFT. 

 DeepSLAM [26] performs feature point detection in the presence of image noise, which has a significant performance gap compared to traditional schemes. 

 SuperPoint [27] proposes a self-supervised framework for training POI detectors and descriptors for large multiview geometric problems in computer vision. 

 GCN-SLAM [28] proposes a deep learning-based GCNv2 network for generating keypoints and descriptors. 

 The paper [29] proposes an information SLAM scheme that fuses 3D shape, position, and semantic labels. 

 Cube SLAM (Monocular) is a 3D object detection and SLAM system based on cube model [30]. It realizes target-level scene construction, positioning and dynamic object tracking. Introduction to SLAM method based on fisheye camera 

 ![avatar]( 2020052422021853.JPG) 

 The paper [31] combines cubeSLAM and Pop-up SLAM to make the map more dense and accurate semantic information than feature point-based SLAM. The official account history article describes it.  

 Identification and segmentation: 

 SLAM ++ [32] demonstrates the main advantages of a new object oriented 3D SLAM scheme that takes advantage of the prior knowledge loop, i.e. many repetitive scenes, specific objects, and structural constructs. 

 The paper [33] proposes a combination of state-of-the-art deep learning methods and LSD-SLAM based on monocular camera video streams, which converts two-dimensional semantic information into three-dimensional point cloud map information through the correspondence between connected key frames with spatial consistency. 

 The Semanticfusion [34] method proposes a fusion scheme of CNNs and state-of-the-art dense SLAM, 

 ElasticFusion [35] is used to build semantic three-dimensional maps. 

 MarrNet proposes an end-to-end trainable framework for estimating 2.5D frames and 3D object shapes in turn. 

 3DMV (RGB D) [36] combines RGB color and geometric information to perform three-dimensional semantic segmentation of RGB-D information. 

 Pix3D [37] studies 3D shape modeling from a single image. 

 Scan complete [38] is a data-driven approach that takes an incomplete 3D scan of a scene as input and predicts a complete 3D model along with semantic labels for each voxel. 

 Fusion ++ [39] is an online object-level SLAM system that can build accurate 3D point cloud maps of arbitrarily reconstructed objects. 

 SegMap [40] is a segmentation-based SLAM system for robot localization, environment reconstruction, and semantic extraction. 

 ![avatar]( 20200524220407621.JPG) 

  Scale Recovery: 

 CNN-SLAM [41] is based on the work of monocular cameras estimating depth through deep learning, while DeepVO [42] and GS3D [43] and UnDeepVO [44] are using deep learning methods to obtain 6 degrees of freedom of pose and depth in monocular cameras. 

 GeoNet [45] is a joint unsupervised learning framework for estimating monocular depth, optical flow, and own motion from video. CodeSLAM [46] proposes a depth map based on a single image that can be efficiently optimized in conjunction with attitude variables. 

 Mono-stixels [47] uses depth, motion, and semantic information in dynamic scenes to estimate depth. 

 GANVO [48] uses an unsupervised learning framework to extract 6-DoF poses and monocular depth maps from unlabeled images, using depth convolution to generate adversarial networks. 

 GEN-SLAM [49] outputs dense point cloud maps with the help of traditional geometric SLAM and single-purpose topological constraints. 

 Dynamic SLAM 

 RDSLAM [50] is a real-time monocular SLAM system based on key frame online representation and update method. 

 DS-SLAM [51] is a semantic information SLAM system based on optimized ORB-SLAM. Semantic information can make SLAM systems more robust in dynamic environments. 

 MaskFusion is a real-time, object-aware, semantic and dynamic RGB-D SLAM system based on Mask R-CNN. The system can label objects with semantic information even in continuous, self-motion. 

 Detect SLAM [52] combines SLAM with object detection based on deep neural networks, enabling these two capabilities to complement each other in unknown and dynamic environments. 

 ![avatar]( 2020052422041884.JPG) 

 DynaSLAM [53] is a SLAM system that supports monocular, stereo, and RGB-D cameras to assist static maps in dynamic environments. StaticFusion [54] proposes a robust dense RGB-D SLAM method for detecting moving objects and simultaneously reconstructing background structures in dynamic environments.  

 The challenges and future of visual SLAM 

 Robustness and portability 

 Visual SLAM still faces great challenges in lighting changes, high dynamic environments, fast motion, vigorous rotation, and low texture environments. First, global shutter instead of rolling shutter is the basis for achieving accurate camera pose estimation. Event cameras like dynamic vision sensors are capable of generating 1 million events per second, which is enough for very fast motion at high speed and high dynamic range. Secondly, utilizing semantic features such as edges, planes, and surfaces, and even reducing feature dependencies, such as combining with tracking of adjacent sidelines, direct tracking, or machine learning, may become a better choice. Third, based on the mathematical principles of SfM/SLAM, precise mathematical formulas are superior to implicit deep learning. The future of SLAM is foreseeable, one is based on embedded platforms such as smartphones or drones (UAVs), and the other is more detailed 3D reconstruction of scenes or objects, scene understanding and deep learning. How to balance real-time and accuracy is a crucial open question. Solutions related to dynamic, unstructured, complex, uncertain and large-scale environments remain to be explored [55]. 

 multi-sensor fusion 

 Actual robots and hardware devices often carry more than one sensor, and are often a fusion of multiple sensors. For example, current research on mobile phone VIOs combines visual information and IMU information to achieve the complementary advantages of the two sensors, providing a very effective solution for the miniaturization and low cost of SLAM. DeLS-3D [56] design is a sensor fusion scheme that fuses camera video, motion sensors (GPS/IMU), and three-dimensional semantic maps to achieve robustness and efficiency of the system. The list of sensors is as follows, but is not limited to LIDAR, sonar, IMU, IR, camera, GPS, radar, etc. The choice of sensor depends on the environment and the type of map required. 

 Semantic SLAM 

 In fact, humans recognize the motion of objects based on perception rather than features in images. Deep learning in SLAM can achieve target recognition and segmentation, helping SLAM systems better perceive their surroundings. Semantic SLAM is also conducive to global optimization, closed-loop detection, and relocation. [57] This article points out that traditional SLAM methods rely on geometric features such as points, lines (PL-SLAM, StructSLAM), and planes to infer the structure of the environment. While semantic SLAM can achieve high-precision real-time localization in large-scale scenes, it teaches robots to perceive the environment like humans. 

 References 

 【1】Hauke Strasdat, J Montiel, and Andrew J Davison. Scale drift-aware large scale monocular slam. Robotics: Science and Systems VI, 2(3):7, 2010. 

 【2】 Stefan Leutenegger, Simon Lynen, Michael Bosse, Roland Siegwart, and Paul Furgale. Keyframe-based visual–inertial odometry using nonlinear optimization. The International Journal of Robotics Research, 34(3):314–334, 2015. 

 【3】 Guoquan Huang, Michael Kaess, and John J Leonard. Towards consistent visual-inertial navigation. In 2014 IEEE International Conference on Robotics and Automation (ICRA), pages 4926–4933. IEEE, 2014. 

 【4】 Mingyang Li and Anastasios I Mourikis. High-precision, consistent ekf-based visual-inertial odometry. The International Journal of Robotics Research, 32(6):690–711, 2013. 

 【5】Ra´ul Mur-Artal and Juan D Tard ´os. Visual-inertial monocular slam with map reuse. IEEE Robotics and Automation Letters, 2(2):796– 803, 2017. 

 【6】 Christian Forster, Luca Carlone, Frank Dellaert, and Davide Scaramuzza. On-manifold preintegration for real-time visual–inertial odometry. IEEE Transactions on Robotics, 33(1):1–21, 2016. 

 【7】Carlos Campos, J. M. M. Montiel, and Juan D. Tard ´os. Fast and robust initialization for visual-inertial slam. 2019 International Conference on Robotics and Automation (ICRA), pages 1288–1294, 2019. 

 【8】Mark Froehlich, Salman Azhar, and Matthew Vanture. An investigation of google tango R tablet for low cost 3d scanning. In ISARC. Proceedings of the International Symposium on Automation and Robotics in Construction, volume 34. Vilnius Gediminas Technical University, Department of Construction Economics , 2017. 

 【9】 Mathieu Garon, Pierre-Olivier Boulet, Jean-Philippe Doironz, Luc Beaulieu, and Jean-Franc¸ois Lalonde. Real-time high resolution 3d data on the hololens. In 2016 IEEE International Symposium on Mixed and Augmented Reality (ISMAR-Adjunct), pages 189–191. IEEE, 2016. 

 【10】Jeffrey Delmerico and Davide Scaramuzza. A benchmark comparison of monocular visual-inertial odometry algorithms for flying robots. In 2018 IEEE International Conference on Robotics and Automation (ICRA), pages 2502–2509. IEEE, 2018. 

 【11】Stephan M Weiss. Vision based navigation for micro helicopters. PhD thesis, ETH Zurich, 2012. 

 [12] Anastasios I Mourikis and Stergios I Roumeliotis. A multi-state constraint kalman filter for vision-aided inertial navigation. In Proceedings 2007 IEEE International Conference on Robotics and Automation, pages 3565–3572. IEEE, 2007. 

 [13] Ke Sun, Kartik Mohta, Bernd Pfrommer, Michael Watterson, Sikang Liu, Yash Mulgaonkar, Camillo J Taylor, and Vijay Kumar. Robust stereo visual inertial odometry for fast autonomous flight. IEEE Robotics and Automation Letters, 3(2):965–972, 2018. 

 [14] Michael Bloesch, Sammy Omari, Marco Hutter, and Roland Siegwart. Robust visual inertial odometry using a direct ekf-based approach. In 2015 IEEE/RSJ international conference on intelligent robots and systems (IROS), pages 298–304. IEEE, 2015. 

 [15] Peiliang Li, Tong Qin, Botao Hu, Fengyuan Zhu, and Shaojie Shen. Monocular visual-inertial state estimation for mobile augmented reality. In 2017 IEEE International Symposium on Mixed and Augmented Reality (ISMAR), pages 11–21. IEEE, 2017. 

 [16] Tong Qin and Shaojie Shen. Online temporal calibration for monocular visual-inertial systems. In 2018 IEEE/RSJ International Conference on Intelligent Robots and Systems (IROS), pages 3662–3669. IEEE, 2018. 

 [17] Tong Qin and Shaojie Shen. Robust initialization of monocular visualinertial estimation on aerial robots. In 2017 IEEE/RSJ International Conference on Intelligent Robots and Systems (IROS), pages 4225– 4232. IEEE, 2017. 

 [18] Zhenfei Yang and Shaojie Shen. Monocular visual–inertial state estimation with online initialization and camera–imu extrinsic calibration. IEEE Transactions on Automation Science and Engineering, 14(1):39– 51, 2016. 

 【19】Haomin Liu, Mingyu Chen, Guofeng Zhang, Hujun Bao, and Yingze Bao. Ice-ba: Incremental, consistent and efficient bundle adjustment for visual-inertial slam. In Proceedings of the IEEE Conference on Computer Vision and Pattern Recognition, pages 1974–1982, 2018. 

 【20】T. Schneider, M. T. Dymczyk, M. Fehr, K. Egger, S. Lynen, I. Gilitschenski, and R. Siegwart. maplab: An open framework for research in visual-inertial mapping and localization. IEEE Robotics and Automation Letters, 2018. 

 [21] Ra´ul Mur-Artal and Juan D Tard ´os. Visual-inertial monocular slam with map reuse. IEEE Robotics and Automation Letters, 2(2):796– 803, 2017. 

 [22]Danping Zou, Yuanxin Wu, Ling Pei, Haibin Ling, and Wenxian Yu. Structvio: Visual-inertial odometry with structural regularity of manmade environments. IEEE Transactions on Robotics, 2019. 

 【23】] Shichao Yang, Yu Song, Michael Kaess, and Sebastian Scherer. Popup slam: Semantic monocular plane slam for low-texture environments. In 2016 IEEE/RSJ International Conference on Intelligent Robots and Systems (IROS), pages 1222–1229. IEEE, 2016. 

 【24】 Georgios Pavlakos, Xiaowei Zhou, Aaron Chan, Konstantinos G Derpanis, and Kostas Daniilidis. 6-dof object pose from semantic keypoints. In 2017 IEEE International Conference on Robotics and Automation (ICRA), pages 2011–2018. IEEE, 2017. 

 [25] Kwang Moo Yi, Eduard Trulls, Vincent Lepetit, and Pascal Fua. Lift: Learned invariant feature transform. In European Conference on Computer Vision, pages 467–483. Springer, 2016. 

 【26】Daniel DeTone, Tomasz Malisiewicz, and Andrew Rabinovich. Toward geometric deep slam. arXiv preprint arXiv:1707.07410, 2017. 

 [27] Daniel DeTone, Tomasz Malisiewicz, and Andrew Rabinovich. Superpoint: Self-supervised interest point detection and description. In Proceedings of the IEEE Conference on Computer Vision and Pattern Recognition Workshops, pages 224–236, 2018. 

 【28】Jiexiong Tang, Ludvig Ericson, John Folkesson, and Patric Jensfelt. Gcnv2: Efficient correspondence prediction for real-time slam. arXiv preprint arXiv:1902.11046, 2019. 

 [29] Margarita Grinvald, Fadri Furrer, Tonci Novkovic, Jen Jen Chung, Cesar Cadena, Roland Siegwart, and Juan Nieto. Volumetric instanceaware semantic mapping and 3d object discovery. arXiv preprint arXiv:1903.00268, 2019. 

 【３０】Shichao Yang and Sebastian Scherer. Cubeslam: Monocular 3-d object slam. IEEE Transactions on Robotics, 2019. 

 [３１] Shichao Yang and Sebastian Scherer. Monocular object and plane slam in structured environments. IEEE Robotics and Automation Letters, 4(4):3145–3152, 2019. 

 【３２】Renato F. Salas-Moreno, Richard A. Newcombe, Hauke Strasdat, Paul H. J. Kelly, and Andrew J. Davison. Slam++: Simultaneous localisation and mapping at the level of objects. In Computer Vision & Pattern Recognition, 2013. 

 [３３] Xuanpeng Li and Rachid Belaroussi. Semi-dense 3d semantic mapping from monocular slam. 2016 

 【３４】John McCormac, Ankur Handa, Andrew Davison, and Stefan Leutenegger. Semanticfusion: Dense 3d semantic mapping with convolutional neural networks. In 2017 IEEE International Conference on Robotics and automation (ICRA), pages 4628–4635. IEEE, 2017. 

 【３５】Thomas Whelan, Renato F Salas-Moreno, Ben Glocker, Andrew J Davison, and Stefan Leutenegger. Elasticfusion: Real-time dense slam and light source estimation. The International Journal of Robotics Research, 35(14):1697–1716, 2016 

 【３６】Jiajun Wu, Yifan Wang, Tianfan Xue, Xingyuan Sun, Bill Freeman, and Josh Tenenbaum. Marrnet: 3d shape reconstruction via 2.5 d sketches. In Advances in neural information processing systems, pages 540–550, 2017. 

 【３７】Xingyuan Sun, Jiajun Wu, Xiuming Zhang, Zhoutong Zhang, Chengkai Zhang, Tianfan Xue, Joshua B Tenenbaum, and William T Freeman. Pix3d: Dataset and methods for single-image 3d shape modeling. In IEEE Conference on Computer Vision and Pattern Recognition (CVPR), 2018. 

 【３８】Angela Dai, Daniel Ritchie, Martin Bokeloh, Scott Reed, J ¨urgen Sturm, and Matthias Nießner. Scancomplete: Large-scale scene completion and semantic segmentation for 3d scans. In Proceedings of the IEEE Conference on Computer Vision and Pattern Recognition, pages 4578– 4587, 2018. 

 [３9] John McCormac, Ronald Clark, Michael Bloesch, Andrew J. Davison, and Stefan Leutenegger. Fusion++: Volumetric object-level slam. 2018 International Conference on 3D Vision (3DV), pages 32–41, 2018. 

 [４0] Renaud Dub´e, Andrei Cramariuc, Daniel Dugas, Juan Nieto, Roland Siegwart, and Cesar Cadena. Segmap: 3d segment mapping using datadriven descriptors. arXiv preprint arXiv:1804.09557, 2018. 

 【４１】Keisuke Tateno, Federico Tombari, Iro Laina, and Nassir Navab. Cnnslam: Real-time dense monocular slam with learned depth prediction. In Proceedings of the IEEE Conference on Computer Vision and Pattern Recognition, pages 6243–6252, 2017. 

 【４２】Vikram Mohanty, Shubh Agrawal, Shaswat Datta, Arna Ghosh, Vishnu Dutt Sharma, and Debashish Chakravarty. Deepvo: A deep learning approach for monocular visual odometry. arXiv preprint arXiv:1611.06069, 2016. 

 [４３] Buyu Li, Wanli Ouyang, Lu Sheng, Xingyu Zeng, and Xiaogang Wang. Gs3d: An efficient 3d object detection framework for autonomous driving. In Proceedings of the IEEE Conference on Computer Vision and Pattern Recognition, pages 1019–1028, 2019. 

 [４４] Ruihao Li, Sen Wang, Zhiqiang Long, and Dongbing Gu. Undeepvo: Monocular visual odometry through unsupervised deep learning. In 2018 IEEE International Conference on Robotics and Automation (ICRA), pages 7286–7291. IEEE, 2018. 

 【４５】 Zhichao Yin and Jianping Shi. Geonet: Unsupervised learning of dense depth, optical flow and camera pose. In CVPR, 2018. 

 [４６] Michael Bloesch, Jan Czarnowski, Ronald Clark, Stefan Leutenegger, and Andrew J Davison. Codeslamlearning a compact, optimisable representation for dense visual slam. In Proceedings of the IEEE Conference on Computer Vision and Pattern Recognition, pages 2560– 2568, 2018. 

 [４７] Fabian Brickwedde, Steffen Abraham, and Rudolf Mester. Monostixels: monocular depth reconstruction of dynamic street scenes. In 2018 IEEE International Conference on Robotics and Automation (ICRA), pages 1–7. IEEE, 2018. 

 [４８] Yasin Almalioglu, Muhamad Risqi U. Saputra, Pedro Porto Buarque de Gusm˜ao, Andrew Markham, and Agathoniki Trigoni. Ganvo: Unsupervised deep monocular visual odometry and depth estimation with generative adversarial networks. 2019 International Conference on Robotics and Automation (ICRA), pages 5474–5480, 2018. 

 [４９] Punarjay Chakravarty, Praveen Narayanan, and Tom Roussel. Genslam: Generative modeling for monocular simultaneous localization and mapping. arXiv preprint arXiv:1902.02086, 2019 

 【50】Wei Tan, Haomin Liu, Zilong Dong, Guofeng Zhang, and Hujun Bao. Robust monocular slam in dynamic environments. In 2013 IEEE International Symposium on Mixed and Augmented Reality (ISMAR), pages 209–218. IEEE, 2013. 

 [51] Chao Yu, Zuxin Liu, Xin-Jun Liu, Fugui Xie, Yi Yang, Qi Wei, and Qiao Fei. Ds-slam: A semantic visual slam towards dynamic environments. In 2018 IEEE/RSJ International Conference on Intelligent Robots and Systems (IROS), pages 1168–1174. IEEE, 2018. 

 【52】Fangwei Zhong, Wang Sheng, Ziqi Zhang, China Chen, and Yizhou Wang. Detect-slam: Making object detection and slam mutually beneficial. In IEEE Winter Conference on Applications of Computer Vision, 2018. 

 [53] Berta Bescos, Jos´e M F´acil, Javier Civera, and Jos´e Neira. Dynaslam: Tracking, mapping, and inpainting in dynamic scenes. IEEE Robotics and Automation Letters, 3(4):4076–4083, 2018. 

 [54] Raluca Scona, Mariano Jaimez, Yvan R Petillot, Maurice Fallon, and Daniel Cremers. Staticfusion: Background reconstruction for dense rgb-d slam in dynamic environments. In 2018 IEEE International Conference on Robotics and Automation (ICRA), pages 1–9. IEEE, 2018 

 【55】Muhammad Sualeh and Gon-Woo Kim. Simultaneous localization and mapping in the epoch of semantics: A survey. International Journal of Control, Automation and Systems, 17(3):729–742, 2019. 

 【56】Peng Wang, Ruigang Yang, Binbin Cao, Wei Xu, and Yuanqing Lin. Dels-3d: Deep localization and segmentation with a 3d semantic map. In Proceedings of the IEEE Conference on Computer Vision and Pattern Recognition, pages 5860–5869, 2018. 

 【５７】Nikolay Atanasov, Sean L Bowman, Kostas Daniilidis, and George J Pappas. A unifying view of geometry, semantics, and data association in slam. In IJCAI, pages 5204–5208, 2018. 



--------------------------------------------------------------------------------

share 

 SLAM involves two main tasks: localization and mapping. In mobile robots or autonomous driving, this is a very important issue: if the robot wants to move accurately, it must have a map of the environment, and then to build a map of the environment, it needs to know the location of the robot. 

 This series of articles is mainly divided into four parts: 

 In the first part, we will introduce Lidar SLAM, including Lidar sensors, open-source Lidar SLAM systems, deep learning in Lidar, and challenges and the future. 

 The second part focuses on Visual SLAM, including camera sensors and open-source visual SLAM systems for different dense SLAMs. 

 The third part introduces visual inertial mileage SLAM, deep learning in visual SLAM, and the future. 

 In the fourth part, we will introduce the integration of lidar and vision. 

 When it comes to lidar and visual SLAM systems, it is essential to calibrate between the two. 

 multi-sensor calibration 

 Camera & IMU: Kalibr [1] is a toolbox that addresses the calibration of the following types of sensors: 

 Multi-camera calibration. 

 Visual inertial calibration (Camera IMU). 

 Roller shutter camera calibration. 

 Vins integrates vision and IMU, with online spatial calibration and online temporal calibration capabilities. 

 The MSCKF-VIO has calibration capabilities for cameras and IMUs. 

 MC-VINS [2] can calibrate external parameters and time offsets between all multiple cameras and IMUs. 

 The IMU-TK [3] [4] can also calibrate the internal parameters of the IMU. 

 The paper [5] proposes an end-to-end network for monocular VIO that integrates data from cameras and IMUs. 

 ![avatar]( 20200524222221480.JPG) 

  Monocular and depth cameras 

 BAD SLAM [6] proposes a calibration benchmark using synchronous global shutter RGB and depth cameras. 

 • Cameras and cameras: mcptam [7] is a SLAM system that uses multiple cameras. It can also calibrate internal and external parameters. 

 MultiCol SLAM [8] is a multifisheye camera SLAM. In addition, the latest version of SVO can also support multiple cameras. 

 • Lidar & IMU: LIO-mapping [9] introduces a tightly coupled Lidar-IMU fusion method. Lidar-IMU alignment is a method for finding external calibration between Lidar and a six-degree-of-freedom attitude sensor in three-dimensional space. The external calibration of Lidar is described in [10] [11]. The doctoral dissertation [12] describes the work of Lidar calibration. 

 ![avatar]( 20200524222251463.JPG) 

  • Camera & Lidar: The paper [13] describes a probabilistic monitoring algorithm and a continuous calibration optimizer that allows camera and lidar calibration to be performed online and automatically. 

 Lidar-Camera [14] presents a new process and experimental setup for finding precise rigid body transformations to use 3D-3D points for external calibration of both the Lidar and the camera. 

 RegNet [15] is the first deep convolutional neural networks (CNNs) to use scanning lidar and monocular cameras to infer 6 degrees of freedom (DOF) external calibration between multimodal sensors. 

 ![avatar]( 20200524222315278.JPG) 

 LIMO [16] proposes a depth extraction algorithm based on LIDAR measurements for extracting camera feature trajectories and motion estimation. CalibNet [17] is a self-supervised deep network capable of automatically estimating six-degree-of-freedom rigid body transformations between 3D lidar and 2D cameras in real time. Autoware can also be used for calibration work of lidar and cameras.  

 Lidar and Vision Fusion 

 Hardware layer: For example, Pandora is a software and hardware solution that integrates 40-wire lidar, camera, and recognition algorithms. The integrated solution allows developers to get a comfortable experience from time synchronization. Focus on algorithm development. 

 Data layer: LiDAR has sparse and high-precision depth data, and the camera has dense but low-precision depth data. The fusion of the two can complete the depth of pixels in the image worthy of repair. The paper [18] only relies on basic image processing operations to complete the fusion of sparse lidar depth data and images. With the deepening of deep learning, [19] proposes to use a single deep regression network to learn directly from the RGB-D original data source and explore the impact of the number of deep samples. [20] Consider CNN running on sparse input and applying sparse laser scan data to complete depth estimation. 

 DFuseNet [21] proposes a CNN designed to upsample a series of sparse distance measurements based on contextual clues gathered from high-resolution intensity images. 

 LICFusion [22] fuses IMU measurements, sparse visual features, and extracted LiDAR point cloud data. 

 ![avatar]( 20200524222343845.JPG) 

  Task layer: Paper [23] is a perception scheme based on the fusion of stereo cameras and lidar. 

 [24]融合了毫米波雷达、激光雷达和相机，以检测和分类移动物体。 

 The paper [25] enhances VO through depth information provided by depth cameras or lidar depth information associated with cameras. 

 V-Loam [26] proposes a general framework for combining visual odometry and lidar odometry. It starts from two aspects: visual odometry and lidar odometry based on scan matching, and improves the performance of real-time motion estimation and point cloud registration algorithms. 

 VI-SLAM This system combines an accurate laser range estimator with a position recognition algorithm that uses vision to achieve loop detection. [27] For the tracking part of SLAM, a robust indoor SLAM system is constructed using an RGB-D camera and a two-dimensional low-cost lidar through mode switching and data fusion. 

 ![avatar]( 20200524222427126.JPG) 

 VIL-SLAM [28] combines tightly coupled stereo VIOs with lidar mapping and lidar-enhanced visual loop closure. [29] Monocular camera images are combined with laser distance measurement to allow visual impact without errors due to increased scale uncertainty. In deep learning, many methods can detect and identify fused data from cameras and lidar, such as point fusion [30], RoarNet [31], AVOD [32], FuseNet [33]. [34] Very precise localization is accomplished in an end-to-end learnable architecture using lidar and cameras.  

 The challenges and future of integrating SLAM 

 Data association: Future SLAMs must integrate multiple sensors. But different sensors have different data types, timestamps, and coordinate system expressions, which need to be handled uniformly. In addition, physical model building, state estimation, and optimization among multiple sensors should also be considered. 

 Hardware Integration: There is currently no suitable chip and integrated hardware to make SLAM technology easier to become a product. On the other hand, if the accuracy of the sensor decreases due to failure, non-nominal conditions or aging, the quality of the sensor measurement (e.g. noise, deviation) does not match the noise model. The stability and integration of the hardware should be followed. The front-end sensor should have data processing capabilities, from the hardware layer to the algorithm layer, to the functional layer to the SDK, and then to the application layer for innovation. 

 Crowdsourcing: Decentralized vision SLAM is a powerful tool for multi-robot applications in environments where absolute positioning systems are not available. Collaborative optimization of vision multi-robot SLAM requires decentralized data and optimization, known as crowdsourcing. Privacy concerns during decentralized data processing should be taken seriously. 

 High-precision maps: High-precision maps are crucial for robots. But what type of map is best for robots? Can dense or sparse maps be used for navigation, localization, and path planning? For long-term maps, a related open question is how often to update the information contained in the map, and how to determine when that information is outdated and can be discarded. 

 ![avatar]( 20200524222516519.JPG) 

  Adaptability, robustness, scalability: It is well known that there is no single SLAM system that can cover all scenarios these days. Most of these require a lot of parameter tuning in order to function properly in a given scenario. In order for a robot to perceive as human, an approach based on appearance rather than on features is preferred, which will help form closed loops integrated with semantic information between day and night sequences or between different seasons. 

 Anti-risk and constraint capabilities: A well-developed SLAM system should be fail-safe and fault-aware. This is not about relocation or circular closures. SLAM systems must have the ability to cope with risks or failures. At the same time, an ideal SLAM solution should be able to operate on different platforms regardless of the platform's computational constraints. How to strike a balance between accuracy, stability and limited resources is a challenging problem. 

 Application: SLAM technology has a wide range of applications, such as: large-scale positioning, navigation and 3D or semantic map construction, environment recognition and understanding, ground robots, drones, VR/AR/MR, AGV (automatic guided vehicle), autonomous driving, virtual interior decoration, virtual fitting room, immersive online games, etc., earthquake relief, video segmentation and editing. 

 ![avatar]( 20200524222523438.JPG) 

  References 

 【1】Joern Rehder, Janosch Nikolic, Thomas Schneider, Timo Hinzmann, and Roland Siegwart. Extending kalibr: Calibrating the extrinsics of multiple imus and of individual axes. In 2016 IEEE International Conference on Robotics and Automation (ICRA), pages 4304–4311. IEEE, 2016. 

 [2] Kevin Eckenhoff, Patrick Geneva, Jesse Bloecker, and Guoquan Huang. Multi-camera visual-inertial navigation with online intrinsic and extrinsic calibration. 2019 International Conference on Robotics and Automation (ICRA), pages 3158–3164, 2019. 

 [3] A. Tedaldi, A. Pretto, and E. Menegatti. A robust and easy to implement method for imu calibration without external equipments. In Proc. of: IEEE International Conference on Robotics and Automation (ICRA), pages 3042–3049, 2014. 

 [4] A. Pretto and G. Grisetti. Calibration and performance evaluation of low-cost imus. In Proc. of: 20th IMEKO TC4 International Symposium, pages 429–434, 2014. 

 【5】] Changhao Chen, Stefano Rosa, Yishu Miao, Chris Xiaoxuan Lu, Wei Wu, Andrew Markham, and Niki Trigoni. Selective sensor fusion for neural visual-inertial odometry. In Proceedings of the IEEE Conference on Computer Vision and Pattern Recognition, pages 10542–10551, 2019. 

 【6】Thomas Schops, Torsten Sattler, and Marc Pollefeys. Bad slam: Bundle adjusted direct rgb-d slam. In The IEEE Conference on Computer Vision and Pattern Recognition (CVPR), June 2019. 

 [7] Adam Harmat, Michael Trentini, and Inna Sharf. Multi-camera tracking and mapping for unmanned aerial vehicles in unstructured environments. Journal of Intelligent & Robotic Systems, 78(2):291– 317, 2015. 

 【8】Steffen Urban and Stefan Hinz. MultiCol-SLAM - a modular real-time multi-camera slam system. arXiv preprint arXiv:1610.07336, 2016 

 【9】Haoyang Ye, Yuying Chen, and Ming Liu. Tightly coupled 3d lidar inertial odometry and mapping. arXiv preprint arXiv:1904.06993, 2019. 

 [10] Deyu Yin, Jingbin Liu, Teng Wu, Keke Liu, Juha Hyypp¨a, and Ruizhi Chen. Extrinsic calibration of 2d laser rangefinders using an existing cuboid-shaped corridor as the reference. Sensors, 18(12):4371, 2018. 

 [1] Shoubin Chen, Jingbin Liu, Teng Wu, Wenchao Huang, Keke Liu, Deyu Yin, Xinlian Liang, Juha Hyypp¨a, and Ruizhi Chen. Extrinsic calibration of 2d laser rangefinders based on a mobile sphere. Remote Sensing, 10(8):1176, 2018. 

 [12] Jesse Sol Levinson. Automatic laser calibration, mapping, and localization for autonomous vehicles. Stanford University, 2011 

 【１３】Jesse Levinson and Sebastian Thrun. Automatic online calibration of cameras and lasers. In Robotics: Science and Systems, volume 2, 2013. 

 [１４] A. Dhall, K. Chelani, V. Radhakrishnan, and K. M. Krishna. LiDARCamera Calibration using 3D-3D Point correspondences. ArXiv eprints, May 2017. 

 [１５] Nick Schneider, Florian Piewak, Christoph Stiller, and Uwe Franke. Regnet: Multimodal sensor registration using deep neural networks. In 2017 IEEE intelligent vehicles symposium (IV), pages 1803–1810. IEEE, 2017. 

 [１６] Johannes Graeter, Alexander Wilczynski, and Martin Lauer. Limo: Lidar-monocular visual odometry. 2018. 

 [１７] Ganesh Iyer, J Krishna Murthy, K Madhava Krishna, et al. Calibnet: self-supervised extrinsic calibration using 3d spatial transformer networks. arXiv preprint arXiv:1803.08181, 2018. 

 【１８】Jason Ku, Ali Harakeh, and Steven L Waslander. In defense of classical image processing: Fast depth completion on the cpu. In 2018 15th Conference on Computer and Robot Vision (CRV), pages 16–22. IEEE, 2018 

 【１９】Fangchang Mal and Sertac Karaman. Sparse-to-dense: Depth prediction from sparse depth samples and a single image. In 2018 IEEE International Conference on Robotics and Automation (ICRA), pages 1–8. IEEE, 2018. 

 [２０] Jonas Uhrig, Nick Schneider, Lukas Schneider, Uwe Franke, Thomas Brox, and Andreas Geiger. Sparsity invariant cnns. In 2017 International Conference on 3D Vision (3DV), pages 11–20. IEEE, 2017. 

 [２１] Shreyas S Shivakumar, Ty Nguyen, Steven W Chen, and Camillo J Taylor. Dfusenet: Deep fusion of rgb and sparse depth information for image guided dense depth completion. arXiv preprint arXiv:1902.00761, 2019. 

 【２２】Xingxing Zuo, Patrick Geneva, Woosik Lee, Yong Liu, and Guoquan Huang. Lic-fusion: Lidar-inertial-camera odometry. arXiv preprint arXiv:1909.04102, 2019. 

 【２３】Olivier Aycard, Qadeer Baig, Siviu Bota, Fawzi Nashashibi, Sergiu Nedevschi, Cosmin Pantilie, Michel Parent, Paulo Resende, and TrungDung Vu. Intersection safety using lidar and stereo vision sensors. In 2011 IEEE Intelligent Vehicles Symposium (IV), pages 863–869. IEEE, 2011. 

 【２４】Ricardo Omar Chavez-Garcia and Olivier Aycard. Multiple sensor fusion and classification for moving object detection and tracking　IEEE Transactions on Intelligent Transportation Systems, 17(2):525– 534, 2015. 

 【２５】Ji Zhang, Michael Kaess, and Sanjiv Singh. Real-time depth enhanced monocular odometry. In 2014 IEEE/RSJ International Conference on Intelligent Robots and Systems, pages 4973–4980. IEEE, 2014. 

 【２６】Ji Zhang and Sanjiv Singh. Visual-lidar odometry and mapping: Lowdrift, robust, and fast. In 2015 IEEE International Conference on Robotics and Automation (ICRA), pages 2174–2181. IEEE, 2015. 

 【２７】Yoshua Nava. Visual-LiDAR SLAM with loop closure. PhD thesis, Masters thesis, KTH Royal Institute of Technology, 2018. 

 【２８】Weizhao Shao, Srinivasan Vijayarangan, Cong Li, and George Kantor. Stereo visual inertial lidar simultaneous localization and mapping. arXiv preprint arXiv:1902.10741, 2019. 

 [29] Franz Andert, Nikolaus Ammann, and Bolko Maass. Lidar-aided camera feature tracking and visual slam for spacecraft low-orbit navigation and planetary landing. In Advances in Aerospace Guidance, Navigation and Control, pages 605–623. Springer, 2015. 

 [３0] Danfei Xu, Dragomir Anguelov, and Ashesh Jain. Pointfusion: Deep sensor fusion for 3d bounding box estimation. In Proceedings of the IEEE Conference on Computer Vision and Pattern Recognition, pages 244–253, 2018 

 【３１】Kiwoo Shin, Youngwook Paul Kwon, and Masayoshi Tomizuka. Roarnet: A robust 3d object detection based on region approximation refinement. arXiv preprint arXiv:1811.03818, 2018. 

 [３2] Jason Ku, Melissa Mozifian, Jungwook Lee, Ali Harakeh, and Steven Waslander. Joint 3d proposal generation and object detection from view aggregation. IROS, 2018. 

 [３3] Caner Hazirbas, Lingni Ma, Csaba Domokos, and Daniel Cremers. Fusenet: Incorporating depth into semantic segmentation via fusionbased cnn architecture. In Asian conference on computer vision, pages 213–228. Springer, 2016 

 【３４】 Ming Liang, Bin Yang, Shenlong Wang, and Raquel Urtasun. Deep continuous fusion for multi-sensor 3d object detection. In Proceedings of the European Conference on Computer Vision (ECCV), pages 641– 656, 2018. 

 ![avatar]( 20200524222602327.JPG) 



--------------------------------------------------------------------------------

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



--------------------------------------------------------------------------------

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



--------------------------------------------------------------------------------

 We only introduce the code of the SSG pattern in semantic segmentation here 

#  First, the source code of each component 

##  1.1、 square_distance 

 Quickly calculate the distance between two point sets by means of a matrix. 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309573741497
  ```  
##  1.2、 index_points 

 Extract the coordinates and features of the point according to the ID number. 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309573741497
  ```  
##  1.3、 farthest_point_sample 

 Implementation of FPS sampling acceleration algorithm. 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309573741497
  ```  
##  1.4、 query_ball_point 

 Sphere radius search 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309573741497
  ```  
##  1.5、 sample_and_group 

 Implementation of PointNet ++ Sampling Layer and Packet Layer 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309573741497
  ```  
#  Setabstraction source code 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309573741497
  ```  
#  FeaturePropagation source code 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309573741497
  ```  
#  IV. SSG network structure source code 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309573741497
  ```  


--------------------------------------------------------------------------------

![avatar]( 20210113175452797.png) 

 Abstract: The SLAM system of stereo vision + inertial navigation + lidar proposed in this paper can achieve good performance in some complex scenarios such as tunnels. VIL-SLAM achieves this goal by combining a tightly coupled stereo vision inertial odometer (VIO) with lidar mapping and lidar-enhanced vision loop closure. The system generates a 6-degree-of-freedom lidar attitude with loop closure correction and a near-real-time 1cm voxel dense point cloud in real time. Compared with state-of-the-art lidar methods, VIL-SLAM shows higher precision and robustness. Main content, the system has four modules, as shown in Figure 2. The visual front end acquires stereo images from a stereo camera. It performs frame-to-frame tracking and stereo frame matching, and outputs stereo matching results as visual measurements. Stereo VIO uses stereo matching and IMU measurement, and performs IMU pre-integration and smooth tight coupling results on the pose map. The module outputs the VIO pose according to the IMU and the camera. The LiDAR mapping module uses the motion estimation of the VIO and performs LiDAR point denoising and scanning for map registration. The loop closure module performs visual loop detection and initial loop constraint estimation, and further fine registration through sparse point cloud ICP alignment. The global attitude map constraining all LiDAR poses is incrementally optimized, resulting in global correction trajectories and real-time LiDAR attitude correction. They are sent back to the LiDAR mapping module for map update and repositioning. In post-processing, the LiDAR scan frames are spliced with the best estimated LiDAR attitude to obtain dense point cloud map results, visual front-end, stereo matching for stereo vision. This paper uses Kanade Lucas Tomasi (KLT) feature tracker to track all feature points in previous stereo matching, both in the left and right images. The output is only produced when they are all tracked. Larger stereo baselines aid in scale estimation and reduce the problem of degradation caused by features at long distances. We use a feature-based approach that is better suited for processing long baselines than KLT. If the number of stereo matches tracked falls below the threshold, feature extraction is performed using the Shi-Tomashi corner detector, followed by a feature elimination process that removes features with pixel distances from any existing features that are less than the threshold. All surviving features are computed after the ORB describes the sub, and then brute-force stereo matching is performed to obtain a new matching result. The system initializes the system by stereo matching the first frame of stereo vision. 

 ![avatar]( 20210113175643931.png) 

 Visual Inertial Navigation Odometer, the goal of stereo VIO is to provide real-time accurate state estimates at relatively high frequencies as a motion model for LiDAR mapping algorithms. A tightly coupled fixed-lag smoother running on a pose graph is a good trade-off between accuracy and efficiency. Optimization-based methods often allow for multiple linearizations to approach the global minimum. The fixed-lag pose graph optimizer further limits the maximum number of variables, so the computational cost is bounded. Since poor visual measurements can lead to convergence problems, a strict outlier rejection mechanism is enforced for visual measurements. The system eliminates outliers by checking for mean reprojection errors. LIDAR Mapping, LIDAR Mapping uses the high-frequency IMU rate VIO pose as motion before performing LIDAR point extraction and scanning frame point clouds to map registration. Representing the scan c as a point cloud obtained from a complete LIDAR rotation. Extracting geometric features from c, including points on sharp edges and points on the plane. This is then solved as an optimization problem by minimizing the Euclidean distance residuals formed by feature points based on the current scanning to the map (all previous feature points). 

 ![avatar]( 20210113175724813.png) 

 Based on radar-enhanced loop detection, loop detection is essential for any SLAM system because of the drift introduced by long-term operation. The purpose of loop closure is to eliminate drift by optimizing the global pose map that combines loop constraints and relative transformation information for LiDAR mapping. To better assist lidar mapping, the corrected lidar attitude is sent back in real time so that the newly scanned feature points are registered to the revisited map. This paper proposes to add ICP alignment on the basis of the visual bag of words loop detection and PnP loop constraint formulas. The system uses the incremental solver iSAM2 to optimize the global attitude map to achieve real-time, experimental results, VIL-SLAM is evaluated, and it is compared with the best real-time lidar-based system LOAM2 on a custom dataset. The stereoscopic VIO sub-module (VIL-VIO) is also evaluated using the EuRoC MAV dataset. The results for five typical environments are provided here, including characterless corridors, disorganized elevated platforms, tunnels, and outdoor environments. Data collection for all these sequences begins and ends at the same point. The odometry (LiDAR mapping attitude) is evaluated based on the final drift error (FDE). The mapping results are evaluated using the mean registration error (MRE) with the Faro scan as the basic true value. The map is first aligned with the model (Faro scan) and then the Euclidean distance between the map point and the nearest point in the model is calculated. The odometer FDE and mapping results are shown in Table 1, preferably shown in bold. Map comparison: Map registration errors of VIL-SLAM (right) and LOAM (left) compared to the model. Errors above 0.3m (a-b) are shown in red, and errors above 0.5m (c) are shown in red. Discontinuous red areas inside the blue and green are missing models due to occlusion by scanning equipment. 

 Summary VIL-SLAM is an advanced odometry and mapping system designed to operate stably over long periods of time in different environments. The current framework loosely couples VIL-VIO and LiDAR mapping together. We are extending it into a tightly coupled framework so that the precise attitude estimates derived from LiDAR mapping can be used for IMU bias correction. ICP refinement of sparse feature points between scan frames in loop closure for better loop constraints. 



--------------------------------------------------------------------------------

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



--------------------------------------------------------------------------------

This blog records the model training process of RandLANet. First look at the code related to training in the main () function of main_Semantic3D.py 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309573773576
  ```  
 You can see that after obtaining the network, you directly call the train () method to start training. 

#  Training process 

 Train () method in RandLANet.py, 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309573773576
  ```  
#  verification process 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309573773576
  ```  


--------------------------------------------------------------------------------

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



--------------------------------------------------------------------------------

I have been using RandLANet for nearly a month, and I plan to document the entire process of RanLANet's semantic segmentation here. This series of blogs will use the Sematic3D dataset as an example to record the specific operation process of each step in combination with the source code. 

 Tf1.x RandLA-Net source code interpretation (1): Data preprocessing 

 Tf1.x RandLA-Net source code interpretation (2): Dataset 

 Tf1.x RandLA-Net Source Code Interpretation (3): Network Architecture 

 Tf1.x RandLA-Net source code interpretation (4): Model training 

 Tf1.x RandLA-Net Source Code Interpretation (5): Testing 



--------------------------------------------------------------------------------

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



--------------------------------------------------------------------------------

Network architecture of RandLA-Net 

#  initialization 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 202402030957374087
  ```  
#  inference 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 202402030957374087
  ```  
#  Training and validation 

 For the specific process, see tf1.x version of RandLA-Net source code interpretation (4): Network training 

#  Loss function 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 202402030957374087
  ```  
#  extended residual block 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 202402030957374087
  ```  
#  LFA module 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 202402030957374087
  ```  
#  relative position encoding 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 202402030957374087
  ```  
#  random sampling 

#  nearest neighbor interpolation 

#  aggregation neighborhood 

#  Pooling 



--------------------------------------------------------------------------------

Hello everyone. Last week we ushered in the first online sharing, the introduction of 3D model retrieval technology. This sharing is a relay sharing. There will be a keynote speaker sharing every week. I hope more small partners will join us to share and give themselves a chance to exercise. Here is a preview. The online live broadcast time is at 19:30 pm this Wednesday. Please pay more attention. 

 This week's online sharing session preview, the main topic: the application of deep learning in 3D scenes 

 Topic content, introduce the main tasks in 3D scenes and the challenges existing in the use of point cloud data. Introduce the current use of deep learning in point cloud data, targeting tasks such as object detection and scene segmentation. Combine Pointnet, Pointnet ++ and other deep learning frameworks for analysis and research. 

 Speaker: A graduate student in software engineering at ETU St. Petersburg, whose research direction is the application of deep learning in NLP and CV, Time: 19:30 2020-2-26 

 How to watch: Live Address: https://live.bilibili.com/21847497 

 How to participate in the discussion: Join the WeChat exchange group. During the live broadcast, you can send your own questions to the group, and discuss them after the live broadcast. How to join the group, comment at the end of the article, comment format "name + school/company", or directly send the keyword "online sharing and discussion WeChat group" in the official account to get the way to join the group. 

 Remarks: Since the speaker is abroad and uses the Bilibili live card, it is not smooth, so this time in the form of recording, the recording will have some impact on the questions and answers of the friends, so please be sure to add the WeChat group, ask questions in the WeChat group, and the part of the bullet comment will also be fed back to the speaker for some answers. 

 Next week's sharing session preview, the main topic: the use of CMake and the construction of projects, sharing content: how to use CMake to build C++ open source projects, introducing how to use Morden CMake to build C++ open source projects, including engineering structure, CMake syntax, open source project elements, etc. Speaker: Raymond, robot engineer, engaged in 3D vision, robot application software research and development, please look forward to it, welcome to share. 

 Advocating sharing, the original intention of the establishment of the point cloud PCL official account is to hope that everyone can take the initiative to share, actively communicate, and make progress together! So far, with point cloud and algorithm as the center, we have held several forums to share and exchange activities, and sometimes we can receive articles translated by students and share them on the official account platform for everyone to communicate and learn. However, the power of the group owner or some students alone is not enough to allow more willing people to join the team of sharing and learning from each other. I think everyone will have this feeling when they are in undergraduate or graduate school or at any time in the process of studying, that is, "no one communicates", there is no way to communicate and share the knowledge they have learned with their peers, or answer questions. This is a very painful thing. Therefore, I appeal to all researchers to actively sign up for this sharing relay. As long as you are willing to share, the content you share is your area of expertise, you can communicate, and you are welcome to contact the group owner. Give yourself a chance to communicate with more friends, and you will definitely gain more. The contact information of the group owner is as follows. 

 Later, let's have a relay sharing of point cloud technology enthusiasts! We look forward to having ideas and willing partners to join our online sharing group and share actively. The topics shared mainly include 3D vision, point cloud, high-precision maps, autonomous driving, and robotics-related fields. We look forward to researchers from various universities and technology experts from all walks of life to participate! Participation method: You can contact the group owner WeChat "920177957" (note required) or email: dianyunpcl@163.com, and enterprises are also welcome to contact the official account for cooperation. 

 A Survey of Semantic Segmentation of Three-Dimensional Point Clouds in Resources and Large Scenes 

 The outofcore module in PCL - Display of large-scale point clouds based on out-of-core octree 

 Target Segmentation Based on Local Convex 

 Point cloud labeling based on 3D convolutional neural networks 

 SuperVoxel of Point Cloud 

 Large-scale point cloud segmentation based on hyperdot graph 

 SLAM Method Based on Fisheye Camera 

 A summary of historical articles on point cloud learning 

 ![avatar]( 20200225111309756.jpg) 

 About us, the current WeChat exchange group continues to grow. Due to the large number of people, there are currently two groups. In order to encourage everyone to share, we hope that everyone can actively share while learning, and send your questions or small summaries to the main mailbox of the group owner dianyunpcl@163.com. If the above content is wrong or needs to be added, please leave a message! At the same time, everyone is welcome to pay attention to the WeChat official account, actively share submissions, or join the 3D visual WeChat group or QQ exchange group. It is not easy to be original. Please contact the group owner for reprinting and indicate the source  



--------------------------------------------------------------------------------

Write on the front 

 The recent official account activities have allowed more people to join the exchange group and try to ask more of my questions. The group owner is also actively recruiting more small partners to share with me, which can promote each other. 

 Here are two questions that are often asked and often asked by group friends, and my answers: 

 (1) When will there be a tutorial that can explain various functions in PCL? 

 (2) How can we solve the problem of large-scale point clouds? 

 Here's the formal answer and the plan. 

 Question 1: For the PCL tutorial, in fact, there are already a lot of online materials, but there is no very systematic information. For this problem, I am also thinking about how to do it. I will slowly launch a systematic learning tutorial in the later plan, implement a PCL tutorial with parallel theory and code, and am negotiating cooperation with depth camera manufacturers to sell depth cameras together with the tutorial. (The whole process is under planning due to time constraints). Then those who want to participate can chat privately with the group owner, participate in data sorting, ppt production, etc. 

 Question 2: The problem of large-scale point cloud, I have told countless people about this problem. Check the outofcore module in the PCL library. This module is to realize the loading and display of large-scale point clouds, rendering and other issues, but there are always many people asking, no one studies it, and no one is willing to share it. Too many people prefer to do something that can be reached. Here I have also consulted a lot of information. Baidu does not have a lot of information, but I can still explain some basic conceptual issues. Here is the only tutorial on the use of point clouds to achieve large-scale point cloud loading and display. Please indicate the source when reprinting. (Because there are too many blogs on the Internet that reprint being_young articles without permission) 

 Here, I mainly write the following content for the outofcore query extranet literature and module related information in the PCL library. It is explained again that the article is from "Point Cloud PCL" and sent out in the blogger park. Please do not reprint it without permission. 

 What is outofcore? 

 Outofcore can be understood as using the memory mapping method to deal with the problem that large-scale point clouds cannot be loaded into memory, and here I will temporarily translate it as "outer-core octree", because according to the implementation method in PCL, the memory mapping algorithm is implemented by the octree method. 

 In PCL, out-of-core-based data processing methods are used to complete large-scale point clouds with the help of octree theory, and use an octree domain search method to construct a topology of scattered data. In the field of visualization and computer graphics, outer-core-based algorithms involve methods for processing large amounts of data models running in limited memory, in short, by restricting access to a small, cached model's word block. 

 First of all, let's take a look at the module introduction of Outofcore of PCL. The module introduction is to realize large-scale point cloud storage through the method of memory mapping and the data structure of octree. The data is located in the directory-based octree hierarchy on some auxiliary storage media, and PCL - outofcore provides a framework for constructing and traversing outofcore octree. Other auxiliary functions will be explained in detail later. 

 The outofcore module in PCL is integrated by Urban Robotic, and the relevant routines are implemented in PCL. This article is summarized on the basis of consulting a large number of relevant materials, and there will inevitably be some misunderstandings. The module can be translated into Chinese as an outer-core octree, which is mainly aimed at point cloud processing. It can also be expanded into a grid or voxel representation. Outofcore supports spatial index data storage and fast data access, and only part of the data is loaded from the hard disk into the running memory for quick visualization. 

 So the framework can meet the following conditions: (1) big data, the framework can handle a large number of point clouds or large space data (2) support non-uniform data, the collected point clouds vary in distribution, density and accuracy, (3) support data query, can effectively search for data, find data and other operations (4) data update, can achieve data addition and deletion operations in a large number of data sets, such as filtering operations, (5) can preserve data quality, avoiding simplified resampling or lossy compression. 

  Out-of-core octree is actually a case where random access memory is not enough to load a large amount of data, a memory mapping method is used, and the data is stored on the hard disk in the form of an octree. 

 In order to meet the requirements of data query, an octree storage structure is adopted here. [Previous articles have introduced octree] Octree is a space-driven partitioning method. If the data distribution is seriously uneven, this method may have serious imbalances. In this case, the use of KDtree is proposed, which requires less memory for the tree structure and can quickly achieve data access. However, the implementation in general PCL mainly uses octree. It is only hoped that the module can support fast data updates, and octree is a very suitable algorithm for implementing off-core implementations, because each level of partitioning is the same, so no additional information needs to be read. 

 In general, there are few open-source solutions for this method to be used, among which PCL is a better algorithm for implementing the outer-core octree module. The open-source module only focuses on the outer-core octree implementation and visualization part, and the depth or resolution of the tree is completely defined by the user. 

 The above is PCL1.7 version above outofcore module to implement the outer core octree class, where the dependency on cJSON as a pcl_outofcore dependency has been linked together, and the function has been encapsulated into two independent classes OutofcoreOctreeNodeMetadata and OutofcoreOctreeMetadata 

 Overview of the file implementing outofcore in PCL 

 Four main hpp files for implementing out-of-core octree in outofcore module 

 １．octree.hpp 

 2. 　octree2.hpp 

 ３．octree ram container.hpp 

 4.    octree disk container.hpp 

 Header file: 

 (a) octree base.h 

 (b) octree base node.h 

 (c) octree abstract node container.h∗ 

 (D) metadata. H *: An abstract class that implements metadata 

 (E) outofcore node data.h *: Interface to implement data files at the outer node level (tree.oct idx) 

 (F) outofcore base data.h *: Implementation and outer octree high-level data interface (tree.octree JSON file) 

 (G) OutofcoreDepthFirstIterator: Depth-first iterator for out-of-core octree with direct access to classes of external nodes 

 (H) OutofcoreIteratorBase: Class for abstract iterators based on iterators in the octree module in pcl 

 (I) octree disk container.h: the IO of the disk container 

 (J) octree ram container.h: the core data structure of an out-of-core octree (no longer needed) 

 (K) outofcore node data.h: Contains the master node data structure and recursive methods for inserting and querying 

 (L) boost.h: contains all boost header files required in pcl outofcore 

 (M) cJSON.h: Minor modifications have been made for compatibility with the PCL build system 

 Template implementation class file: 

 (a)octree base.hpp 

 (b) octree base node.hpp 

 (c) octree disk container.hpp 

 (d) octree ram container.hpp 

 (e) OutofcoreDepthFirstIterator.hpp 

 (f) OutofcoreIteratorBase.hpp 

 source file 

 (a) cJSON.cpp 

 (b) outofcore node data.cpp 

 (c) outofcore base data.cpp 

 Format of Outofcore nodes 

 Each internal and leaf node on the disk can contain up to two files. 

 *. oct_idx JSON data file with oct_idx suffix in the format: 

 {

”version”:3 ,

”bb_min”:[xxx,yyy,zzz],

”bb_max”:[xxx,yyy,zzz],

”bin”:”pathtodata.pcd ”

} 

 This JSON data can be accessed directly using the OutofcoreOctreeNodeMetadata class. This class abstracts the interface to JSON data on disk, so in theory the format can be easily changed to XML, YAML, or other desired formats. 

 * .Pcd The pcd file contains the standard format (v7 +) PCD file for all point clouds associated with this node. This file is also available for all leaf nodes, but only for internal ("branch") nodes (if a LOD has been built). This file is accessible through OutofcoreOctreeDiskContainer classes. 

 The root node contains an attached file 

 *. octree contains advanced information about octree structures. The format is: 

 ![avatar]( aHR0cHM6Ly9jb21tb24uY25ibG9ncy5jb20vaW1hZ2VzL2NvcHljb2RlLmdpZg) 

 {

”name”:”test,

”version”:3,

”pointtype”:”urp”,        #(needs to be changed ∗)

”lod”:3,                  #depth of the tree

”numpts”:[X0,X1,X2, ... ,XD] , #total number of points at each LOD

”coordsystem”:”ECEF”           #the tree is not affected by this value

} 

 ![avatar]( aHR0cHM6Ly9jb21tb24uY25ibG9ncy5jb20vaW1hZ2VzL2NvcHljb2RlLmdpZg) 

 If you want to use the outofcore module in PCL, just add 

 #include <pcl/outofcore/outofcore.h> 

 #include <pcl/outofcore/outofcore_impl.h> 

 The specific implementation will be explained in more specific routines later. 

 The outofcore module in PCL realizes the characteristics of the algorithm. Point cloud insertion (1) addPointCloud (2) addPointCloud and genLOD The method of addPointCloud can be publicly accessed and the point cloud can be inserted into the external octree. NaN invalid points will be ignored, and all points will be inserted into the leaf node at full density. Multiple point clouds can be inserted into the external octree by iteratively calling the method of addPointClooud, and it is recommended to use the structure PointCloud2 to represent the point cloud 

 Point cloud query, point cloud query using: queryBoundingBox This function is a public interface for point cloud lookups provided by the octree built for outofcore. This method is overloaded and, depending on the parameters passed, will return all points within the query bounding box of the specified depth, or return a list of all PCD files whose union will contain all points within the query bounding box. 

 Depth level (LOD level of Depth): Multi-resolution outer-core octree, how to build LOD: buildLOD, addPointCloud and genLOD A key feature of the outer-core octree is the so-called "depth level" referred to as LOD, according to the habit of making the root level of the octree 0, each level is i-1 level octave sampling, (here I understand the pyramid structure) The depth level is constructed by randomly sampling the number of points at each level. This percentage can be set by the method setSamplePercent in the OutOfcoreCreeBase class. This parameter can also be set when creating a multi-resolution representation of the point cloud, which can achieve a fast rendering effect. During the rendering process, it can be based on certain query methods, such as voxels The distance to the viewpoint, the resolution required to access the point cloud, and of course it can also be accessed by the level and depth, bounding box 

 buildLOD: buildLOD rebuilds the LOD of the outofcore octree using a multi-resolution approach. Each branch node is the union of the subsamples of its leaves. The percentage of subsamples is determined by setSamplePercent, which defaults to 0.125 ^ depth-maxdepth LOD. See [5] for details on the algorithm.   

 Code implementation and comments 

 Code that implements generating an out-of-core octree filesystem from a large-scale point cloud: 

 ![avatar]( aHR0cHM6Ly9jb21tb24uY25ibG9ncy5jb20vaW1hZ2VzL2NvcHljb2RlLmdpZg) 

 #include <pcl/common/time.h>

#include <pcl/point_cloud.h>

#include <pcl/point_types.h>

#include < pcl/PCLPointCloud2.h >//It is recommended to use the point cloud header file in the form of using outofcore point cloud

#include <pcl/io/pcd_io.h>

#include <pcl/pcl_macros.h>

#include <pcl/console/print.h>

#include <pcl/console/parse.h>

//Add outofcore related header files

#include <pcl/outofcore/outofcore.h>

#include <pcl/outofcore/outofcore_impl.h>

typedef pcl::PointXYZ PointT;

using namespace pcl;

using namespace pcl::outofcore;

using pcl::console::parse_argument;

using pcl::console::parse_file_extension_argument;

using pcl::console::find_switch;

using pcl::console::print_error;

using pcl::console::print_warn;

using pcl::console::print_info;

#include <boost/foreach.hpp>

typedef OutofcoreOctreeBase<> octree_disk;

const int OCTREE_DEPTH (0);

const int OCTREE_RESOLUTION (1);

/*

Realize reading point cloud files

*/

PCLPointCloud2::Ptr  getCloudFromFile (boost::filesystem::path pcd_path)

{

  PCLPointCloud2::Ptr cloud(new PCLPointCloud2);

  if (io::loadPCDFile (pcd_path.string (), *cloud) == -1)

  {

    PCL_ERROR ("Couldn't read file\n");

  }

  print_info ("(%d)\n", (cloud->width * cloud->height));

  return cloud;

}

int outofcoreProcess (std::vector<boost::filesystem::path> pcd_paths, boost::filesystem::path root_dir, 

                  int depth, double resolution, int build_octree_with, bool gen_lod, bool overwrite, bool multiresolution)

{

  // Bounding box min/max pts

  PointT min_pt, max_pt;

  // Iterate over all pcd files resizing min/max

  for (size_t i = 0; i < pcd_paths.size (); i++)

  {

    // Get cloud

    PCLPointCloud2::Ptr cloud = getCloudFromFile (pcd_paths[i]);

    PointCloud<PointXYZ>::Ptr cloudXYZ (new PointCloud<PointXYZ>);

    fromPCLPointCloud2 (*cloud, *cloudXYZ);

    PointT tmp_min_pt, tmp_max_pt;

    if (i == 0)

    {

      getMinMax3D (* cloudXYZ, min_pt, max_pt);//Get the maximum and minimum value of the point cloud data on the XYZ axis

    }

    else

    {

      getMinMax3D (*cloudXYZ, tmp_min_pt, tmp_max_pt);

      // Resize new min

      if (tmp_min_pt.x < min_pt.x)

        min _ pt.x = tmp _ min _ pt.x;

      If (tmp_min_pt.y < min_pt.y)

        min_pt.y = tmp_min_pt.y;

      if (tmp _ min _ pt.z < min _ pt.z)

        min _ pt.z = tmp _ min _ pt.z;

      // Resize new max

      if (tmp_max_pt.x > max_pt.x)

        max_pt.x = tmp_max_pt.x;

      If (tmp_max_pt.y > max_pt.y)

        max_pt.y = tmp_max_pt.y;

      if (tmp _ max _ pt.z > max _ pt.z)

        max _ pt.z = tmp _ max _ pt.z;

    }

  }

  std::cout << "Bounds: " << min_pt << " - " << max_pt << std::endl;

  // The bounding box of the root node of the out-of-core octree must be specified

  const Eigen::Vector3d bounding_box_min (min_pt.x, min_pt.y, min_pt.z);

  const Eigen::Vector3d bounding_box_max (max_pt.x, max_pt.y, max_pt.z);

  //specify the directory and the root node's meta data file with a

  //".oct_idx" extension (currently it must be this extension)

  boost::filesystem::path octree_path_on_disk (root_dir / "tree.oct_idx");

  print_info ("Writing: %s\n", octree_path_on_disk.c_str ());

  //make sure there isn't an octree there already

  if (boost::filesystem::exists (octree_path_on_disk))

  {

    if (overwrite)

    {

      boost::filesystem::remove_all (root_dir);

    }

    else

    {

      PCL_ERROR ("There's already an octree in the default location. Check the tree directory\n");

      return (-1);

    }

  }

  octree_disk *outofcore_octree;

  //create the out-of-core data structure (typedef'd above)

  if (build_octree_with == OCTREE_DEPTH)

  {

    outofcore_octree = new octree_disk (depth, bounding_box_min, bounding_box_max, octree_path_on_disk, "ECEF");

  }

  else

  {

    outofcore_octree = new octree_disk (bounding_box_min, bounding_box_max, resolution, octree_path_on_disk, "ECEF");

  }

  uint64_t total_pts = 0;

  // Iterate over all pcd files adding points to the octree

  for (size_t i = 0; i < pcd_paths.size (); i++)

  {

    PCLPointCloud2::Ptr cloud = getCloudFromFile (pcd_paths[i]);

    boost::uint64_t pts = 0;

    if (gen_lod && !multiresolution)

    {

      print_info ("  Generating LODs\n");

      pts = outofcore_octree->addPointCloud_and_genLOD (cloud);

    }

    else

    {

      pts = outofcore_octree->addPointCloud (cloud, false);

    }

    print_info ("Successfully added %lu points\n", pts);

    print_info ("%lu Points were dropped (probably NaN)\n", cloud->width*cloud->height - pts);

//    assert ( pts == cloud->width * cloud->height );

    total_pts += pts;

  }

  print_info ("Added a total of %lu from %d clouds\n",total_pts, pcd_paths.size ());

  double x, y;

  outofcore_octree->getBinDimension (x, y);

  print_info ("  Depth: %i\n", outofcore_octree->getDepth ());

  print_info ("  Resolution: [%f, %f]\n", x, y);

  if(multiresolution)

  {

    print_info ("Generating LOD...\n");

    outofcore_octree->setSamplePercent (0.25);

    outofcore_octree->buildLOD ();

  }

  //free outofcore data structure; the destructor forces buffer flush to disk

  delete outofcore_octree;

  return 0;

}

void

printHelp (int, char **argv)

{

  print_info ("This program is used to process pcd fiels into an outofcore data structure viewable by the");

  print_info ("pcl_outofcore_viewer\n\n");

  print_info ("%s <options> <input>.pcd <output_tree_dir>\n", argv[0]);

  print_info ("\n");

  print_info ("Options:\n");

  print_info ("\t -depth <resolution>           \t Octree depth\n");

  print_info ("\t -resolution <resolution>      \t Octree resolution\n");

  print_info ("\t -gen_lod                      \t Generate octree LODs\n");

  print_info ("\t -overwrite                    \t Overwrite existing octree\n");

  print_info ("\t -multiresolution              \t Generate multiresolutoin LOD\n");

  print_info ("\t -h                            \t Display help\n");

  print_info ("\n");

}



main (int argc, char* argv[])

{

  // Check for help (-h) flag

  if (argc > 1)

  {

    if (find_switch (argc, argv, "-h"))

    {

      printHelp (argc, argv);

      return (-1);

    }

  }

  // If no arguments specified

  if (argc - 1 < 1)

  {

    printHelp (argc, argv);

    return (-1);

  }

  if (find_switch (argc, argv, "-debug"))

  {

    pcl::console::setVerbosityLevel ( pcl::console::L_DEBUG );

  }

  // Defaults

  int depth = 4;

  double resolution = .1;

  bool gen_lod = false;

  bool multiresolution = false;

  bool overwrite = false;

  int build_octree_with = OCTREE_DEPTH;

  // If both depth and resolution specified

  if (find_switch (argc, argv, "-depth") && find_switch (argc, argv, "-resolution"))

  {

    PCL_ERROR ("Both -depth and -resolution specified, please specify one (Mutually exclusive)\n");

  }

  // Just resolution specified (Update how we build the tree)

  else if (find_switch (argc, argv, "-resolution"))

  {

    build_octree_with = OCTREE_RESOLUTION;

  }

  // Parse options

  parse_argument (argc, argv, "-depth", depth);

  parse_argument (argc, argv, "-resolution", resolution);

  gen_lod = find_switch (argc, argv, "-gen_lod");

  overwrite = find_switch (argc, argv, "-overwrite");

  if (gen_lod && find_switch (argc, argv, "-multiresolution"))

  {

    multiresolution = true;

  }

  // Parse non-option arguments for pcd files

  std::vector<int> file_arg_indices = parse_file_extension_argument (argc, argv, ".pcd");

  std::vector<boost::filesystem::path> pcd_paths;

  for (size_t i = 0; i < file_arg_indices.size (); i++)

  {

    boost::filesystem::path pcd_path (argv[file_arg_indices[i]]);

    if (!boost::filesystem::exists (pcd_path))

    {

      PCL_WARN ("File %s doesn't exist", pcd_path.string ().c_str ());

      continue;

    }

    pcd_paths.push_back (pcd_path);

  }

  // Check if we should process any files

  if (pcd_paths.size () < 1)

  {

    PCL_ERROR ("No .pcd files specified\n");

    return -1;

  }

  // Get root directory

  boost::filesystem::path root_dir (argv[argc - 1]);

  // Check if a root directory was specified, use directory of pcd file

  if (root_dir.extension () == ".pcd")

    root_dir = root_dir.parent_path () / (root_dir.stem().string() + "_tree").c_str();

  return outofcoreProcess (pcd_paths, root_dir, depth, resolution, build_octree_with, gen_lod, overwrite, multiresolution);

} 

 ![avatar]( aHR0cHM6Ly9jb21tb24uY25ibG9ncy5jb20vaW1hZ2VzL2NvcHljb2RlLmdpZg) 

 The visual code is as follows (the compilation and implementation of these codes are recommended in PCL version 1.7 or above) 

 To create a multi-resolution outofcore octree with leaf node voxels up to 50 cm in size, use the following: pcl _outofcoreprocess − resolution 0.50 − genlod data01.pcd myotheroutofcoretree 

 Using the OutCore algorithm in PCL can use the executable file in the built-in tool, and the construction process can be parameterized by depth or resolution. If the resolution (i.e. maximum leaf size) is specified, the depth is automatically calculated. If the set tree is too deep: the construction of the LOD may take a long time 

 pcl_outofcore_viewer visualize results using different depths 

  Here, different resolution visualizations are used. For large-scale point clouds, the point clouds are displayed according to different perspectives. For the visualized parts, we load them in, and for the unneeded parts, we don't need to load them in. This is also why it can improve the efficiency of visualization. 

 The following is an experimental routine using real PCD point cloud data. The PCD file is a large-scale Street View point cloud with 200MB 

 ![avatar]( aHR0cHM6Ly9pbWcyMDE4LmNuYmxvZ3MuY29tL2Jsb2cvOTc2Mzk0LzIwMTkxMi85NzYzOTQtMjAxOTEyMDkxNTE4MjUzNzYtOTAzNTI2MjYyLnBuZw) 

 The result of this direct visualization of the point cloud, we can see the number of point clouds and the loading time 

 ![avatar]( aHR0cHM6Ly9pbWcyMDE4LmNuYmxvZ3MuY29tL2Jsb2cvOTc2Mzk0LzIwMTkxMi85NzYzOTQtMjAxOTEyMDkxNTE5MDcxNDYtMTkwNjAwMzA3Ni5wbmc) 

 We used to generate out-of-core octree files of different depths and resolutions, respectively 

 Use our outofcore_viewer visualized results 

 ![avatar]( aHR0cHM6Ly9pbWcyMDE4LmNuYmxvZ3MuY29tL2Jsb2cvOTc2Mzk0LzIwMTkxMi85NzYzOTQtMjAxOTEyMDkxNTE5NTU4MzUtMTkyNDI2ODAwNC5wbmc) 

 The algorithm uses the above method to generate an out-of-core octree for a larger point cloud, and can also achieve good visualization of point clouds 

 References [1] PCL Urban Robotics Code Sprint Blog. http://www.pointclouds.org/blog/urcs. [2] Point Cloud Library Documentation: Module outofcore. https://docs.pointclouds.org/trunk/ group__outofcore.html. [3] Urban Robotics. http://www.urbanrobotics.net. [4] Adam Stambler. osgpcl: OpenSceneGraph Point Cloud Library Cloud Viewer. https://github.com/ adasta/osgpcl, 2012. [5] Claus Scheiblauer and Michael Wimmer. Out-of-core selection and editing of huge point clouds. Computers & Graphics, 35(2):342–351, April 2011. 

 The articles here are all original by the blogger "Point Cloud PCL". Please do not reprint them without permission. Thank you for your understanding and cooperation. 

 Please follow the official account and join WeChat or ＱＱ communication group 

 ![avatar]( aHR0cHM6Ly9tbWJpei5xbG9nby5jbi9tbWJpel9wbmcvOXFkYmV3OGlhWkxqMXNFaWJRTHZRVmdic0Z1T3ZqRk9mT0kzSlR4ODRldXh2N2FaaWNPZ3B1aWFheWhqUWljMzNwNEh0QWY5amZGSUk1Um1pYWUyZmNmZFdNN1EvMD93eF9mbXQ9cG5n) 



--------------------------------------------------------------------------------

  PCL project compilation and generation using CMake with VS is currently the most convenient method. 

 The general steps are as follows: 

>  Write CMakeLists.txt and cpp files Use Cmake for project generation Use VS to open the project 

  After opening the sln file generated by CMake with VS, you can see three projects: 

 ![avatar]( 20210718212402864.png) 

  The pcl_visualizer_demo in the middle is my project file, and the other two are generated by CMake. Click Run and an error will be reported: 

 ![avatar]( 20210718203412502.png) 

  The solution to this problem is actually very simple. 

 Because the current default startup project is ALL_BUILD this project, not your own, so just set pcl_visualizer_demo this project as a startup project: 

 ![avatar]( 20210718212903605.png) 

    Click Run again and do not report an error.  



--------------------------------------------------------------------------------

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



--------------------------------------------------------------------------------

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



--------------------------------------------------------------------------------

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



--------------------------------------------------------------------------------

