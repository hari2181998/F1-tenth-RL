# We are still working on the official deployment of this repo, sorry for the delay!!!



# TC-Driver: Trajectory Conditioned Driving for Robust Autonomous Racing - A Reinforcement Learning Approach

A model-free RL approach to tackle model missmatch and enhance track generalisation in autonomous racing. Instead of end-to-end RL architectures (control output learned directly from sensory input), we can leverage the reliability of traditional planning methods to interact with a low level RL agent that has learned how to drive/race under varying model parameters. This allows for robustness against model mismatch and greater generalisation towards unseen tracks and demonstrates zero-shot Sim2Real capabilities on a physical F1TENTH race car.

This repository contains the code to reproduce the proposed TC-Driver, as well as the benchmark MPCC and End2End architecture in the [F1TENTH Gym environment](https://github.com/f1tenth/f1tenth_gym).  

# Simulation Results

**Tire Generalisation Results**
Results for experiment with tire friction lower than nominal value and outside of training range. Results come from 200 runs.

|            | Lap time t_\mu [s] | Lap time t_\sigma [s] | Crashes   | Advancement adv_\mu | Advancement adv_\sigma |
|------------|--------------------|-----------------------|-----------|---------------------|------------------------|
| MPC        | **10.094**         | 0.501                 | 80.50%    | 32.67%              | 28.26%                 |
| end-to-end | 11.148             | 0.302                 | 73.50%    | 52.51%              | 28.69%                 |
| TC-Driver  | 10.798             | **0.143**             | **2.50%** | **99.37%**          | **4.90%**              |

**Track Generalisation results**
Results for experiment on tracks unseen during training time. Results come from 200 runs.

| Track        | Driver     | Lap time t_\mu [s] | Lap time t_\sigma [s] | Crashes    | Advancement adv_\mu | Advancement adv_\sigma |
|--------------|------------|--------------------|-----------------------|------------|---------------------|------------------------|
| Autodrome    | MPC        | 46.461             | 0.029                 | 0.00%      | 100.00%             | 0.00%                  |
| Autodrome    | end-to-end | **52.5527**        | **0.234**             | 96.00%     | 35.09%              | 27.06%                 |
| Autodrome    | TC-Driver  | 59.020             | 0.307                 | **8.0%**   | **95.32%**          | **17.88%**             |
| Catalunya    | MPC        | 41.475             | 0.036                 | 0.00%      | 100.00%             | 0.00%                  |
| Catalunya    | end-to-end | **46.878**         | **0.207**             | 95.50%     | 44.16%              | **30.33%**             |
| Catalunya    | TC-Driver  | 52.978%            | 0.321                 | **59.50%** | **65.27%**          | 37.03%                 |
| Oschersleben | MPC        | 25.915             | 0.022                 | 0.00%      | 100.00%             | 0.00%                  |
| Oschersleben | end-to-end | n.a.               | n.a.                  | 100.00%    | 19.27%              | **19.93%**             |
| Oschersleben | TC-Driver  | **34.603**         | **0.415**             | **94.00%** | **46.95%**          | 31.23%                 |


# Model Free Zero-Shot Sim2Real Capabilities
The proposed TC-Driver RL agent is trained in simulation only and can be deployed on a physical car, on an unseen track and complete laps with similar crash-ratio as observed in simulation. In the image below, you can see the physical 1:10 scaled F1TENTH car, along with an example track on which it was deployed. 

<img src="/misc/imgs/titlepage_car.png" width="500">

Here you can see the RVIZ visualisation of TC-Driver and the End2End learned architectures. TC-Driver can perform the 10 laps with a single crash, while the End2End architecture fails to complete a single lap without crash. Therefore TC-Driver demonstrates a 10% crash ratio on this track, while End2End has a 100% crash ratio. The rosbag recordings are uploaded [here](/TC_Driver/plotting/).

| TC-Driver | End2End |
| ------ | ------ |
| ![TC](/misc/imgs/tc_rviz.gif) | ![E2E](/misc/imgs/e2e_rviz.gif) |

![Track](/misc/imgs/real_traj.png)

_Note: Different track recordings following._

Lastly here is a gif of the TC-Driver completing its track :)
![TC_video](/misc/imgs/tc_video.gif)

