# Kuka-youBot-Pick-and-place-object-
Modelling in Robotics

The main objective of this project is to make the KUKA youBot move using forward and inverse kinematics. 

We designed and implemented a simulation on the youBot to pick up the cube from a given initial position and moves its base towards a designated position and place the cube.

The project was implemented by using the following steps:

  a. Inverse kinematics: It is necessary to place the arm in the desired positions (to pick up the cube, place it in the tray and put it      in the basket). It works is by giving the desired position coordinates (x,y,z) as an input, the toolframe angles (alpha, beta) and      the gripper value (in this project we used 0 for closed gripper and 0.01 for open gripper). It provides the joint angles (5 in          total) that are calculated to go to the position, the gripper output and a boolean output (0 or 1) for the solution which                corresponds to whether the arm can reach the desired position or not. The tool angle is fixed at [0 -90] 
  
  b. Robot movement: The robot must move straight with a given linear velocity and sideways with a given transversal velocity. We            calculated the linear velocities to be 0.1666 and 0.15 for transversal. This value can be estimated by dividing the meters              travelled with the seconds required.
  
  c. Enable Arm/Enable Base: For the robot to complete its task successfully, two boolean variables can be used. The first one is the
     EnableArm which at 1 enables the arm while it performs the pick and place cube task. The second is the EnableBase which at 1,            enables the base to move with linear and transversal velocity.
     
  d. Counter/Clock: There is a need of a counter that increases every six seconds so, so as to separate each movement in steps and            activate them with a counter clock. This counter has a period of 6 seconds and its maximum value is 255. The Matlab function has        been implemented in such a way that if the all the steps have been executed, the robot does nothing (arm and base boolean variables      are set to 0).
  
  e. Sequence Implementation: From the counter function above, we can generate an input sequence for the function block. The function        block has hardcoded values for various movements for the robot arm and base. The input to the function is a regular step signal          which indicates the time allocated for each movement of the robot (counter). The output is a matrix containing the following values      in a sequence: -
     
     [enablearm enablebase x y z gripper linear transversal]
     
     Enablearm - This binary output determines the activation state of the arm. 1 instructs the arm to accept signals from the youBot PC      and 0 indicates an inactive state.
     
     Enablebase - This binary output determines the activation state of the base wheels. 1 instructs the wheels to accept signals from        the youBot PC and 0 indicates an inactive state. x y z - These parameters indicate the position of the end effector tool. 
     
     Gripper - This binary input controls the actions of the gripper. This indicates the extent to which a gripper needs to be opened.

     Linear - The linear speed is passed with this parameter. The speed is in meters per second.
     
     Angular - The angular speed is passed with this parameter. The speed is in meters per second. 
     
From the obtained matrix from the Matlab function block, a demux is used to seperate all the values and give them as inputs to the youBot and inverse Kinematics blocks. To be noted that we need to mux the x y z values after demuxing them to be able to input them in the Inverse kinematics block.

After that, while the model is running, every six seconds a set of parameters is coming out of the function and goes in the other blocks. The final output is the movement of the arm or the base that is observed on the robot.

Credits:
Georgios Tsiatsios - gets0002@student.umu.se
Ganesh Chaitanya Kudaka - chku0012@student.umu.se
Senthilkumar Konnaiyandi Sivakumaran - seko0011@student.umu.se
