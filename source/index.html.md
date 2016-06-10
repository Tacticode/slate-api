---
title: API Reference

language_tabs:
  - javascript

toc_footers:
  - <a href='https://github.com/tripit/slate'>Documentation Powered by Slate</a>

search: true
---

# Introduction

Welcome to the Tacticode API!

# Retrieving information

## About the character

### getPositionX()

```javascript
var x = getPositionX();
```

Returns the X coordinate of the current character.

### getPositionY()

```javascript
var y = getPositionY();
```

Returns the Y coordinate of the current character.

### getSkills()

```javascript
var skills = getSkills();

for (int i = 0; i < skills.length; ++i) {
	console.log(skills[i]);
	// ...
}
```

Returns an array containing the names of the current character skills.

## About the map

### getCellHeight(x, y)

```javascript
var height = getCellHeight(getPlayerX(), getPlayerY());

console.log("Current height:", height);
```

Returns the height of the specified cell.

### isCellWalkable(x, y)

```javascript
var walkable = isCellWalkable(getPlayerX(), getPlayerY() + 1);

if (walkable) {
	console.log("The cell south of us is walkable.")
}
```

Returns true if an entity can walk on the specified cell, false otherwise.

### hasCellLineOfSight(x, y)

```javascript
var los = hasCellLineOfSight(getPlayerX(), getPlayerY() + 1);

if (los) {
	cast("Fireball", getPlayerX(), getPlayerY() + 2);
}
```

Returns true if the specified cell does not block the line of sight, false otherwise.

## About the other entities

### getEntities()

```javascript
var entities = getEntities();

for (int i = 0; i < entities.length; ++i) {
	console.log(entities[i].name, entities[i].x, entities[i].y);
	// ...
}
```

Returns an array containing all entities on the map, including our character.

 Variable | Type   | Description
----------|--------|----------------------------------
 id       | number | Unique identifier for the entity 
 name     | string | Name of the entity
 x        | number | X coordinate of the entity
 y        | number | Y coordinate of the entity
 team     | number | Team of the entity
 race     | string | Race of the entity

### getEntityOnCell(x, y)

```javascript
var entity = getEntityOnCell(15, 4);

if (entity !== null) {
	console.log(entity.name, entity.team, entity.race);
	// ...
}
```

If there is an entity on the specified cell, returns the entity. Returns `null` otherwise.

# Executing an action

## With our character

### moveToCell(x, y)

### move(direction)

### cast(spell)

### cast(spell, x, y)

# Waiting for an event

## Mandatory events

### onTurn()
