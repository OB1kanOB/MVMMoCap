#Existing Pose estimation and 3d Reconstruction methods

##Pose Estimation
Pose estimation is a critical process in computer vision that involves detecting and tracking the positions of human body parts, such as joints and limbs, in images and videos. This process has significant applications in robotics, human-computer interaction, and
animation. Various frameworks and approaches have been developed for human pose estimation, including bottom-up and top-down methods.
Bottom-up methods, such as OpenPose (Cao et al., 2021), treat human pose estimation as a part detection problem. OpenPose uses a multi-stage architecture based on convolutional neural networks (CNNs) to detect body parts. It employs a Part Affinity Fields (PAF) model to predict the relationships between parts, providing a comprehensive understanding of the human body’s structure in the image.
Top-down methods, like Convolutional Pose Machines (CPMs) (Wei et al., 2016) and
AlphaPose, start with a whole body model and then fit it to the image. CPMs are
designed to handle occlusions and variations in body scale, posture, and appearance.
AlphaPose, also known as RMPE (Regional Multi-person Pose Estimation)(Fang et al.,
2016), uses predefined models of human bodies to identify key points in an image or
video stream. These keypoints are then used to estimate the overall pose of the body.

![Comparison of detected key-points !](/images/KeypointModelComparison.png "Comparison of detected key-points")
![GRF and SPM comparisons of AlphaPose, BlazePose and OpenPose against
the ground truth (Mundt et al., 2022) !](/images/SPMComparison.png "GRF and SPM comparison")
