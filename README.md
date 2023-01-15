# Tricycle-model-Control-on-simulink
The car-like model used in this project is the tricycle model described in 3.2.3.1 above to model
this system a Simulink model is created based on the tricycle kinematics shown in equation 3.2.
As shown in Figure 3.5 kinematic model block has 3 inputs. The first input is the steering angle in
degrees which is then converted to radiant before being used by the block, the second input is the
velocity, the last input is the length of the vehicle itself (the distance between the rear axle and the
front axle).
On the other side of the block are the outputs of the model, these outputs area the rate of change
of the x and y positions as well as the rate of change in the heading angle of the robot with respect
to a fixed reference frame
![image](https://user-images.githubusercontent.com/122736585/212552831-8a3e94c7-00e3-4178-89a9-e76e1c0215eb.png)

Open loop simulation

The first simulation for the implemented tricycle model is an open-loop simulation meant to test
the model and verify that it is working properly. In this simulation as shown in Figure 3.6 the input
of the model that controls the steering angle of the vehicle is connected to a knop, this knop when
tuned it changes the input steering angle of the model. The second input which is the speed, is
connected to a toggle switch which controls whether or not the vehicle is moving, if the switch is
off the vehicle is stationary, if it is on the vehicle
moves at a constant speed. Figure 3.7 shows the path took the vehicle during the simulation based
on the user inputs, from this figure it can be seen that the vehicle turns according to the input of
the user on the steering knop, this is with respect to the relation between the heading angle and
steering angle of course. 

Closed Loop Simulation

Now that the model has been tested to be working in an open loop simulation. In this subsection it
will be tested in closed loop simulations to observe its performance in more realistic situations.
Shown in Figure 3.8 the closed loop system. Here, the same kinematic model used earlier in the
open-loop simulation is connected here to a controller, this controller issues motion commands to
the vehicle model, these commands aim to drive the vehicle towards a defined goal point. When
the vehicle moves, it provides feedback on the position and heading angle to the controller to help
it minimize the error towards the goal point. In the prototype’s implementation (which will be
discussed thoroughly in 3.3 below) the feedback on the position will be provided by the GPS
module and the feedback on the heading angle will be provided by the compass module

Waypoint Following Technique

A kinematic method is required once a target waypoint is chosen, which enables the robot to travel
to the waypoint. A kinematic model algorithm for the destination robot (44) was created by Coulter
at Carnegie Mellon University. The robot measures as much of the arc as it can go from the current
location to the destination position and calculates the look-ahead distance to pursue the destination.
According to the method, the vehicle follows a certain procedure as shown below to track the
point:
50
1- Define the vehicle’s heading and its position
2- Define the waypoint’s destination
3- Convert the waypoint’s position into the coordinate system of the of the vehicle.
4- Define the lookahead distance between the vehicle and the point and also the angle.
5- Compare the angle between the point and the vehicle and the heading angle of the
vehicle.
6- Determine (calculate) the steering and throttling control angles

Following a target point based on user input

Once the target point following technique is implemented, the first closed loop simulation could
be made. This simulation involves the robot tracking a goal point defined by the user. This
simulation shown in Figure 3.10 the kinematic model block on the right provides feedback of the
position and the heading angle of the vehicle with respect to a fixed reference frame to the
controller block on the left, the controller which is a proportional controller, takes the current
position of the robot and its heading angle along with the goal point provided by the user, then it
calculated the error in the heading angle based on the error in the distance using trigonometry.
Based on the error between the robot’s position and the goal point it outputs the desired heading
angle and motion command, it sends 0 to stop the vehicle and sends 1 to move it. This procedure
Is repeated until the robot reaches the goal point, then it stops.

Multiple Waypoint Tracking

After accomplishment a specific waypoint successfully, another closed loop simulation was
created to make the robot follow 6 different predefined waypoints consecutively. This attained by
generating two arrays in the geometric path tracking block, as the first array has the X coordinates
and the second has Y coordinates of the waypoints that the robot should pass through them. Also,
a knob was added to control the speed of the robot based on user input. lastly as it shown in Figure
3.12 that robot had effectively reached the 6 waypoints that are in green color as shown in Figure
3.13.




