Player controller is  an abstract class that is extended by default in teh package by rigidbody player controller. It derives from `Singleton` class, which means it can only have a single instance within each scense.

The idea behind abstract classes should solve issues with cusom logging and suctom functions that are implemented differnetly for 2D and 3D screesn as possibly for mobile screens. Therefore functions below are not necessarilly implemented by default adn you are invited to implemtnt them as you see fit when modifying the player contrller in your won project.

### Variables
#### Rotation
`Vector2 Rotation {get;}`

Returns Vector2 euler angles of World coordinate rotation of the player and camera. X coordinate is 360 calculated with the zero vector of Vector3.Forward, Y coordinate is camera rotation. Setting rotation can be done with [`LookAtPosition`](#lookatposition), as it's rather tricky. 

#### Position
`Vector3 Postition {get; set;}`

Returns position of the player instance.

`Vector2 Vector2Postition {get; set;}`

Returns only X and Z position of Vector3 position.

#### PointingDirection
`Vector2 PointingDirection { get; }`

Returns pointing direction of the player in eulerAngles. Useful for implementation of VR paradigms, where we can use controllers rather than camera to point. In basic Rigidbody implementation it is evvectively same as Rotation.

### Functions
#### MoveToCenter
`void MoveToCenter()`

Useful in experiments where the beginning of trials is positioned at the Vector3(0, y, 0) coordinates. Moves player to the center position while keeping the y axis constant.

#### MoveToPosition
`void  MoveToPosition(Vector2 position)`

Moves player to X and Z world position while keeping the Y axis constant. 

#### Unstuck
`void Unstuck()`

Moves player one bit towards `default(Vector3)`. Should fix any situations where the player gets stuck in walls

#### EnableRotation
`void EnableRotation(bool bo = true)`

Enables or disables rotation of the player-

#### LookAtPosition
`void LookAtPosition(Vector3 point)`

Rotates player and camera to look at a particular point in World coordinates

`void LookAtPosition(Vector2 point)`

Same as previous, but keeps the camera Y axis. Only turns/rotates in horizontal level.

#### SetHeight
`void SetHeight(float height)`

Defines height of the camera in the world view. Usually doesn't modify the colider, but you can implement it if you need.

#### SetSpeed
`void SetSpeed(float speed)`

Sets the speed of player controller to designated float. The speed itself is modified within each controller. Float shoudl be within 0-100, as the attached player controller UI actually only takes these numbers, but you need to define it depending on what controller you are using.

#### HeaderLine
`string HeaderLine()`

Necessary to implement the `IPlayerController` interface for logging purposes. Basically defines column names for the controler to log with [PlayerInformation](#playerinformation). Column names need to be separated by `;` and the string shoudl end with `;`.

!!! example
    ```
    public override string HeaderLine()
    {
        return "Position; Rotation.X; Rotation.Y;";
    }
    ```

#### PlayerInformation
`List<string> PlayerInformation()`

Returns a list with all the information you want to log about hte player every time player information gets logged. This information should correspond to the HeaderLine

!!! example
    ```
    var strgs = new List<string>
    {
        Position.ToString("F4"),
        Rotation.x.ToString("F4"),
        Rotation.y.ToString("F4")
    };
    return strgs;
    ```


## Rigidbody
### Functions
#### Stop
`void Stop()`