# RF-Drift-Controller

I'm fairly certain either something in the script or the particles are responsible for causing occasional lag spikes. If you find a fix (it's probably the number of particles tbh), feel free to message me - or just branch or push the changes. 

### CONFIGURATION ### 
(Configurable values found in the driftController > Data Container component)

- 'Ground Detect Range' - Distance the drift controller checks below itself to see if there's any ground, to determine whether the vehicle is grounded (is the ground at least X number of meters below?). Default: 0.65
    Activate the the line renderer component on the driftController to visually see this distance (when testing the vehicle - it won't show in the Unity preview).

- 'Skid Trails Y Offset' - Offset to Y-axis position of the drift tyre trails. Used to adjust the placement of the trails upwards so they don't go underneath the ground. Default: 0.1

- 'Min Handbrake Skid Velocity' - Minimum forward velocity the vehicle needs to be while braking to start a drift. Set to -1 to disable brake drifing. Default: 18

- 'Min Lateral Skid Velocity' - Minimum lateral (horizontal) velocity for the vehicle to start a drift (i.e. sharp turns at high speeds). Set to -1 to disable lateral skid drifing. Default: 14

- 'Drift Linger Duration' - How long the drift effects will continue after the vehicle has finished a drift. Default: 0.55 

- 'Drift Audio Gain Rate' - How fast the drift sfx gains in volume. Default: 2

- 'Drift Audio Decrease Rate' - How fast the drift sfx loses volume once the drift has ended. Default: 2

### USAGE ###

Place the GameObject that contains the Arcade Car script (I think any vehicle script will work) as the value of the 'vehicleTarget' target (found under driftController > Scripted Behaviour > Targets). 

By default, the configurable values are set up for use on my AE86 Trueno Mod. These preset values should work decently well out of the box for fast vehicles that can make sharp turns - though you would need to change the positions of the effects and audio source GameObjects to fit the shape of your vehicle.  
You would likely need to adjust the 'Ground Detect Range' and 'Min Handbrake / Lateral Skid Velocity' values to fit the height and speed of your vehicle. 

- 'Skid Trails Parent' - Parent object for particle effects that will play while drifting. Moves along the ground.
To keep the tyre skid trails on the ground, the script will update the Y position of 'Skid Trails Parent' GameObject every frame - everything under 'Skid Trails Parent' will move relative to the ground.
- 'Extra Effect Parent' - Parent object for particle effects that will play while drifting.
The 'Extra Effects Parent' GameObject does not move - and will stay fixed on the vehicle. You can use it to add exhaust flares or fumes, or any other particle effects you want to play while drifting.
- 'Drift SFX' - Contains audio clip to play while drifting.

### HOW IT WORKS ###

The driftController GameObject checks so see if there's collision underneath its position within a set distance ([Ground Detect Range] distance). If there is, then the vehicle is considered on the ground. If not, a drift cannot start and any existing drift is stopped.
    * Note that the check only determines whether the driftController is close to the ground, *not* the vehicle rigidbody or the individual wheels. If you want each wheel to have an independent ground distance check, you'd probably want a driftController on each wheel.
If either the lateral velocity or forward velocity while braking goes over the configured values (Min Lateral / Handbrake Skid Velocity) while the vehicle is considered on the ground, then a drift is triggered. Each particle system under the targets 'trailTarget' and 'otherEffectsTarget' are set to Play() for the duration of the drift + Drift Linger Duration. The audio fades in and out during this. 
    * Note that only particle systems are set to play. This is because as far as I'm aware, Trail Renderers are not exposed in Ravenscript (so the best I could do with trails is toggle setActive - which gets rid of existing skid marks). 


Credits:
Smoke Sprite Sheet from RF Tools Pack.
Drift audio from Sound Effects Wiki's files from 'The Odyssey Collection: Expanded Sound Effects Library' by Pro Sound Effects.
Link: https://soundeffects.fandom.com/wiki/Pro_Sound_Effects,_Vehicle_Skidding_Maneuvers,_CU_and_Distant,_Many_Tire_Squeals,_Sliding,_High_Revs,_Hard_Accelerations,_Car_Drifting,_Many_Variations [Accessed 25/11/2022] 