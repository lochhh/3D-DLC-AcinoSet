# 3D-DLC-AcinoSet
Code for 2-camera based 3D pose estimation using DeepLabCut, based on the [3D DeepLabCut tutorial](https://deeplabcut.github.io/DeepLabCut/docs/Overviewof3D.html) and the [AcinoSet dataset](https://github.com/African-Robotics-Unit/AcinoSet/tree/main).

## Dataset
This code uses [`AcinoSet/data/2017_08_29/top/jules/run1_1`](https://www.dropbox.com/scl/fo/1lakpgu4ft1b7m3msynmc/ADaosJiuuZrti4r7u-_llMg/data/2017_08_29/top/jules/run1_1?dl=0&rlkey=8loeysmtffcj2pnolgqto306o&subfolder_nav_tracking=1).

Specifically, it uses videos from `cam1` and `cam2` along with the corresponding DeepLabCut predictions provided in the [`dlc_pw`](https://www.dropbox.com/scl/fo/1lakpgu4ft1b7m3msynmc/AGldwNGZftCrWaXX3fbkM-I/data/2017_08_29/top/jules/run1_1/dlc_pw?dl=0&rlkey=8loeysmtffcj2pnolgqto306o&subfolder_nav_tracking=1) folder.

## Camera Intrinsics and Extrinsics
As `deeplabcut.calibrate_cameras()` did not yield satisfactory results, the camera parameters were manually created in `generate_camera_params.ipynb` by adapting the calibration results provided in the AcinoSet repository to the `.pickle` files required by DeepLabCut for 3D triangulation. 
These files are expected in `<3D_DLC_Project_Name>/camera_matrix` and include:
- <camera_1_name>_intrinsic_params.pickle
- <camera_2_name>_intrinsic_params.pickle
- stereo_params.pickle

### Intrinsics
The intrinsic calibration files can be found in:
- [AcinoSet/data/intrinsic_calib/2017](https://www.dropbox.com/scl/fo/1lakpgu4ft1b7m3msynmc/ALAdNQLHjGnbpoaEmWUlvTI/data/intrinsic_calib/2017?dl=0&rlkey=8loeysmtffcj2pnolgqto306o&subfolder_nav_tracking=1)

### Extrinsics
The extrinsic calibration files can be found in:
- [AcinoSet/data/2017_08_29/top/extrinsic_calib](https://www.dropbox.com/scl/fo/1lakpgu4ft1b7m3msynmc/AJqm7hd7a7UFwGxDAXj5AO4/data/2017_08_29/top/extrinsic_calib?dl=0&rlkey=8loeysmtffcj2pnolgqto306o&subfolder_nav_tracking=1)

## Triangulation
`deeplabcut.triangulate()` does not work with the provided DeepLabCut predictions, but instead analyses the videos directly using the 2D models (which were not provided with AcinoSet) before triangulating the results.
For this, `Demo_3D_DeepLabCut.ipynb` modifies the triangulation function to directly use the provided 2D predictions from the `dlc_pw` folder.