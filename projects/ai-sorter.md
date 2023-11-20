---
layout: page
title: AI Sorter
subtitle: A simple AI character that throw away garbages
cover-img: "/assets/projects/ai-sorter/cover.png"
---

## Resume
AI Sorter is a simple AI that walks in a designated space and grab thrashes on the ground when it founds some and throw them in the bin.
I've made this project for 2 reasons :
- I needed something to present about AI for my degree exam
- I wanted to test new methods when using a State Machine and Components

[📥Source code](https://github.com/Tequiloutre/AI_Sorter/tree/main/AI_Sorter/Assets/Scripts)

<br>
<hr>
<br>

## Demo
<video width="640" height="360" controls>
    <source src="/assets/projects/ai-sorter/AISorter_Demo.mp4" type="video/mp4">
</video>

<br>
<hr>
<br>

## Behavior
The architecture of this project remains on two principles :
- `Components` doesn't do anything on `Update` but has public methods that does things
- The behavior is explained on states `Update()` method and calls the needed public methods of the components

For example :
```cs
public class MovementComponent : Component
{
	public void MoveTowards(Vector3 _direction); //Move towards the given direction
}
```

```cs
public class State_Patrol : State
{
	private MovementComponent movement = null;

	public override void Init()
	{
		movement = character.GetMovement; //Gets the MovementComponent of the AI character
		sight = character.GetSight; //Gets the SightComponent of the AI character
		sight.OnTargetDetected += OnTargetDetected; //Subscribe once to needed events to change states
	}

	public override void Update() //This is the state update, not the engine one
	{
		sight.SearchTarget(); //Search targets through the SightComponent, it will trigger the OnTargetDetected event if found
		brain.GetNextPathPoint(_position, out Vector3 _targetPosition); //Gets the next point in the path calculated by the BrainComponent
		Vector3 _direction = _targetPosition - _position;
		movement.MoveTowards(_direction);
	}
}
```
