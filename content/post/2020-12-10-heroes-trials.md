---
title: "Heroes Trials"
date: 2020-12-10T02:02:32+10:30
Tags: ['c-sharp','unity','released-game','game-ai']
---

While living in Tokyo I volunteered for a convention “Tokyo Sandbox.” Which focuses on giving indie game developers the opportunity to show their work to game industry veterans and investors. During this event I met the developer for an RPG game called “Adel” at the time. They were looking for someone to develop the AI for their game which lead to me eventually working with him and his company [Shinyuden](http://www.shinyuden.com/homepage/). As of 2018 the game has been released on PlayStation, Switch, Steam and Xbox.

I spent about 1 year on the project in which the skills I used were

* C# Programming for Unity.
* Building an AI Framework for Boss Encounters and general enemies.
* Managing software amongst a team using SVN.
* Refactoring old code to fit with newer systems.

# My Experience

I joined the game development team about halfway through and the framework for the full game was mostly already there. However, there was a lot of issues that needed to be fixed. The game was built using several disparate Unity Plugins and didn’t mesh together as well as it could have. Furthermore, there was no robust AI, the reason I was brought in. I replaced the simple AI plugin they were using with my own implementation of a hierarchical state machine tool [that can be found on GitHub](https://github.com/Rhiyo/RoseHFSM). This also required me acting as a designer, as the boss encounters were not implemented and required someone to plan out how the encounter would work using the AI system.

Much of the old code required refactoring to make sure all the systems would work together, this made it easy to iterate over content and makes changes when need be. Originally, when an issue would arise, we would find it difficult to find where as the code was hard to read and was often left alone to not cause issues. Refactoring helped to follow the code and fix with any issues we had further on.

As for project management, when I joined, they had decided to cut back the game to have less content to make it more feasible for a small, busy, team to release on time. Overall, we worked well together, but were rushed within the last weeks to fix small issues that were lingering and left alone for too long. I also tried implementing small features just before the release, which almost caused an issue. In this regard, I now know not to leave bugs, however small, for too long as they might be harder to fix then what was original though. Furthermore, it is never a good idea to attempt to add new features, however small, before the release of the game. 
