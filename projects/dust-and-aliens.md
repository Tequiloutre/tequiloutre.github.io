---
layout: page
title: Dust & Aliens
subtitle: A game where there's dust and also aliens
cover-img: "/assets/projects/dust-and-aliens/cover.png"
---

## Resume

<a href="/assets/projects/dust-and-aliens/hud.jpg"><img src="/assets/projects/dust-and-aliens/hud.jpg" style="float: right; max-width: 45%; margin-left: 2%;"></a>

Dust & Aliens is a Fast FPS Roguelite set in futuristic western universe.

The player takes on the role of a cowboy who must fight waves of aliens in different arenas.

<a href="/assets/projects/dust-and-aliens/hud.jpg"><img src="/assets/projects/dust-and-aliens/shop.jpg" style="float: left; max-width: 45%; margin-right: 2%;"></a>

The goal of the game is to advance through the various arenas to get the highest score possible.

Use this score to buy upgrades and try to get as far as possible to defeat the game's final boss.

<p align="center"><a href="https://store.steampowered.com/app/2190230/Dust_and_Aliens/">The game is available on Steam for free</a></p>

<br>
<hr>
<br>

## Context

This was our 3rd year school project for which we teamed up in "real conditions" with other progs, designers, game designers, sound designers, etc... to work on a AAA-type video game.

We started prototyping the game at the end of our 2nd year on Unreal Engine 4.7 and decided to restart on a new, clean project on UE 5.1 on 3rd year when we were almost sure of the architecture of the game.

<br>
<hr>
<br>

## My work on this project
### Entities

The **player** and the **enemies** have many things in common so we decided to make them have a **common parent** : `DA_Entity`.

`DA_Entity` inherit from `APawn` to handle `AController` easily and contains a `DA_MovementComponent`.

<p align="center"><a href="/assets/projects/dust-and-aliens/uml_actors.png"><img src="/assets/projects/dust-and-aliens/uml_actors.png"></a></p>

<br>
<hr>
<br>

### Movement

As well as the **entities**, the **player** and the **enemies** movements are very similar so they have a **common parent** : `DA_MovementComponent`

<p align="center"><a href="/assets/projects/dust-and-aliens/uml_movements.png"><img src="/assets/projects/dust-and-aliens/uml_movements.png"></a></p>

We used the Unreal's `UMovementComponent` because it already **handles collisions** but decided not to use the `UCharacterMovement` for 2 reasons :
- it contains many mechanics that we didn't need
- we decided to do a state machine

<br>
<hr>
<br>

### State Machine

Because the **player** had many different movements and the **aliens** will need those same movements to be able to **follow him**, we decided to create a **State Machine** :

| [![uml_movement_fsm](/assets/projects/dust-and-aliens/uml_movement_fsm.png)](/assets/projects/dust-and-aliens/uml_movement_fsm.png) | [![movement_states](/assets/projects/dust-and-aliens/movement_states.png)](/assets/projects/dust-and-aliens/movement_states.png) |

Our `DA_MovementComponent` works as a **State Machine**, it has a **TMap** that contains all possible `DA_MovementState` associated with an enum to get it easily.

All the possible **states** are created **once** and overrides those methods :
- `StateEnter()`
- `StateUpdate()`
- `StateExit()`

to explain their behaviour but only the **active state** make the entity **move**.

When an **event** is **triggered** *(ex: ground is detected, jump is asked, ...)* the corresponding **state** is set as **active** and now works instead of the previous.
