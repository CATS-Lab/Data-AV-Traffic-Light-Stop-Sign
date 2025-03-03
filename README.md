# Github dataset README.md

This dataset is derived from the Waymo Motion dataset and focuses on capturing the interactions between autonomous vehicles (AVs) and traffic control devices such as traffic lights and stop signs. It addresses a critical gap by providing real-world trajectory data that reflects how AVs interpret and respond to traffic control signals, supporting research in AV behavior modeling, traffic simulation, and the design of intelligent transportation systems.

# Dataset Overview

- **Data Source:** Waymo Motion dataset
- **Interaction Scenarios:**
    - **Traffic Light Interactions:** Includes stopping, left turns, right turns, and proceeding straight. Over 37,000 trajectory segments are provided.
    - **Stop Sign Interactions:** Includes four-way stops, right turns, one-step left turns, and two-step left turns. Over 44,000 trajectory segments are available.
- **Data Content:**
    - Each segment represents a 9.1-second interval sampled at 0.1-second intervals.
    - Contains AV positions, speeds, and accelerations.
    - Includes the position and state information of traffic lights or stop signs (e.g., red, yellow, green; arrow or circle).

# Data Processing Pipeline

- **Data Extraction**
    - Segments are selected from the Waymo Motion dataset based on predefined rules (e.g., presence of traffic control devices, non-stationary vehicle movement, and trajectory intersection with the control device).
- **Trajectory Organization**
    - Original data in `tfrecord` format is converted into CSV format. In the CSV files, each column represents a time-series variable (e.g., position, speed, acceleration), and each row corresponds to a time step.
- **Quality Assessment and Enhancement**
    - Trajectories are evaluated using metrics such as anomalous acceleration, jerk, and jerk sign inversion ratios.
    - A wavelet-based denoising method (using the db6 wavelet) is applied to reduce noise and anomalies, resulting in smoother and more reliable trajectories.

# Repository Structure

The directory structure of this repository is as follows:

.
├── interactions_with_stop_sign
│   ├── four_way_stops
│   │   ├── left_turns
│   │   ├── right_turns
│   │   └── straight_proceeds
│   ├── one_step_left_turns_at_stop_sign
│   └── two_step_left_turns_at_stop_sign
├── interactions_with_traffic_light
│   ├── left_turns_at_traffic_light
│   ├── right_turns_at_traffic_light
│   ├── stops_at_traffic_light
│   └── straight_proceeds_at_traffic_light
└── [README.md](http://readme.md/)

# Data Structure

The structure of the AV-traffic light interaction data is as follows:

| Attribute | Unit | Description |
| --- | --- | --- |
| AV_speed | m/s | The raw speed of the AV. |
| AV_x | m | The x-coordinate of the AV in the coordinate system defined by Waymo dataset. |
| AV_y | m | The y-coordinate of the AV in the coordinate system defined by Waymo dataset. |
| AV_acc | m/s^2 | The raw acceleration of the AV. |
| AV_distance_to_light | m | The Euclidean distance between the current position of the AV and the controlling traffic light (stop line). |
| nearest_light_x | m | The x-coordinate of the the controlling traffic light in the same coordinate system. |
| nearest_light_y | m | The y-coordinate of the the controlling traffic light in the same coordinate system. |
| nearest_light_state | - | The state of the controlling traffic light, encoded as follows: **0**: unknown **1**: arrow red **2**: arrow yellow **3**: arrow green **4**: circle red **5**: circle yellow **6**: circle green **7**: flashing red **8**: flashing yellow

 |
| AV_speed_enhanced | m/s | The denoised speed of the AV, which helps reduce measurement noise. |
| AV_acc_enhanced | m/s^2 | The denoised acceleration of the AV, which helps reduce the effects of noise and discrete differentiation. |

The structure of the AV-stop sign interaction data is as follows:

| Attribute | Unit | Description |
| --- | --- | --- |
| AV_speed | m/s | The raw speed of the AV. |
| AV_x | m | The x-coordinate of the AV in the coordinate system defined by Waymo dataset. |
| AV_y | m | The y-coordinate of the AV in the coordinate system defined by Waymo dataset. |
| AV_acc | m/s^2 | The raw acceleration of the AV. |
| AV_distance_to_stop_sign | m | The Euclidean distance between the current position of the AV and the nearest stop sign. |
| nearest_stop_sign_x | m | The x-coordinate of the nearest stop sign in the same coordinate system. |
| nearest_stop_sign_y | m | The y-coordinate of the nearest stop sign in the same coordinate system. |
| AV_speed_enhanced | m/s | The denoised speed of the AV, which helps reduce measurement noise. |
| AV_acc_enhanced | m/s^2 | The denoised acceleration of the AV, which helps reduce the effects of noise and discrete differentiation. |

# Note

Due to GitHub repository size limitations, only ten sample data files are provided in each directory of this repository. The full dataset is hosted on Google Drive:

[https://drive.google.com/drive/folders/1bJa62v7YHbsfcZ4yItmFxoIxhrVZvOLW](https://drive.google.com/drive/folders/1bJa62v7YHbsfcZ4yItmFxoIxhrVZvOLW)

If you would like to use the complete dataset, please email us to request access.

**Contact:** Zheng Li, zli2674@wisc.edu

# Citation

If you use this dataset in your research, please cite the following paper:

> Li, Z., Bao, Z., Meng, H., Shi, H., Li, Q., Yao, H., & Li, X. (2025). Interaction Dataset of Autonomous Vehicles with Traffic Lights and Signs. *arXiv preprint arXiv:2501.12536*.
>