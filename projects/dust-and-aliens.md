---
layout: page
title: Dust & Aliens
subtitle: A game where there's dust and also aliens
cover-img: "/assets/projects/dust-and-aliens/cover.png"
---

## Resume
Dust & Aliens is a Roguelike Fast FPS game where you play as a robot cowboy that kills aliens in a futuristic western arena.

This was our 3rd year school project for which we teamed up in "real conditions" with other progs, designers, game designers, sound designers, etc... to work on a AAA-type video game.

We started prototyping the game at the end of our 2nd year on Unreal Engine 4.7 and decided to restart on a new, clean project on UE 5.1 on 3rd year when we were almost sure of the architecture of the game.

<hr>

## My work on this project
### 3C & Entities

The **player** and the **enemies** have many things in common so we decided to make them have a **common parent** : `DA_Entity`

`DA_Entity` inherit from `APawn` to handle controlers easily and contains a `DA_MovementComponent`

| [![uml_actors](/assets/projects/dust-and-aliens/uml_actors.png)](/assets/projects/dust-and-aliens/uml_actors.png) |

<hr>

### Movement

As well as the **entities**, the **player** and the **enemies** movements are very similar so they have a **common parent** : `DA_MovementComponent`

| [![uml_movements](/assets/projects/dust-and-aliens/uml_movements.png)](/assets/projects/dust-and-aliens/uml_movements.png) |

We used the Unreal's `UMovementComponent` because it already **handles collisions** but decided not to use the `UCharacterMovement` for 2 reasons :
- it contains many mechanics that we didn't need
- we decided to do a state machine

<hr>

### State Machine

Because the **player** had many different movements and the **aliens** will need those same movements to be able to **follow him**, we decided to create a **State Machine** :

| [![uml_movement_fsm](/assets/projects/dust-and-aliens/uml_movement_fsm.png)](/assets/projects/dust-and-aliens/uml_movement_fsm.png) | [![movement_states](/assets/projects/dust-and-aliens/movement_states.png)](/assets/projects/dust-and-aliens/movement_states.png) |

Our `DA_MovementComponent` works as a **State Machine**, it has a **TMap** that contains all possible `DA_MovementState` associated with an enum to get it easily.

All the possible **states** are created **once** and overrides those methods :
- `StateEnter()`
- `StateUpdate()`
- `StateExit()`

to explain their behaviour but only the **active state** make the entity **move**.

When an **event** is **triggered** *(ex: ground is detected or jump is asked, ...)* the corresponding **state** is set as **active** and now works instead of the previous.

```cpp
bool PortProcess::Execute(const std::vector<std::string>& _args)
{
	if (_args.size() != 1) return false;
	
	Port* _targetPort = VM::GetActiveNode()->GetPort(stoi(_args[0]));
	if (!_targetPort || _targetPort->GetType() != targetType) return false;
	_targetPort->Open();
	return true;
}
```