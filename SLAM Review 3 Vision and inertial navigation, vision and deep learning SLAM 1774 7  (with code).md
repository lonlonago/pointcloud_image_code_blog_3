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

