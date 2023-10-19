# Existing Pose estimation and 3d Reconstruction methods

## Pose Estimation
Pose estimation is a critical process in computer vision that involves detecting and tracking the positions of human body parts, such as joints and limbs, in images and videos. This process has significant applications in robotics, human-computer interaction, and animation. Various frameworks and approaches have been developed for human pose estimation, including bottom-up and top-down methods.

Bottom-up methods, such as OpenPose (Cao et al., 2021), treat human pose estimation as a part detection problem. OpenPose uses a multi-stage architecture based on convolutional neural networks (CNNs) to detect body parts. It employs a Part Affinity Fields (PAF) model to predict the relationships between parts, providing a comprehensive understanding of the human body’s structure in the image.

Top-down methods, like Convolutional Pose Machines (CPMs) (Wei et al., 2016) and
AlphaPose, start with a whole body model and then fit it to the image. CPMs are
designed to handle occlusions and variations in body scale, posture, and appearance.
AlphaPose, also known as RMPE (Regional Multi-person Pose Estimation)(Fang et al.,
2016), uses predefined models of human bodies to identify key points in an image or
video stream. These keypoints are then used to estimate the overall pose of the body.

| ![Comparison of detected key-points !](/images/KeypointModelComparison.png "Comparison of detected key-points") |
|:--:| 
| *Comparison of detected key-points* |

| ![GRF and SPM comparisons of AlphaPose, BlazePose and OpenPose against the ground truth (Mundt et al., 2022) !](/images/SPMComparison.png "GRF and SPM comparison") |
|:--:| 
| *GRF and SPM comparisons of AlphaPose, BlazePose and OpenPose against the ground truth (Mundt et al., 2022)* |

## 3D Reconstruction
Following pose estimation, 3D reconstruction from multiple 2D poses is the next
crucial step. This process involves generating a 3D model of an object or a scene from
multiple 2D views, a critical step in applications such as live performance capture and
reconstruction.
Direct methods for 3D reconstruction, such as structure from motion (SfM), multiple
view stereo (MVS), and multi-view triangular mesh generation (MVT), use the 2D poses
directly to generate a 3D model. SfM involves reconstructing the 3D structure of a scene
from two or more images, while MVS uses multiple views of a scene to generate a dense
3D point cloud. MVT involves triangulating multiple views of a scene to generate a 3D
triangular mesh.(Hartley & Sturm, 1997)(Henry & Christian, 2022)

| ![Example of 2 RGB-D camera setup (Meerits et al., 2019) !](/images/RGBDCameraSetup.png "Example of 2 RGB-D camera setup") |
|:--:| 
| *Example of 2 RGB-D camera setup (Meerits et al., 2019)* |

Indirect methods, on the other hand, first estimate the 3D poses from the 2D poses and
then use these 3D poses to reconstruct the scene. These methods often involve the use
of human body models, such as the statistical body model (SBM) or the articulated body
model (ABM). These models can be trained on large datasets of 3D human poses and
can generate high-quality 3D reconstructions of human bodies in real-time. There are
various implementations of SBMs and ABMs that have been used in combination with
2D pose estimation models, including the SMPL model (Loper et al., 2015), which is a
widely used SBM, and the MANO model (Romero et al., 2017), which is an ABM that
models the human hand. These models can be trained on large datasets of 3D human poses, and can be used to generate high-quality 3D reconstructions of human bodies in
real-time.

| ![Joints and weights distribution in SMPL (Loper et al., 2015) !](/images/SMPLWeightDistribution.png "Joints and weights distribution in SMPL") |
|:--:| 
| *Joints and weights distribution in SMPL (Loper et al., 2015)* |

There are also approaches that aim to achieve 3D pose estimation and reconstruction
using a single RGB image, such as the Human Mesh Recovery (HMR) model (Kanazawa
et al., 2018) and SMPLify-X (Pavlakos et al., 2019). The underlying idea of this
technique involves utilizing a parametric body model, like SMPL (Skinned Multi-Person
Linear), and iteratively fitting its projection to the 2D image by refining its pose, joint
angles, and scale. By minimizing the reprojection error, the model generates 3D pose
estimates from a monocular image.

| ![Shows the iterative fitting on monocular 2D image (Eidos.Ai, 2021)-1 !](/images/SMPL3dpose1.png "Shows the iterative fitting on monocular 2D image") |
|:--:| 
| ![Shows the iterative fitting on monocular 2D image (Eidos.Ai, 2021)-2 !](/images/SMPL3dpose2.png "Shows the iterative fitting on monocular 2D image") |
| ![Shows the iterative fitting on monocular 2D image (Eidos.Ai, 2021)-3 !](/images/SMPL3dpose3.png "Shows the iterative fitting on monocular 2D image") |
| *Shows the iterative fitting on monocular 2D image (Eidos.Ai, 2021)* |

It’s crucial to acknowledge that the method under discussion has certain constraints.
The primary limitation is that it offers a 3D pose representation of the skeleton within
the reference frame of the 2D image, without taking into account the broader scene,
particularly in the context of a video sequence. As a result, depth information is lost
when the subject is moving. In the case of 2D pose detection using AlphaPose, there
is a recognized 3D pose estimation model, HybrIK (Li et al., 2021) (Li et al., 2023),
which is built on the method mentioned above. However, it’s essential to be aware
of the shortcomings of this approach, especially its restricted depth information in dynamic scenes. This limitation was highlighted during our experiments with custom
data gathered from our specific scene.

| ![Comparison of GLAMR vs HybrIK estimation showing the impact of global optimization of positioning (Yuan et al., 2022). !](/images/GLAMRvsHybrIK.png "Comparison of GLAMR vs HybrIK") |
|:--:| 
| *Comparison of GLAMR vs HybrIK estimation showing the impact of global optimization of positioning (Yuan et al., 2022)* |

The challenge of dynamic camera or subject movement is also tackled in another paper,
GLAMR (Yuan et al., 2022), which enhances the results of HybrIK while operating
on a monocular image/video. Unlike previous studies, this method reconstructs human
meshes in consistent global coordinates, even with dynamic cameras. Given that the
joint reconstruction of human motions and camera poses is underdetermined, a global
trajectory predictor is employed. This predictor generates global human trajectories
based on local body movements. Utilizing the predicted trajectories as anchors, the
global optimization framework refines these trajectories and optimizes the camera poses
to align with the video evidence, such as 2D keypoints.
