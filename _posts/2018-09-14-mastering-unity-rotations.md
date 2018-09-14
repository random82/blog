---
layout: post
title:  Learnings from a project inception
date:   2018-09-14 10:53:18 +1100
category: software development
tags: [unity3d, scripting]
---

# Mastering Unity3D rotations

## Real-life toy problem

Few days ago I started learning more about Unity 3D and I had some problems with understanding rotations in a three dimensional space. Even though 3D engines might offer all necessary transformations, setting objects in desired places still remains a problem. I decided to build a model in Unity specifically to play with rotations.

A model that helped me to understand different aspects of rotations was Rubik's Cube - a puzzle invented in 1974 by a professor of architecture [Wikipedia: Rubik's Cube](https://en.wikipedia.org/wiki/Rubik%27s_Cube). The original version of the puzzle requires moving blocks along different place to put 26 blocks (cubelets) in a correct place.

## Building the cube - finding rotation planes

The reason why the cube worked so well for me is because it requires implementing rotations of cubelet groups that wont break structure of the cube. Also, the implementation should allow rotating groups of objects in 9 planes. 

I've started with cube set up as follows:

## Animation - how to get exact rotation