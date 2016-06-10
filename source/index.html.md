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

Returns the X coordinate of the current character.

```javascript
var x = getPositionX();
```

### getPositionY()

Returns the Y coordinate of the current character.

```javascript
var y = getPositionY();
```

### getSkills()

Returns an array containing the names of the current character skills.

```javascript
var skills = getSkills();

for (int i = 0; i < skills.length; ++i) {
	console.log(skills[i]);
	// ...
}
```

## About the map

### getCellHeight(x, y)

Returns the height of the specified cell.

```javascript
var height = getCellHeight(getPlayerX(), getPlayerY());

console.log("Current height:", height);
```

### isCellWalkable(x, y)

Returns true if an entity can walk on the specified cell, false otherwise.

```javascript
var walkable = isCellWalkable(getPlayerX(), getPlayerY() + 1);

if (walkable) {
	console.log("The cell south of us is walkable.")
}```

### hasCellLineOfSight(x, y)

Returns true if the specified cell does not block the line of sight, false otherwise.

```javascript
var los = hasCellLineOfSight(getPlayerX(), getPlayerY() + 1);

if (los) {
	cast("Fireball", getPlayerX(), getPlayerY() + 2);
}```

## About the other entities

### getEntities()

Returns an array containing all entities on the map, including our character.

 Variable | Type   | Description
----------|--------|----------------------------------
 id       | number | Unique identifier for the entity 
----------|--------|----------------------------------
 name     | string | Name of the entity
----------|--------|----------------------------------
 x        | number | X coordinate of the entity
----------|--------|----------------------------------
 y        | number | Y coordinate of the entity
----------|--------|----------------------------------
 team     | number | Team of the entity
----------|--------|----------------------------------
 race     | string | Race of the entity

```javascript
var entities = getEntities();

for (int i = 0; i < entities.length; ++i) {
	console.log(entities[i].name, entities[i].x, entities[i].y);
	// ...
}
```

### getEntityOnCell(x, y)

If there is an entity on the specified cell, returns the entity. Returns `null` otherwise.

```javascript
var entity = getEntityOnCell(15, 4);

if (entity !== null) {
	console.log(entity.name, entity.team, entity.race);
	// ...
}
```

# Executing an action

## With our character

### moveToCell(x, y)

### move(direction)

### cast(spell)

### cast(spell, x, y)

# Waiting for an event

## Mandatory events

### onTurn()
