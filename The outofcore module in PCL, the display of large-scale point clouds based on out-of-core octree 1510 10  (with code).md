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

