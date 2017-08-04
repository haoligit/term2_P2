# **Project 2 Submission in CarND-Term2**
This repository contains project 2 submission in Self-Driving Car Nano-Degree, Term 2, Unscented Kalman Filters. Modified source codes are all included in folder ./src. The following files are modified:

##### 1. ukf.cpp
##### 2. ukf.h
##### 3. tools.cpp

Besides the standard UKF predict and update functions, a few special treatments are implemented.

1. When initialize state `x_`, for both RADAR and LASER measurement, only `X` and `Y` are initialized accordingly, and `v` `yaw` and `yawd` are set to `ZERO`, since these parameters couldn't be determined by single measurement.

2. When initialize covariance matrix `P_`, covariance of `X` and `Y` are set to `0.0225` for LASER measurement, and set to `0.36` for RADAR measurement, since LASER gives more accurate position measurement than RADAR. All other diagonal elemets are set to `10`.

3. For RADAR measurement update, after using `atan2()` to calculate predicted direction, the angle difference between measurement and prediction is wrapped around to stay within -PI to PI.

4. For process noise standard deviation, I chose `std_a_ = 1.0` for longitudinal acceleration in m/s^2, and `std_yawdd_ = 0.5` for yaw acceleration in rad/s^2.

When running with the simulator, the following tracking RMSE are reported for RADAR only, LASER only and RADAR + LASER:

|    RMSE   | Sensor| X   |  Y | VX | VY |
|:---------:|:---:|:---:|:--:|:--:|:--:|
| Data set 1 |R only| 0.2039 | 0.2513 | 0.3520 | 0.2354|
| Data set 1 |L only| 0.1608 | 0.1474 | 0.4122 | 0.2634|
| Data set 1 |R + L| 0.0665 | 0.0809 | 0.3250 | 0.1954|
| Data set 2 |R only| 0.1911 | 0.2696 | 0.4856 | 0.5865|
| Data set 2 |L only| 0.1542| 0.1380| 0.4241 | 0.2895|
| Data set 2 |R + L| 0.0654 | 0.0651 | 0.3653 | 0.2115|
