# CW3-ERSKCCUFO
Creeper World 3 mapping template for the ERS+KCC+UFO gamemode.

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

## KCC
Kajacx Creeper Cloud

A Cloud Maker unit (rainmaker) that will collect creeper or anticreeper to create a cloud. Once enough C/AC is collected, the cloud starts moving towards nearest opposing units, raining creeper or AC down on the ground as it goes.

Hover over a Cloud Maker to see range, clock on it to make it nullifieable / not nullifiable.

### CloudMaker.crpl
Cloud Maker Settings:
   * *CreeperNeeded* - The amount of creeper or AC needed to create a cloud.
   * *CreeperMultiplier* - When cloud is created, it will have *CreeperNeeded* x *CreeperMultiplier* C/AC total ready to rain down.
   * *TeamLock* - Lock the Cloud Maker to specific team - 1 = Enemy (accepts only C), -1 = Friendly (accepts only AC), 0 = Neutral (accepts both C/AC).
   * *WaitTime* - Wait for this many seconds before starting to collect C/AC and producing clouds.
   
Cloud Settings:
   * *CloudMaxHealth* - Health of the clouds, clouds can be damaged by beams.
   * *CloudRainAmount* - C/AC "rained" (added per frame), this will drain the cloud's C/AC reserve until the cloud dissapears.
   * *CloudRainSpeed* - Cloud movement speed, in pixels per frame. 1 cell per second is approx 0.5 pixels per frame.
   * *CloudMaxRange* - Cloud aggro range, in cells. Clouds will only target units in this range from them. Use 9999 for infinite range.

## UFO
"A Cute Alien Muffin"

UFO Base creates UFOs that go and abduct friendly units. UFOs can be temporarly disabled by shooting them with beams, at which point they fall on the ground and can be damaged by snipers. However, fallen UFOs can quickly regenerate and start flying again, shooting it down again with beams will make it crash again, making them damagable by snipers once more. Only "shields" (damagable by beams) is regenerated, real health (damagable by snipers) never regeneates on an UFO.

Destroying an UFO: When you destroy a fallen UFO after it abducted one of your units, that unit will re-spawn at the UFO's current position (except for CN). If a ufo falls where is no terrain, it will instead keep falling into the void, if that happens or the UFO gets away, you will permanently lose the abducted unit (except for CN) and the spawner will begin cooldown towards the next UFO.

Image explanation:
   * Bottom-left corner - target type setting:
     * No image - any (friendly) unit type can be targeted by this UFO
     * Image of a unit - only units of this type can be targeted by this UFO
   * Bottom-right corner - target selection setting:
     * Dots with a cirle - closest possible target will be selected
     * Dots without a cirle - random possible target will be selected
   * Top-left corner - spawn amount setting:
     * No image - 1 UFO will be spawned
     * Image with X UFOs - X UFOs will be spawned
   * Top-right corner - target range setting:
     * 1 colored circle, 2 grayed out circles - limited UFO range (hover over UFO maker or UFO unit to see range)
     * 3 colored circles - infinite UFO range

### UfoMaker.crpl
UFO Maker Settings:
   * *InitialDelay* - After start of the game, wait this many seconds before making the first UFO.
   * *ProductionDelay* - After a UFO is destroyed (or gets away), wait this many seconds before making the next UFO.
   * *UfosSpawned* - Spawn this many UFOs at once. All of them need to be destroyed before the timer continues. Max 5.
   
UFO Unit Settings:
   * *Speed* - UFO movement speed, in pixels per frame. 1 cell per second is approx 0.5 pixels per frame.
   * *BeamHealth* - The amount of "shields" - damage needed from bams to make the UFO fall down.
   * *SniperHealth* - The (real) health of the UFO, this can only be damaged by snipers when fallen and doesn't regenerate.
   * *TargetOnly* - Make UFO target only a specific unit type(s). Separate by comma. List of avaliable types below.
   * *TargetClosest* - 1 to target closest possible target, 0 to target random target. UFO always has infinite range.
   * *TargetRange* - UFO unit target range, in cell radius around the UFO. Use 9999 for infinite range.
   
