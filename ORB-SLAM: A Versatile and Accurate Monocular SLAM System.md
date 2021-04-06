@def review = true
@def tags = ["reviews","robotics","SLAM"]
@def reviewers = ["Keith Russell"]
@def hasmath = false
@def class = "journal"
@def authors = "Raul Mur-Artal; J. M. M. Montiel; Juan D. Tardos"
@def title = "ORB-SLAM: A Versatile and Accurate Monocular SLAM System"
@def venue = "IEEE"
@def year = "2015"

\toc

\toc

### Broad area/overview
This paper presents a new SLAM method: ORB-SLAM.  This method uses a single monocular camera and operates in real time in a wide range of environments.  SLAM has been a very popular topic in robotics research in recent years, with the rise of cheap and powerful computers as well as cheap and versatile sensors such as Lidar, Radar, cameras (both monocular and stereo), among many others.  This has led to a rise in the amount of research that combines these two aspects and processes large amounts of data in useful ways.  SLAM is also very useful in a wide range of applications that are of interest to many industries, including self driving vehicles and automated warehouse operations to name a few.


### Specific Problem
The field of SLAM is not new, and this paper only progresses the already very well established wealth of literature on the subject.  Real time visual SLAM has already been implemented [1], and the work in this paper builds upon an even more recent design called PTAM (which stands for parallel tracking and mapping) [2].  ORB-SLAM was built mainly on the work of this algorithm, but with improvements over it.  PTAM had many flaws limiting its application, including lack of loop closing and handling of occlusion, low invariance to viewpoint of the relocalization, as well as requiring manual intervention for map bootstrapping.  These are the problems which ORB-SLAM seeks to overcome.

### Solution Ideas
* The ORB in ORB-SLAM stands for oriented fast and rotated brief, and is an existing robust feature detection algorithm first presented in 2011 [3].  This is the algorithm used to detect features in the image.
* ORB-SLAM also uses three simultaneous threads: a tracking thread, a local mapping thread, and a loop closing thread.  The tracking thread is responsible for localizing the camera and deciding when to insert a keyframe.  The local mapping thread takes in the new keyframes and processes them to reconstruct the surroundings of the camera pose.  The loop closing thread searches for loops in each new keyframe, and when a loop is found it accounts for the drift, aligns the loop, and fuses identical features.
* Each keyframe is stored with the following information
    * Camera pose
    * Camera intrinsics (ie focal length and principal point)
    * All ORB features extracted in that keyframe
* ORB-SLAM also implements a "survival of the fittest" strategy of inserting keyframes, where as many frames as possible are inserted, and redundant ones are later removed.  This approach offers high robustness and is a large advantage over the PTAM model of cautiously inserting keyframes.

### Comments
This paper demonstrates a very robust and effective visual SLAM algorithm by improving upon its predecessors in all of the necessary ways.  The experimental section of this paper showcases the effectiveness of the algorithm on many popular training datasets to verify the efficacy of ORB-SLAM.  I believe that algorithms like ORB-SLAM will be very crucial in the evolving fields of computer vision and SLAM, since having a single monocular camera is both a cheap and simple setup which is much more likely to be implemented in research and industry than large, complicated and expensive setups that provide only minor improvements to performance.


### Citations
[1]  E. Mouragnon, M. Lhuillier, M. Dhome, F. Dekeyser, and P. Sayd, “Real
time localization and 3D reconstruction,” in Proc. IEEE Comput. Soc.
Conf. Comput. Vision Pattern Recog., 2006, vol. 1, pp. 363–370.

[2]  G. Klein and D. Murray, “Parallel tracking and mapping for small AR
workspaces,” in Proc. IEEE ACM Int. Symp. Mixed Augmented Reality,
Nara, Japan, Nov. 2007, pp. 225–234.

[3]  E. Rublee, V. Rabaud, K. Konolige and G. Bradski, "ORB: An efficient alternative to SIFT or SURF," 2011 International Conference on Computer Vision, Barcelona, Spain, 2011, pp. 2564-2571, doi: 10.1109/ICCV.2011.6126544.