---
title: Tacticode API Reference

language_tabs:
  - javascript

toc_footers:
  - <a href='https://github.com/tripit/slate'>Documentation Powered by Slate</a>

search: true
---

# Introduction

Welcome to the Tacticode API!

<aside class="success">
This page is still a work-in-progress, do not hesitate to add or edit things!
</aside>


# Retrieving information

## getCurrentEntity()

```javascript
var me = getCurrentEntity();

console.log("Position:", me.x, me.y);
console.log("Team:", me.team);
console.log("Life:", me.health + "/" + me.maxHealth);
console.log("MP:", me.movement + "/" + me.maxMovement);

for (var i = 0; i < me.skills.length; ++i) {
	console.log(me.skills[i]);
}
```

Returns an object containing information about the current character.

### RETURN VALUE

Returns an object containing:

 Variable | Type   | Description
----------|--------|----------------------------------
 id       | number | Unique identifier for the entity 
 name     | string | Name of the entity
 x        | number | X coordinate of the entity
 y        | number | Y coordinate of the entity
 team     | number | Team of the entity
 race     | string | Race of the entity
 health   | number | Current life of the entity
 maxHealth   | number | Maximum life of the entity
 movement    | number | Current movement points of the entity
 maxMovement | number | Maximum movement points of the entity
 skills   | array of string | Array containing the skills this entity can use


## getEntities()

```javascript
var entities = getEntities();

for (var i = 0; i < entities.length; ++i) {
	console.log(entities[i].name, entities[i].x, entities[i].y);
	// ...
}
```

Returns an array containing all entities on the map, including our character.

### RETURN VALUE

Returns an array of entities. See the return value of `getCurrentEntity()` for the definition of an entity.


## getEntityOnCell(x, y)

```javascript
var entity = getEntityOnCell(15, 4);

if (entity !== null) {
	console.log(entity.name, entity.team, entity.race);
	// ...
}
```

If there is an entity on the specified cell, returns the entity. Returns `null` otherwise.

### RETURN VALUE

Returns an entity or `null`. See the return value of `getCurrentEntity()` for the definition of an entity.


## getCell(x, y)

```javascript
var cell = getCell(getPositionX(), getPositionY());

console.log("Current height: ", cell.height);
console.log("Walkable? ", cell.isAccessible);
console.log("Line of sight? ", cell.hasLineOfSight);
```

Returns an object containing information about the specified cell.

### PARAMETERS

Parameter | Type   | Description
----------|--------|-------------
x         | number | X coordinate of the cell.
y         | number | Y coordinate of the cell.

### RETURN VALUE

If the cell does not exist, returns null. Otherwise, returns an object containing the following variables:

 Variable | Type   | Description
----------|--------|----------------------------------
 x        | number | X coordinate of the cell
 y        | number | Y coordinate of the cell
 height   | number | Height of the cell
 isAccessible   | boolean | True if we can walk on the cell, false otherwise.
 hasLineOfSight | boolean | False if the cell is blocking the sight, true otherwise.
 isFree   | boolean | True if there is an entity on the cell.


# Executing actions

## moveToCell(x, y)

```javascript
var result = moveToCell(2, 8);

if (result !== SUCCESS) {
	console.log(entity.name, entity.team, entity.race);
	// ...
}
```

Move the current character to the specified cell.

<aside class="warning">This function will not avoid obstacles, make sure the path is clear!</aside>

### PARAMETERS

Parameter | Type   | Description
----------|--------|-------------
x         | number | X coordinate of the cell.
y         | number | Y coordinate of the cell.

### RETURN VALUE

Returns one of the following values:

 Value                 | Description
-----------------------| ---------------------------------------
 `SUCCESS`             | The character moved to the destination.
 `ERROR_OBSTACLE`      | There is an obstacle preventing the movement.
 `ERROR_NOT_ENOUGH_MP` | The character does not have enough movement points.
 `ERROR_TRAP`          | A trap was activated and interrupted the movement.

<aside class="notice">Even in case of an error, the character might have moved partially!</aside>


## cast(skill, x, y)

```javascript
var entities = getEntities();

cast("Fireball", entities[0].x, entities[0].y);
```

Cast a skill on the specified cell.

### PARAMETERS

Parameter | Type   | Description
----------|--------|-------------
skill     | string | Name of the skill to use.
x         | number | X coordinate of the cell.
y         | number | Y coordinate of the cell.

### RETURN VALUE

Returns one of the following values:

 Value                 | Description
-----------------------| ---------------------------------------
 `SUCCESS`             | The character used the skill successfully.
 `ERROR_ALREADY_USED`  | The character already used a skill this turn.

 
## cast(skill)

```javascript
cast("Heal");

// This is identical to:
cast("Heal", getPositionX(), getPositionY());
```

Cast a skill on the current character. Alias for `cast(spell, getPositionX(), getPositionY())`.

### PARAMETERS

Parameter | Type   | Description
----------|--------|-------------
skill     | string | Name of the skill to use.

### RETURN VALUE

See `cast(skill, x, y)`.


# Waiting for events

## onTurn()

```javascript
function onTurn() {
	var x = getPositionX();
	var y = getPositionY();
	moveToCell(x + 2, y);
	
	var entities = getEntities();
	cast("Arrow", entities[0].x, entities[0].y);	
}
```

You have to declare this event for your script to be valid. This is where you will code your character behaviour.

This event is called once per turn, per character.
