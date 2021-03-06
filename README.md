# CarND-Controls-PID
Self-Driving Car Engineer Nanodegree Program

---

There are 3 basic elements of a PID controller 

* P - Proportional
* I - Integral
* D - Derivative

Each of these components have a specific effect on the controller. 

The PID controller runs in a feedback loop and uses the error value from the system. In our case it is the CTE ( Cross Track Error )

This project tuning the parameters has been a time taking process. 

In an attempt to understand and practically observe the effect of each component, I tuned the parameters manually. I supplied a set of values and restarted the simulator programatically for each of these values and monitored the vehicle path.

#### Kp
The value of Kp was directly proportional to the steering angle of the car. The higher the value of Kp the sharper the steering angle of the car. Tuning this parameter especially on the curves was challanging. The lower value could not keep the car in the track as the steering angle was small and a higher value made the car the come back to track but creater sharp oscillations.

#### Ki
The Ki parameter is an integral term that tries to eliminate this residual error by adding a historic cumulative value of the error. Its likely that there would be residual error after applying the proportional control. This ends up causing a bias over a long period of time that avoids the car to get in the exact trajectory.
In my case changing Ki had very little visible effect. There was a little stabilization after adding a value for Ki.

#### Kd
Kp is the amount of correction to apply . This means that for a large value when the error is small will lead to overshoot and , if the controller were to apply a large correction in the opposite direction and repeatedly overshoot the desired position, the output would oscillate.
The Kd param helped with reducing the oscillating effect of the Kp param. The Kd was tuned for each of the Kp values to make sure that the car would not oscillate for small errors and at the same time negotiate tight turns correctly without creating a oscillating effect.
Kd is a derivative term and does not consider the error but the rate of change od error. It tries to bring this rate of change of error to Zero.

### Videos

Only P Controller. 
```cpp
pid.Init( 0.12 , 0 , 0 );
```

https://youtu.be/GMvlFiZrT64

[![](imgs/p.png)](https://youtu.be/GMvlFiZrT64)

PD Controller. 
```cpp
pid.Init( 0.12 , 0 , 3 );
```

https://youtu.be/_N7IS2L5g1w

[![](imgs/pd.png)](https://youtu.be/_N7IS2L5g1w)


PID Controller. 
```cpp
pid.Init( 0.12 , 0.0009 , 3 );
```

https://youtu.be/HDsHO7-0m3E

[![](imgs/pd.png)](https://youtu.be/HDsHO7-0m3E)

---
## Dependencies

* cmake >= 3.5
 * All OSes: [click here for installation instructions](https://cmake.org/install/)
* make >= 4.1(mac, linux), 3.81(Windows)
  * Linux: make is installed by default on most Linux distros
  * Mac: [install Xcode command line tools to get make](https://developer.apple.com/xcode/features/)
  * Windows: [Click here for installation instructions](http://gnuwin32.sourceforge.net/packages/make.htm)
* gcc/g++ >= 5.4
  * Linux: gcc / g++ is installed by default on most Linux distros
  * Mac: same deal as make - [install Xcode command line tools]((https://developer.apple.com/xcode/features/)
  * Windows: recommend using [MinGW](http://www.mingw.org/)
* [uWebSockets](https://github.com/uWebSockets/uWebSockets)
  * Run either `./install-mac.sh` or `./install-ubuntu.sh`.
  * If you install from source, checkout to commit `e94b6e1`, i.e.
    ```
    git clone https://github.com/uWebSockets/uWebSockets 
    cd uWebSockets
    git checkout e94b6e1
    ```
    Some function signatures have changed in v0.14.x. See [this PR](https://github.com/udacity/CarND-MPC-Project/pull/3) for more details.
* Simulator. You can download these from the [project intro page](https://github.com/udacity/self-driving-car-sim/releases) in the classroom.

There's an experimental patch for windows in this [PR](https://github.com/udacity/CarND-PID-Control-Project/pull/3)

## Basic Build Instructions

1. Clone this repo.
2. Make a build directory: `mkdir build && cd build`
3. Compile: `cmake .. && make`
4. Run it: `./pid`. 

Tips for setting up your environment can be found [here](https://classroom.udacity.com/nanodegrees/nd013/parts/40f38239-66b6-46ec-ae68-03afd8a601c8/modules/0949fca6-b379-42af-a919-ee50aa304e6a/lessons/f758c44c-5e40-4e01-93b5-1a82aa4e044f/concepts/23d376c7-0195-4276-bdf0-e02f1f3c665d)

## Editor Settings

We've purposefully kept editor configuration files out of this repo in order to
keep it as simple and environment agnostic as possible. However, we recommend
using the following settings:

* indent using spaces
* set tab width to 2 spaces (keeps the matrices in source code aligned)

## Code Style

Please (do your best to) stick to [Google's C++ style guide](https://google.github.io/styleguide/cppguide.html).

## Project Instructions and Rubric

Note: regardless of the changes you make, your project must be buildable using
cmake and make!

More information is only accessible by people who are already enrolled in Term 2
of CarND. If you are enrolled, see [the project page](https://classroom.udacity.com/nanodegrees/nd013/parts/40f38239-66b6-46ec-ae68-03afd8a601c8/modules/f1820894-8322-4bb3-81aa-b26b3c6dcbaf/lessons/e8235395-22dd-4b87-88e0-d108c5e5bbf4/concepts/6a4d8d42-6a04-4aa6-b284-1697c0fd6562)
for instructions and the project rubric.

## Hints!

* You don't have to follow this directory structure, but if you do, your work
  will span all of the .cpp files here. Keep an eye out for TODOs.

## Call for IDE Profiles Pull Requests

Help your fellow students!

We decided to create Makefiles with cmake to keep this project as platform
agnostic as possible. Similarly, we omitted IDE profiles in order to we ensure
that students don't feel pressured to use one IDE or another.

However! I'd love to help people get up and running with their IDEs of choice.
If you've created a profile for an IDE that you think other students would
appreciate, we'd love to have you add the requisite profile files and
instructions to ide_profiles/. For example if you wanted to add a VS Code
profile, you'd add:

* /ide_profiles/vscode/.vscode
* /ide_profiles/vscode/README.md

The README should explain what the profile does, how to take advantage of it,
and how to install it.

Frankly, I've never been involved in a project with multiple IDE profiles
before. I believe the best way to handle this would be to keep them out of the
repo root to avoid clutter. My expectation is that most profiles will include
instructions to copy files to a new location to get picked up by the IDE, but
that's just a guess.

One last note here: regardless of the IDE used, every submitted project must
still be compilable with cmake and make./

## How to write a README
A well written README file can enhance your project and portfolio.  Develop your abilities to create professional README files by completing [this free course](https://www.udacity.com/course/writing-readmes--ud777).

