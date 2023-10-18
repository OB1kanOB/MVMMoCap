# Detailed Results

Notable findings from the analysis include the following:
- Removal of a single camera from a well-balanced 8 camera setup has a relatively
minor impact, resulting in an error margin on the order of 0.06 meters. This
suggests that the overall system remains robust even with the absence of one
camera.
- The implementation of a semicircular camera setup consisting of 5 cameras
generally produces satisfactory results in terms of triangulation. However, it
should be noted that when the subject is facing away from the cameras, the pose
estimation model struggles to accurately detect facial features such as the eyes
and nose. Despite this limitation, reliable estimations for the remaining body
joints are still achieved. The length error analysis indicates that the 5-camera
setup exhibits slightly lower error compared to the 8-camera setup. However, it is
important to consider external factors and the specific choice of cameras removed
for the semicircular setup, which may introduce calibration errors. Therefore, the
lower error observed in the 5-camera setup does not necessarily imply that it is
superior. Upon visualizing the skeleton and mesh, it becomes evident that there
are some discrepancies between these two setups.
- With a reduction in the number of cameras to 4, while still maintaining uniform
coverage through a diagonal arrangement, the triangulation results remain comparable to those achieved in previous setups. It is important to highlight a distinct
peak observed during leg-raising motions, such as a kick. This peak is likely
attributed to the rapid movement, resulting in limited visibility from multiple
angles.
- The performance of 3 and 2 camera setups is generally unsatisfactory, as evidenced
by significant fluctuations and glitching in the reconstructed skeleton. These
configurations struggle to provide consistent and accurate pose estimations.

![8 camera vs 7 camera arrangement !](/images/8v7cam.png "8 camera vs 7 camera arrangement")
![8 camera vs 5 camera arrangement !](/images/8v5cam.png "8 camera vs 5 camera arrangement")
![8 camera vs 4 camera arrangement !](/images/8v4cam.png "8 camera vs 4 camera arrangement")
![8 camera vs 3 camera arrangement !](/images/8v3cam.png "8 camera vs 3 camera arrangement")
![8 camera vs 2 camera arrangement !](/images/8v2cam.png "8 camera vs 2 camera arrangement")
