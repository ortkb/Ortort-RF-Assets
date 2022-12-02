# Mute AudioSource on exiting a Vehicle

Made to address the bug(?) of the Throttle / Brake Audio continuing to play if the player leaves the vehicle while still accelerating / braking.
This simply makes sure to mute the AudioSource this prefab is parented to when the player exits the vehicle.

### USAGE ###

Place the muteAudioOnVehicleExit prefab as a child of your 'Throttle Audio Source' or 'Brake Sounds' Game Object. 
Then place the Game Object that contains the Arcade Car / Vehicle script as the value of the 'vehicleTarget' target.

### KNOWN ISSUES ###
If an audio source was muted previously, it can be briefly be heard fading out when reentering the vehicle driver seat.