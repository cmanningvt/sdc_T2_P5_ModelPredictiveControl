## Writeup

---

**Model Predictive Control Project**

[//]: # (Image References)
[image1]: ./examples/car_not_car.png


## [Rubric](https://review.udacity.com/#!/rubrics/896/view) Points
### Here I will consider the rubric points individually and describe how I addressed each point in my implementation.  

---
### Writeup / README

#### 1. Your code should compile.

The following is the the output of the command "cmake .. && make"

-- The C compiler identification is GNU 5.4.0

-- The CXX compiler identification is GNU 5.4.0

-- Check for working C compiler: /usr/bin/cc

-- Check for working C compiler: /usr/bin/cc -- works

-- Detecting C compiler ABI info

-- Detecting C compiler ABI info - done

-- Detecting C compile features

-- Detecting C compile features - done

-- Check for working CXX compiler: /usr/bin/c++

-- Check for working CXX compiler: /usr/bin/c++ -- works

-- Detecting CXX compiler ABI info

-- Detecting CXX compiler ABI info - done

-- Detecting CXX compile features

-- Detecting CXX compile features - done

-- Configuring done

-- Generating done

-- Build files have been written to: /sdc_T2_P5_ModelPredictiveControl/build

Scanning dependencies of target mpc

[ 33%] Building CXX object CMakeFiles/mpc.dir/src/MPC.cpp.o

[ 66%] Building CXX object CMakeFiles/mpc.dir/src/main.cpp.o

[100%] Linking CXX executable mpc

[100%] Built target mpc


This shows no errors and the code compiles successfully.

#### 2. Student describes their model in detail. This includes the state, actuators and update equations.

The algorithm is implemented as discussed in the lessons. The state includes the position (x, y), heading (psi), speed (v), and error terms (cte, epsi). The actuators include the steering and throttle. The update equations are included in the comments of mpc.cpp.

#### 3. Student discusses the reasoning behind the chosen N (timestep length) and dt (elapsed duration between timesteps) values. Additionally the student details the previous values tried.

The values of N and dt are chosen so that the predicted path is far enough in the future bu tthe computation is not too intense to run in real time. I attempted to use different values to reduce the time gap and a sufficient value seem to be anything in the range of 0.9 to 1.2. Anything larger than that caused erratic movements. 

#### 4. A polynomial is fitted to waypoints. If the student preprocesses waypoints, the vehicle state, and/or actuators prior to the MPC procedure it is described.

The points were first adapted to the vehicles coordinate system. So x, y, and psi became zero. Then the polynomial was fit to the waypoints. Before feeding the state vector to the solver, it is adapted to account for a latency using the equations of the vehicle model.

#### 5. The student implements Model Predictive Control that handles a 100 millisecond latency. Student provides details on how they deal with latency.

The latency is handled by adapting the state variables before sending them to the solver. See lines 172-177 of main.cpp.

#### 6. No tire may leave the drivable portion of the track surface. The car may not pop up onto ledges or roll over any surfaces that would otherwise be considered unsafe (if humans were in the vehicle). The car can't go over the curb, but, driving on the lines before the curb is ok.

The vehicle successfully travels a complete lap around the track.