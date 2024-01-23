# Pedestrian System - Documentation

## System Setup

### Pedestrian Path Spline

Used to specify where NPCs can walk. One or more splines must be laid out in the map to
specify walkable paths. Each instance has a “Closed Loop Toggle” that toggles between a
closed and an open spline.

### Spawners

Spawners specify the areas where NPCs are spawned from, or relocated to. One or more
spawners must be placed around the map, preferably in areas hidden from the player’s view.
Ensure that there is at least one spawner is inside the player region radius as only spawners
inside the radius will spawn NPCs.

### Traffic Poles

Traffic poles come in pairs. They use a user specified ID system to detect their pair. Each
instance will contain an “ID” parameter under the “Crossing ID” section. Any NPC interacting
with a traffic pole will cross to its other pair, at the correct time depending on the traffic light
colour.

### Master Sim Controller

The master sim is used to take in all the parameters of the pedestrian system to aid with the
customisation and functionality of the tool. One instance must be placed on the map, in
order to edit and interact with the system.

### Nav Mesh Bounds Volume

The Nav Mesh Bounds Volume is required for the navigation invoker to build the nav mesh
dynamically during run time, and it’s necessary for the NPCs to move around. Place at least
one instance in the map, ensure full coverage of the pathways the NPCs can take.

## Project Configuration Settings

### Project Settings – Crowd Manager

These settings control the Detour Crowd AI Controller. The “max agents” is set to 100. If
more NPCs are required, the required number needs to be set. The settings can further be
customised as needed.

### Dynamic Navigation Invoker 

Inside the BP_Custom_Player blueprints, in the “components” tab, the navigation invoker
component can be found. The “tile generation radius” is set to 6000. If the player region
radius needs to be above 6000, the tile generation radius must be set accordingly. The “tile
removal radius” can also be modified accordingly

## UI Manual

### NPC Controls

* **NPC Count:** Number of NPCs required within the player region radius.
* **Min and Max Walk Speed:** Each NPC will get a random walk speed between this
range.
* **NPC Colour, Colour Variation and randomisation:** Colour sets the NPC colour, which
has a deviation factor set by the variation. Randomise randomises the colours. If
true, the system will ignore the colour and variation parameters.
* **NPC Height and Variation:** Height sets the scale of the NPC and has a deviation factor
set by the variation.


### Traffic Pole Controls

* **Traffic Light Toggle Time:** Sets the time gap each time the traffic light switches
between the red and green light.
* **Crossing Probability:** The probability of an NPC crossing if it encounters a traffic pole
in its path. For example, a 0.5 probability will mean half of the NPCs will cross at a
traffic pole.
* **Red Green Toggle:** Specifies which light colour represents “go” and “stop”. If true,
green is “go” and red is “stop”, and vice versa.

### Pedestrian Spline Controls

* **Path Noise:** Sets the amount of noise / variation in the target positions generated
along the pedestrian spline.
* **Gap Length:** Sets the distance between each target generated along the spline path.  
(Tip: Turn on “NPC Target Visibility” in the “Debugging Controls” to see the changes reflected
in-game.)

### Player Interaction Controls

* **Player Region Radius:** The region around the player inside which all NPCs are
supposed to exist. If they go outside this radius, they get relocated to one of the
spawners inside the radius.
* **Player Look At Radius:** The radius around the NPC that the player must be inside, for
the NPC to look at / notice the player.
* **NPC Scare Radius:** The radius around the NPC that the player must be inside, to
trigger the NPC interaction animations.

### Debugging Controls

* **Player Walk Speed:** Sets player walk speed. Useful for moving fast across the map for
debugging purposes.
* **Spawner Visibility In Game:** If true, all spawners on the map will be visible during
runtime. If false, they will be hidden in game.
* **NPC Target Visibility In Game:** If true, all targets generated along the pedestrian
spline paths will be visible during runtime. If false, they will be hidden in game.
* **Player Region Radius Debug:** If true, will draw a debug sphere for the player region
radius.
* **NPC Scare Radius Debug:** If true, will draw a debug sphere for the NPC scare radius.
* **NPC Look At Radius Debug:** If true, will draw a debug sphere for the NPC look at
radius.

## Error Checking 

### Pedestrian Path Spline

* “No Pedestrian paths found on the map!!! Place them to specify where the NPCs can
walk.”

### NPCs

* “Min Walk Speed is greater than Max Walk Speed! To ensure proper working of the
system, assign appropriate values.”

### Spawners

* “There are no spawners in the spawner range! Place spawners inside the range or
increase the player region radius.”
* “NPC Spawning Aborted!!! Could not spawn the specified NPC Count because
collision was detected multiple times!” – **It means the system tried to spawn too
many NPCs per spawner, in a small radius, resulting in heavy collision between all
of them. So spawning was aborted to prevent abnormal intersecting between the
NPCs themselves and also the ground. To prevent this, either increase the number
of spawners within the player region radius or decrease the NPC count.**

### Traffic Poles

* “{Traffic Pole Instance} has no ID specified.”
* “{ID} ID found less than 2 times! Cannot make a traffic pole pair. ID found in {Traffic
Pole Instance}”
* “{ID} ID found more than 2 times! Only 2 is required to make a traffic pole pair. ID
found in {Traffic Pole Instance}”

### Master Sim Controller

* 0 instances of BP_Master_Sim is present on the map. Please place one to ensure
proper working of the system.”
* “More than 1 instance of BP_Master_Sim is present on the map. Place make sure
only one is present to ensure proper working of the system.”

### Nav Mesh Bounds Volume

* “No Nav Mesh Bounds Volume found! Add one to the map to ensure proper working
of the system.”
