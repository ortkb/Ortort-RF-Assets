# Kill Throttle Audio on Player Exit

Made to address the bug(?) of the Throttle Audio continuing to play if the player leaves the vehicle while still accelerating.
This simply makes sure to turn off the Throttle Audio when the player exits the vehicle.

### USAGE ###

Place the killThrottleAudioOnExit prefab as a child of your 'Throttle Audio Source' Game Object. 
Then place the Game Object that contains the Arcade Car script (I think any vehicle script will work) as the value of the 'vehicleTarget' target.