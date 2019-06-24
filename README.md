# CW3-ERSUFO
Creeper World 3 mapping template for the ERS+UFO gamemode.

Creeper World 3 is property of https://knucklecracker.com/

## ERS
Enemy Radioactivity Source

This unit will deal damage to friendly units in range. Below is a list of all properties that can be modified on an ERS unit.

### ERSUnitBase.crpl
   * *Power* - The total damage dealt to each unit in range per minute. You can find how much health each player unit has here https://knucklecracker.com/wiki/doku.php?id=cw3:unit_data_overview. Heal rate is completely turned off for all units in range of the radioactivity. For example, a Mortar, having 2 health, will die in exactly 2 minutes with a *Power* value of 1.
   * *Radius* - The radius of the damage circle.
   * *Decay* - This is a multiplier of how much the circle radius will change after a minute has passed. For example, 0.9 means circle will shrink by 10% after 1 minute. 0.75 means circle will shrink by 25% after 1 minute.
   * *StartDelay* - The amount of game frames until the unit starts emitting/moving.
   * *Health* - The amount of health the unit has to defend against AC if *HurtByAntiCreeper* is enabled. 1 health equals exactly 1 minute of exposure to AC that is required to destroy the unit.
   * *Type* - Set to 0 to damage all units. Set to 1 to damage all landed units. Set to 2 to damage all flying units.
   * *StrengthBasedOnRange* - If set to 0, the amount of damage dealt to units inside the circle is always equal to *Power*. If set to 1, more damage is dealt closer to the epicenter - 0\**Power* at the edge, 1\**Power* in the middle between edge and epicenter, 2\**Power* in the epicenter.
   * *HurtByAntiCreeper* - If set to 0, the unit cannot be damaged by AC. If set to 1, the unit will be damaged if submerged in AC.
   
### ERSUnitMovement.crpl
   * *Speed* - The speed the unit will move at, measured in cells travelled per second.
   * *Waypoint1/2/3...* - Designate the coordinates the unit should move between. Always start from Waypoint1. Input coordinates in this format: `x,y`. For example, if you set Waypoint1 to `0,0`, Waypoint2 to `0,10` and Waypoint3 to `10,10`, the unit will move in a triangle shape around the top left corner of the map.
