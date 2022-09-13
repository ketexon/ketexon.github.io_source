---
layout: programming_post
title: "Debugger"
date_published: 2022-09-12
start_date: 2022-01-16
end_date: 2022-09-13
updated: false
published: true
repo: "https://github.com/rh5140/srs-team-bug"
tags:
 - Game
 - C#
 - Unity
toc: true
---
# Description

I worked on this game as the technical lead under the supervision of the UCLA club [ACM Studio](https://www.uclaacm.com/committees#studio) Officer (now president) Ray Hsiao during the club's year-long "Students Run Students" game design projects.

The game is a 2D grid-based, turn-based puzzle game where you are a fly trap and your objective is to swallow all the bugs (*ahcktually, they're arthropods*). However, some bugs are not only arthropods, but also *computer* bugs! As of now, their main feature is manipulating movement.

The architecture of the game was set up to be decentralized from Unity. There is a `Board` and on the `Board` there are `BoardObjects` (including bugs, the player, and walls). For each turn, the player gets to make a `BoardAction`, which is only a movement, and the arthropods get to make their own `BoardAction`(s). What makes it interesting is that bugs can register `BoardActionRule`s, which are basically a map of `BoardAction`s. That is, they take in a `BoardAction` and spit a new one out. There is a helper class that lets you construct a `BoardAction` from an enable condition (the rule only works if *condition*), a filter (the rule only applies to `BoardAction`s that *condition*) , and a map (the `BoardAction` gets turned into *blank*). Since `BoardAction` contains information about the creator `BoardObject`, the target `BoardObject`, and the `Board`, this allows for many complex behaviors including selecting what types of `BoardObject`s get affected, having them only work when the arthropod is not in the player's mouth, and having the effect only work when the creator is within a range of the target.

# Reflection

I definitely may have overarchitectured this one. I tried to make it as object oriented as possible. One problem with the OOP was that to create a new behavior for an arthropod, you'd need to create a subclass and add the behavior there. The problem: if you want two behaviors (eg. an arthropod that moves in its turn but also adds a rule) you can't subclass both `MovingArthropod` and `RestrictMotionArthropod`, so you'd need to create a new subclass and copy-paste the code. I did fix this by creating `ArthropodBehavior`, which was essentially just the entire functionality of an arthropod subclass but contained in its own class. I added each arthropod behavior to the main `Arthropod` class and allowed you to disable each one.

Another thing I did was try to make the code as expandable as possible. This is obvious with the `BoardActionRule`, which is generalized to a map. Since there were only a handleful of behaviors, this wasn't necessary. There could have been a bool field labeled "InputFlipped". This would have made it so the player would have to flip the controls themselves, which does not feel separated enough, but it would make it at least 7 times easier. Heck, `Board` probably wasn't needed. We could have just used Unity's physics and world coordinates for everything.

I feel like I did not want to get dirty in this project. If something felt jank, I wanted to make it more "elegant", which led to it being a large codebase for simple behaviors. Next time, I may heed to the advice that the architecture should *not* be generalizable until it has to be.

# Credits

| Name           | Role                                           |
| -------------- | ---------------------------------------------- |
| Ray Hsiao      | Team Lead, UI Designer/Programmer              |
| Alexander Chen | Puzzle Designer, Concept/Sprite Artist         |
| Zane Clark     | Technical Lead, Software Architect, Programmer |
| Mike Han       | UI Programmer                                  |
| Kevin Hong     | Gameplay Programmer                            |
| Amber Jiang    | Art Director, Concept/Sprite/UI Artist         |
| Victoria Lam   | Concept/Tilemap/UI Artist                      |
| Brad Lowe      | Gameplay Programmer                            |
| Felix Peng     | Gameplay Programmer                            |
| Anbu Vajuravel | Writer                                         |
| Andrew Zhu     | Gameplay Programmer                            |
| Spencer Gouw   | Composer                                       |