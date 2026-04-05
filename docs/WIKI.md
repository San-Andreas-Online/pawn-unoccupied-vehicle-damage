# SA-MP Interaction Menu Documentation

## Table of Contents

- [SA-MP Interaction Menu Documentation](#sa-mp-interaction-menu-documentation)
  - [Table of Contents](#table-of-contents)
  - [Installation](#installation)
  - [Defines](#defines)
  - [⚙️ Functions](#️-functions)
    - [`GetVehicleSize`](#getvehiclesize)
      - [Example usage of GetVehicleSize](#example-usage-of-getvehiclesize)
    - [`GetVehicleDirectionalSpeedDifference`](#getvehicledirectionalspeeddifference)
      - [Example usage of GetVehicleDirectionalSpeedDifference](#example-usage-of-getvehicledirectionalspeeddifference)
  - [🔄 CallBacks](#-callbacks)
    - [`OnEmptyVehicleDamage`](#onemptyvehicledamage)
      - [Example usage of OnEmptyVehicleDamage](#example-usage-of-onemptyvehicledamage)
    - [`OnEmptyVehicleCollide`](#onemptyvehiclecollide)
      - [Example usage of OnEmptyVehicleCollide](#example-usage-of-onemptyvehiclecollide)

---

## Installation

1. Include the script in your SA-MP gamemode:

```pawn
#include <unoccupied_vehicle_damage>
```

## Defines

| Define                                 | Description                                                | Default value  |
| -------------------------------------- | ---------------------------------------------------------- | -------------- |
| `VEHICLE_ATTACK_DETECTION_DELAY_MS`    | Delay between each trigger of vehicle attack detection.    | `500`          |
| `VEHICLE_COLLISION_DETECTION_DELAY_MS` | Delay between each trigger of vehicle collision detection. | `500`          |

## ⚙️ Functions

### `GetVehicleSize`

```pawn
GetVehicleSize(modelID, &Float: size_X, &Float: size_Y, &Float: size_Z)
```

> Retrieves the size dimensions of a vehicle model.  
> **Author**: RyDeR
>
> - **modelID**: The ID of the vehicle model.
> - **size_X**: Reference variable to store the size in the X dimension.
> - **size_Y**: Reference variable to store the size in the Y dimension.
> - **size_Z**: Reference variable to store the size in the Z dimension.
>
> - **Returns**: `true` if the model ID is valid and sizes are retrieved, `false` otherwise.

#### Example usage of GetVehicleSize

```pawn
new modelID = 411, Float:size_X, Float:size_Y, Float:size_Z;
if (GetVehicleSize(modelID, size_X, size_Y, size_Z)) {
    printf("Vehicle model %d size: X=%.2f, Y=%.2f, Z=%.2f", modelID, size_X, size_Y, size_Z);
} else {
    printf("Failed to get size for vehicle model %d.", modelID);
}
```

### `GetVehicleDirectionalSpeedDifference`

```pawn
GetVehicleDirectionalSpeedDifference(vehicleid, comparison_vehicleid, bool:get3d = true)
```

> Retrieves the directional speed difference between two vehicles.
>
> - **vehicleid**: The ID of the first vehicle.
> - **comparison_vehicleid**: The ID of the second vehicle to compare against.
> - **get3d**: If `true`, calculates the 3D speed difference; if `false`, calculates the 2D speed difference.
>
> - **Returns**: The directional speed difference in km/h.

#### Example usage of GetVehicleDirectionalSpeedDifference

```pawn
new vehicleid = 1;
new comparison_vehicleid = 2;
new bool:get3d = true;
new speedDifference = GetVehicleDirectionalSpeedDifference(vehicleid, comparison_vehicleid, get3d);
printf("The directional speed difference between vehicle %d and vehicle %d is %.2f km/h.", vehicleid, comparison_vehicleid, speedDifference);
```

## 🔄 CallBacks

### `OnEmptyVehicleDamage`

```pawn
OnEmptyVehicleDamage(vehicleid, playerid, WEAPON:weaponid)
```

> Triggered when an unoccupied vehicle takes damage caused by a player.
>
> - **vehicleid**: ID of the damaged vehicle.
> - **playerid**: ID of the player who caused the damage.
> - **weaponid**: Weapon used to deal damage.
> - **x, y, z**: Coordinates where the damage occurred.

#### Example usage of OnEmptyVehicleDamage

```pawn
public OnEmptyVehicleDamage(vehicleid, playerid, WEAPON:weaponid, Float:x, Float:y, Float:z)
{
  printf("[UVD] Vehicle %d damaged by player %d with weapon %d at position (%.2f, %.2f, %.2f)", vehicleid, playerid, _:weaponid, x, y, z);
  return 1;
}
```

### `OnEmptyVehicleCollide`

```pawn
OnEmptyVehicleCollide(playerid, vehicleid)
```

> Triggered when a player collides with an unoccupied vehicle.
>
> - **playerid**: ID of the player involved in the collision.
> - **vehicleid**: ID of the unoccupied vehicle.

#### Example usage of OnEmptyVehicleCollide

```pawn
public OnEmptyVehicleCollide(playerid, vehicleid)
{
  printf("[UVD] Player %d collided with empty vehicle %d", playerid, vehicleid);
  return 1;
}
```
