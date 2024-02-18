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

