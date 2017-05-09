# CarND-Controls-PID
Self-Driving Car Engineer Nanodegree Program
- PID Controller Project: implement a PID controller to enable autonamous driving in Simulator. 
---
## PID Parameter and Tuning
There are 3 parameters for PID controller: proportional coefficient, integral coefficient, and derivative coefficient. 
* Proportional: This parameter produces an output value that is proportional to the cross track error (CTE). Larger value tends to cause unstablity due to overshooting. Smaller value may result in unresponsible or unsensitive control. 
* Integral: This parameter deals with certain offset or bias of the control system. It calcuates the sum of the instantaneous error over time and gives the accumulated offset that should have been corrected previously.
* Derivative: This parameter is to reduce the oscillation and overshooting of the proportinal coefficient. It predicts system behavior and thus improves settling time and stability of the controller. 

There are a few ways to tune these PID parameters such as manual tuning and twiddle. In this project, I tried manual tuning first and it worked just fine. 
I first tried to change all 3 paremeters together and it turns out to be a bad idea. The car drove off the track immediately and I had no way to tell which parameters to tune next. 
Then I started using only proportinal parameter. I began with 5 and it caused the car overshooting. It must be too big. So I reduce it from 5 gradually to 1. The it seemed better but the car oscillated a lot. I know I should add derivative parameters to solve the issue. But when the derivative parameter is too big like 5, the car wiggles a lot. So I reduce it down to 1. The result is acceptable. Then I tried change both proportional and derivative parameters little by little and find the best combination (0.07, 0, 1).
For the integral term, I tried a few small values and it didn't change the result that much. This may be due to the provided CTE is accurate enough without much bias. But I still set the integral parameter to a small value 0.001 in case there is still some accumulated offset for the controller. 

## PID Result and Discussion
![GIF of PID Controller](https://github.com/buaalsy2003/CarND-PID-Control-Project/blob/master/PID.gif)

With the tuned PID parameters, the car can stay in the lane and run smoothly in the simulator for many laps without major issues. In cases of high speed or sharp turn, the car may approach to lane edges or wiggle a little. The speed can go up to 60mph.
In the future, I will implement Twiddle algorithm to estimate parameter range before manual fine tune. This will speed up the process, especially for larger or more complex control system. 

## Dependencies

* cmake >= 3.5
 * All OSes: [click here for installation instructions](https://cmake.org/install/)
* make >= 4.1
  * Linux: make is installed by default on most Linux distros
  * Mac: [install Xcode command line tools to get make](https://developer.apple.com/xcode/features/)
  * Windows: [Click here for installation instructions](http://gnuwin32.sourceforge.net/packages/make.htm)
* gcc/g++ >= 5.4
  * Linux: gcc / g++ is installed by default on most Linux distros
  * Mac: same deal as make - [install Xcode command line tools]((https://developer.apple.com/xcode/features/)
  * Windows: recommend using [MinGW](http://www.mingw.org/)
* [uWebSockets](https://github.com/uWebSockets/uWebSockets) == 0.13, but the master branch will probably work just fine
  * Follow the instructions in the [uWebSockets README](https://github.com/uWebSockets/uWebSockets/blob/master/README.md) to get setup for your platform. You can download the zip of the appropriate version from the [releases page](https://github.com/uWebSockets/uWebSockets/releases). Here's a link to the [v0.13 zip](https://github.com/uWebSockets/uWebSockets/archive/v0.13.0.zip).
  * If you run OSX and have homebrew installed you can just run the ./install-mac.sh script to install this
* Simulator. You can download these from the [project intro page](https://github.com/udacity/CarND-PID-Control-Project/releases) in the classroom.

## Basic Build Instructions

1. Clone this repo.
2. Make a build directory: `mkdir build && cd build`
3. Compile: `cmake .. && make`
4. Run it: `./pid`. 

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
