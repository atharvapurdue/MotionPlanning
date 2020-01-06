# CODE EXPLAINATION (STARTER CODE + MY CODE)
## Below are the sreenshots of the code and a brief explaination  

![Alt text](https://github.com/sparklytopaz/MotionPlanning/blob/master/m1.JPG?raw=true "m1")

*Here, all the necessary libraries are imported* 
Class `States` : defines the 7 states that a Unmanned Aerial Vehicle can take and they are assigned values automatically.
>>- &nbsp;1. MANUAL 
>>- &nbsp;2. ARMING
>>- &nbsp;3. TAKEOFF
>>- &nbsp;4. WAYPOINT
>>- &nbsp;5. LANDING
>>- &nbsp;6. DISARMING
>>- &nbsp;7. PLANNING

![Alt text](https://github.com/sparklytopaz/MotionPlanning/blob/master/m2.JPG?raw=true "m2")

Class `MotionPlanning` is a child class of udacidrone drone class.
Whenever an instance is created, `__init__()` function is called.`__init()` function initialises the following variables:-
>>- &nbsp;target_position
>>- &nbsp;waypoints
>>- &nbsp;in_mission
>>- &nbsp;check_states
Also, callback functions are registered such as:-
>>- &nbsp;position
>>- &nbsp;velocity
>>- &nbsp;state 

Function`local_position_callback` is triggered everytime there is a change in the position of the UAV. The function response depends on the flight_state variable.

Function `velocity_callback()` is a callback function which is triggered whenever there is a change in the velocity of the UAV.This function responds only when the UAV is in the LANDING state and checks if the UAV altitude is within 0.1m of the global home position    altitude. If so and the UAV is within 0.01m of the ground, the function calls the disarming_transition() function.


![Alt text](https://github.com/sparklytopaz/MotionPlanning/blob/master/m3.png?raw=true "m3")

The `state_callback` function is called periodically in a heartbeat fashion and is responsible for advancing the flight status of the UAV. The function responds based on the current flight status as below:

>>MANUAL : When the flight state is MANUAL the function calls the arming_transition() function to proceed to arm and gain control of the UAV.

>>ARMING : When the flight state is ARMING and the UAV is armed, the function calls on the path_plan() function to proceed to plan a path for the UAV to follow.

>>PLANNING : When the flight state is PLANNING the function calls the takeoff_transition() function to make the UAV takeoff to target altitude.

>>DISARMING : When the flight state is DISARMING and the UAV is not armed and not in guided mode, the function calls the manual_transition() function to disarm the UAV
    
The `arming_transition()` function performs the following tasks :

- &nbsp; Changes the flight state to **ARMING** 
- &nbsp; Arms the drone
- &nbsp; Changes control of UAV from manual to guided

The `takeoff_transition()` function performs the following tasks :

- &nbsp; Changes the flight state to **TAKEOFF** 
- &nbsp; Initiates the UAV takeoff to the target position altitude.

The `waypoint_transition()` function performs the following tasks :

- &nbsp; Changes the flight state to **WAYPOINT** 
- &nbsp; Sets the target position to the next waypooint.
- &nbsp; Commans the UAV to the target position.

The `landing_transition()` function performs the following tasks :

- &nbsp; Changes the flight state to **LANDING** 
- &nbsp; Initiates the landing pocedure of the UAV.

The `disarming_transition()` function performs the following tasks :

- &nbsp; Changes the flight state to **DISARMING**
- &nbsp; Disarms the drone
- &nbsp; Changes control of UAV from guided to manual

![Alt text](https://github.com/sparklytopaz/MotionPlanning/blob/master/m4.png?raw=true "m4")

The `manual_transition()` function performs the following tasks :

- &nbsp; Changes the flight state to **MANUAL**
- &nbsp; Stops the drone
- &nbsp; Sets the `in_mission` variable to False

![waypoint transition](./misc/mp_send_waypoints.PNG)

The `send_waypoint()` function sends the waypoints to the FCND Simulator for visualization purposes.

![plan path](./misc/mp_plan_path.PNG)

The `plan_path()` function performs the following tasks :

- &nbsp; Changes the flight state to **PLANNING**
- &nbsp; Sets the `TARGET_ALTITUDE` & `SAFETY_DISTANCE` parameters
- &nbsp; Sets the `target_position` altitude to `TARGET_ALTITUDE`

![Alt text](https://github.com/sparklytopaz/MotionPlanning/blob/master/m5.png?raw=true "m5")

Function `TAKEOFF` : When the flight state is TAKEOFF the function checks if the UAV is within 95 % of the target altitude. When so, it calls the waypoint_transition() function.
    
Function `WAYPOINT` : When the flight state is WAYPOINT the function checks if the UAV is within 1m of the target waypoint.If that is the case and  there are no more waypoints,it calls the landing_transition() function.If there are more waypoints left, then the waypoint_transition()  function is called again to proceed to the next waypoint.
  
Function `VELOCITY` : This is the velocity callback function which is triggered whenever there is a change in the velocity of the UAV.This function responds only when the UAV is in the LANDING state and checks if the UAV altitude is within 0.1m of the global home position altitude. If so and the UAV is within 0.01m of the ground, the function calls the disarming_transition() function.
![Alt text](https://github.com/sparklytopaz/MotionPlanning/blob/master/m6.png?raw=true "m6")
**hi**
![Alt text](https://github.com/sparklytopaz/MotionPlanning/blob/master/m7.png?raw=true "m7")
