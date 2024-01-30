---
title: "Pathfinder:Kingmaker Helper"
date: 2021-03-29T13:57:00+10:30
Tags: ['project', 'javascript', 'python']
---

* [Live Site](https://rhiyo.gitlab.io/pfkm-helper/)
* [Code Repository](https://gitlab.com/Rhiyo/pfkm-helper)

thisisthestartofsummary

Last year I played the game Pathfinder Kingmaker and had issues while trying to finish a quest. The quest required you kill 50 specific monsters spread throughout the game. However, the game did tell you which monsters you had killed, just how many. This made it difficult to complete the quest as if you were only missing 1 or 2 monsters, even if you looked online for their locations, if you didn't know which monsters were missing you would still have to check all locations.

I was able to finish the quest but I felt this was a good opporunity to make something that could help others complete the quest more easily. Luckily save files for the game keep a log and within this logs there are flags for when the player had killed a monster that was required for this quest. I made a script in Python that searched for this flag and then went backwards finding the last monster the player killed to make a list of all required monsters and their matching ID in the log file using my log file. With this last I made an app that the player could input their log file into which returns a list of monsters they still need to slay to complete the quest and their locations.

Originally, I had developed this app using Python and Flask, however log files were quite big and using this method required processing the log files host-side. Instead, I switched to using Javascript which allowed for the processing of a file client-side. Meaning no upload of a semi-large file required. An issue with this was that I hadn't worked with JavaScript in a long time. It was a hard transition from Python to JavaScript, but once I found corresponding libraries it became okay. I used [d3](https://d3js.org/) to manage tabular data and a package called [line-navigator](https://www.npmjs.com/package/line-navigator) to read the log file line by line searching for the flags required.

Details for other quests are also tracked in the log file, quests that also require finding things spread out through the game world. Luckily these other quests are better tracked in game making it easier on the player. I still scraped all these items from the log file alongside their locations, however I have yet to implement a feature in the webapp for a user to find what items they are missing in their own log file. This is because it would require more UI work, and is much less sought after in comparison to the original quest I wanted to help people with.

## A good time for CI/CD...

This was also good opportunity to practice ci/cd processes. I made use of Gitlab's Pages as a host for the site and set up a gitlab ci file to deploy the website after any changes to the repository. The deployment is based on a node.js docker so NPM can be used to install packages the javascript webapp depends on. In the future I hope to implement some proper automated node testing and a linter within a testing stage too.
