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

