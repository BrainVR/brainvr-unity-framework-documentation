## Arena objects
Arena objects are game objects with implemented functions for positionings, rotations etc. Arena objects come with Arena object manager as well, which allows grouping of controllers of the same type and doing madifications groupwise (such as setting same height or colour). Specific implementations of arena object is the Goal object ([Goal controller](#goal controller)and [Goal manager](#goal manager)) and mark object ([Mark controller](#mark controller)and [Mark manager](#mark manager)), see those sections for info.

### Arena object controller
Arena obejct (AO) controller shoudl consist of a single empty game object with only controller script attached. It has `PossibleObjects` and `ActiveObject` parameters which are usually children obejcts, that AO can change "into". When creating an AO object, don't forget to add it's child object as well. Arena object shoudl have all colliders and mesh renderers in child objects, not on the same object where is the controller script.

#### Variables

Variable          | Purpose       
----------------- | ------------- 
ActiveObject      | active game object if any
PossibleObjects   | Contains an array of possible nested gameobjects to be played with with `SetType`. Can be set in unity
Position          | Vector3 position in world coordinates

#### Functions
Function          | Purpose       
----------------- | ------------- 
[Show](arena-object.md#show) | Shows the object and enables all non trigger collider.
[Hide](arena-object.md#hide) | If the ocject is visible, it becomes invisible
[SetRotation](arena-object.md#arena-object-controller#setrotation) | Sets the obejct rotation with the Quaternion.
[StartRotation](arena-object.md#startrotation)  | Starts rotating the object in a given vector.
[StopRotation](arena-object.md#stoprotation)  | If the object is rotating, stops the rotation.
[SetSize](arena-object.md#setsize)  | Sets the scale according to passed vector.
[SetColor](arena-object.md#setcolor) | Sets the colour of the main material of the object. Saves the previous colour so you can call `ResetColor()` 
[ResetColor](arena-object.md#resetcolor)  | resets the color to the original one.
[SetType](arena-object.md#settype) | Sets the object to the one desired, based on its string name.
[Switch](arena-object.md#switch)| Switches betwen visible and invisible state and returns the current state.

### Arena object manager
Arena object manager allows to manage and controll all assigned controllers of a given type. Common practice is to have a single manager for each type of object that you have in scene. 
By defualt, Arena object manager is a singleton, so you can't have multiple in the same scene. If you need more, you can override the base class or create multiple child classes of distinct names out of the single implementation of a single manager (eg. Start manager can have two children, Star1Manager and Start2Manager which inherit from the a base class)

#### Variables
Variable          | Purpose       
----------------- | ------------- 
Objects | Generic list of all the obejct of the fiven type that manager holds.


#### Functions
Function          | Purpose       
----------------- | ------------- 
[ShowAll](arena-object-manager.md#showall) | Shows the object and enables all non trigger collider.
[HideAll](arena-object-manager.md#hideall) | If the ocject is visible, it becomes invisible
[SetColor](arena-object-manager.md#set-color) | Sets the colour of all assigned objects.
[ResetColor](arena-object-manager.md#reset-color)  | resets the color to the original one.
[SetType](arena-object-manager.md#set-type) | Sets all assigned objects to the one desired, based on its string name.

### Goal Object
Goal object adds some additional functionality to the arena object by adding event functionality. It inherits all the functionality from the [Arena Object](#Arena Object) and [Arena object Controller](#Arena object Controller).

#### Goal controller
Goal controller (GC) extends [Arena object controller](#arena-object-controller) but adds goal/target specific functinoality

#### Variables
Variable          | Purpose       
----------------- | ------------- 
[GoalName](objects/goal-controller.md#GoalName) | Holds the name of goal object.
[PlayerInside](objects/goal-controller.md#PlayerInside) | Holds the bool value of if player is inside the goal or not.

##### Events
Events          | Purpose       
----------------- | ------------- 
[OnEnter](objects/goal-controller.md#OnEnter) | Is sent when player enters the goal object.
[OnExit](objects/goal-controller.md#OnExit) | Is sent when player exits the goal object.

#### Goal manager
Goal manager extend [Arena object manager](#Arena-object-manager). It is a singleton that is used to manage and controll all referenced [Goal Controllers](#Goal Controller).

#### Variables
Variable          | Purpose       
----------------- | ------------- 
[GetGoal](objects/goal-manager.md#GetGoal) | Returns a Goal controller script given by index.
[ResizeGoals](objects/goal-manager.md#ResizeGoals) | Resizes the local scale of all of the goals objects.
[InstantiateGoalsCircumference](objects/goal-manager.md#InstantiateGoalsCircumference) | Instantiates goals attributes.

## Experiment manager
Experiemnt manager is reponsible for loading expeirment from the data and manipulating expeirment states.

### Functions
Function | Purpose
----------------- | ------------- 
[LoadExperiment](experiment-manager.md#loadexperiment) | initialises the expeirment form name and possible settings file.
[StartExperiment](experiment-manager.md#) | Starts the expeirment.
[StopExperiment](experiment-manager.md#)| Stops the expeirment.
[RestartExperiment](experiment-manager.md#) | Stops and then starts expperiment. buggy ATM.
[SwitchExperimentState](experiment-manager.md#) | Doens't do anything at this point.
[SetTrial](experiment-manager.md#) | Sets the trial to designated number.

## Player controllers
PLayer controllers build upon the player controller and `IPlayerController` class to proovide bothe control as well as loggin informiaton necessary for conprehensive logs across differnet modalities of play (PC. VR, mobile etc.). Some functiuon needs to be implemented in order ot create sa new player log.

### Variables
Variable          | Purpose       
----------------- | ------------- 
[Position](player-controller.md#Position)| Returns player position
[Rotation](player-controller.md#rotation)| Returns player rotation
[Vector2Postition](player-controller.md#position)| Returns player position in X and Z
[PointingDirection](player-controller.md#pointingdirection)| Returns rotation of player pointing.


### Functions
Function          | Purpose       
----------------- | ------------- 
[MoveToCenter](player-controller.md#movetocenter) | Generic list of all the obejct of the fiven type that manager holds.
[unstuck](player-controller.md#unstuck)| Tries to unlock player if they get stuck in mesh.
[EnableMovement](player-controller.md#enablemovement)|Enables or disables movement
[EnableRotation](player-controller.md#enablerotation)| Enables or disables rotation
[LookAtPosition](player-controller.md#lookatposition)| Rotates player to face certain point
[SetHeight](player-controller.md#movetocenter)| Sets player height
[SetSpeed](player-controller.md#movetocenter)| Sets player speed

### Rigidbody player controller

## Beeper
Beepers are designed to simply play sounds when certain events happen within the game. Beeper objects have beeper manager and beeper controlers.

### Beeper Manager
[BeeperManager](beeper-manager) takes care of cntrolling all attached controllers and plays souds based on string designation

#### Variables
Variable          | Function       
----------------- | ------------- 
[BeeperControlles](beeper-manager.md#beepercontrolers) | list of all attached BeeperControllers.

#### Function
Function          | Function       
----------------- | ------------- 
[Play](beeper-manager.md#beepercontrolers) | Plays one shot of the sounds in the controller

##

## Data holders

### Settings holder

## Input manager

## Console manager