Possible units types for *TargetOnly*:
   * COLLECTOR
   * RELAY
   * REACTOR
   * SHIELD
   * OREMINE
   * SIPHON
   * TERP
   * GUPPY
   * PULSECANNON
   * MORTAR
   * STRAFER
   * BOMBER
   * NULLIFIER
   * SPRAYER
   * BEAM
   * SNIPER
   * BERTHA
   * GUPPYAIR
   * STRATERAIR
   * BOMBERAIR
   * COMMANDNODE
   * ANTIEMITTER
   * CRPLCORE:CloudMaker
   * CRPLCORE:FlipEmitter
   * CRPLCORE:CreeperCloud

## Creeper Bomb
This unit keeps Creeper or AC inside, until it is released when the timer runs out. Connecting the core of the bomb will allow ammo transfer. Each ammo packet delivered to the core will increase the timer (for Creeper) or decrease the timer (for AC).

### CreeperBomb.crpl
   * *StartDelay* - The amount of time until the bomb is set off.
   * *Radius* - The radius of the bomb.
   * *Amt* - The amount of Creeper held inside. Negative values hold Anti-Creeper.
   * *TimeChangePerPacket* - Can only be positive. The amount of time reduced from (for Creeper) or added to (for AC) the timer, in frames.

## Blind Inhibitor
A "hidden" inhibitor that will spawn only after player collects shield keys. Any number of shield keys is possible (1, 2, 3, 4, ...), and for each order of key collection a different inhibitor can spawn, and 1 inhibitor can have multiple combinations. The player will see "blind" inhibitors as being semi-transparent with possible combinations above them as well as numbers above keys, so they will know which keys to collect in order to spawn which inhibitor.

Wrong setting can resolve in an unpassable map, so make sure that the keys are set correctly. If some inhibitor sequences are missing, then the inhibitor might not spawn, and if some sequence is duplicated, then multiple inhibitors might spawn, eigter way the player can still win, however the keys must be set properly.

### BlindInhibitor.crpl
   * *Squences* - Which key sequences wil lactivate this inhibitor, separated by comma. Examples: "12" or "123,231,312".
   * *EmitInterval* - Creeper spawn interval of the created inhibitor, in frames (1 second = 30 frames).
   * *EmitAmount* - Amount of creeper produce, float creeper value, like in unit editor.

### BlindKey.crpl
   Place and always keep under a shield key (on the same cell).
   * *KeyNumber* - Number of this key for the inhibitor sequence.
   
## FFE - Flip Flop Emitter
Modified flipemitter from CMS, flood with opposing C/AC to switch teams. Both UFOs and Rainclouds can target flipmitters from the opposing team, but only active ones.

### FlipEmitter.crpl
   * *Camt* - Creeper created.
   * *ACamt* - Anti-creeper created, use negative values for AC.
   * *Cinterval* - Creeper production interval, in frames.
   * *ACinterval* - Anti-creeper production interval, in frames.
   * *StartDelay* - Wait this many frames before starting to produce.
   * *StartAsCreeper* - 1 to start as creeper-producing flipmitter, 0 to start as AC producing.
   * *Thresh* - Flooding threshold, this much C/AC is needed to flip this flipmitter.

## Help Menu
A menu with description of each componet, each tab has a space of 768x512 pixels backed by 6 256x256 images. Adding new tabs is done easily in the Help.crpl script, at least until the template runs out of 265x256 image slots, which will probably be soon.

### Help.crpl
   * *DisplayInEdit* - When set to 0, the core will not be in screen mode and will not work. Automaticly fixed when finalized.
   * *Enable[Tab]* - Enables individual help tabs. Useful when you use only some custom units from the template in a map.
