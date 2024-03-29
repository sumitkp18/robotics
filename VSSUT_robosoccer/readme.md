# Intro
   
   This project has been started to enable proper research in the field of:
   +  Motion planning and odometry of omnidrive robots 
   + Image Processing and Computer Vision 
   + Artificial Intelligence 
   + Electronics circuit design 
   + Mechanical design 
      
And, prepare multiple autonomous soccer playing robots for the Robocup Small Sized League.


# Working model of 1st prototype: 
https://drive.google.com/file/d/0B7AcDGyuUegYVWpWdWh5Y0dlZXM/view?usp=sharing

   ## Explanation:
   In the video the robot is trying to reach the ball and stop at a particular distance from the ball. It also maintains it orientation such that the its front(marked by green) is always towards the ball.
   
   An overhead camera is used to monitor the area below and the video is captured for processing on a PC usnig Python and OpenCV. The green and red spots on the robot is used to track the position of the robot and determine its orientation w.r.t a reference axes. The green spot marks the front of the robot. The position of the ball is also determined w.r.t the reference axes.
   
   For calculating the motion parameters two parameters are detemined : 
   + Distance of robot's center from the ball's center.
   + The angle between line joining robot's center and ball and line joining the center of two marks on the robot.
    
Two PID controllers are used:
   + to control the speed according to the distanc between the robot and ball and 
   + to minimise the angle between line joining robot's center and ball and line joining the center of two marks on the robot
   
As we are using variable speed in different direections for a kiwi drive holonomic motion, we have calculated the locus of the velocity cone to determine the maximum speed in all directions.

Finally three values are calculated: 
   + the translational speed of the robot (v)
   + the rotational speed of the robot (w)
   + the direction of motion. (Ø)
   
The arduino board on the robot receives these three values and accordingly drives the motors for the required motion.

------------------------------------------------------------------------------------------------------------------------

# Mechanical
    
  ## Motion
        The base of the robot has been prepared for a kiwi drive holonomic motion i.e a three wheeled robot.
        
  ## Wheels:
            The wheels used are 100mm plastic omni wheels.
        
  ## Motors:
            Three Faulhaber Coreless 17W Encoder Motor 120RPM are used to drive the robot.

------------------------------------------------------------------------------------------------------------------------

# Electronics
  
  ## Microcontroller:
          Arduino UNO is being used as the microcontroller board to control the robot.
      
  ## Communication
          Xbee is used for wireless communication between the robot and PC.
      
  ## Motor Drivers
          3 x Cytron 13 amp DC motor drivers are used to control the three motors coupled to the wheels of the robot.
          
  ## Camera
          Intex IT-306WC is used as an overhead camera to take the complete view of the field of motion of the robot

------------------------------------------------------------------------------------------------------------------------

# Programming

The complete robot control is done in the following steps:
   + Capture video from camera through PC
   + Use image processing and algorithms to extract required information from video frames
   + Send the data to MCU on robot through Xbee
   + Command the robot to move and orient in the desired way
      
The complete processing can be categorised into two:
   + Image Processing
   + Robot control
        
 ## Image processing
          
   ### Platform
              We are using OpenCV libraries in Python.
              
   ### Algorithm
              <to be explained>
              
 ## Robot control
           
   The MCU on the robot receives the data packet about the motion from the PC through the xbee.
           
   The data consists of three parameters:
   + x : The required speed in x direction
   + y : The required speed in x direction
   + w : The required angular speed along z-axis
           
   Using the above three parameters and the inverse kinematics matrix, the speed (PWM) and direction of each motor is calculated and the motors are conrolled accordingly.
             
