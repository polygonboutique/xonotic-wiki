GSoC 2011 ideas
===============

This page lists a number of ideas given by the developers, which can serve as the bases for a proposal. The ideas are quite short on purpose, you are encouraged to talk to (one of) the prospective mentors about the project to find out more about a certain subject. We can also point you in the right direction regarding documentation or code you may find useful when writing your proposal.

You may obviously come up with your own ideas, but please discuss them with us before writing your proposal. Many ideas are likely to have implications that need to be taken into account, and we may be able to point you to previous attempts of implementing certain features.

Getting in touch
----------------

We frequently hang out in our main irc channel: \#xonotic on Freenode. There are also many other people there who may be able to help you in your quest for information, don’t hesitate to ask!

Alternatively you may contact us using the forums or email. Generally the mentors can be reached by their nickname [at] xonotic.org, if you don’t know who can mentor you please address the emails to admin [at] xonotic [you-know-what-comes-here] org, and we will find someone who can assist you.

FAQ
---

To give you a basic idea of how the game works internally, this is a short summary of the pieces involved. We use the DarkPlaces engine to run the game, the engine is written entirely in C and provides all the features for rendering and integration. The engine is based on the GPL sources of Quake 1, and is still fully compatible with it. The engine spawns a sort of VM that executes the gamecode, this is written in the C-derived language QuakeC. QuakeC is actually a subset of the C language, and is quite easy to learn (if you know a little C you can pick it up in a few hours). The gamecode is compiled using fteqcc, which produces a progs.dat (server code), csprogs.dat (client code) and menu.dat (guess). Maps are created using some form of Radiant, mostly NetRadiant.

Everything that ships with the game is licensed under the GPLv2. This means that all your contributions must also be licensed under this license, but you maintain all the rights to the code you write.

Ideas
-----

### Round-Based Gametype

This is required for games like arena, clan arena, and freezetag. A proper round-based system which allows for two types of spectators: one for each team and one for a player that just joined. Also proper scoring system for this. This includes rewriting some of our current gamemodes to use the round-based system.
Prospective mentors: Samual, Dib, tZork, FruitieX
Effort Level: Medium to High
Knowledge required: QuakeC / C

### Allowing CSQC to control entities (and maybe also ragdolls and animation blending)

Currently tasks such as ragdolls and animation blending cannot be accomplished from the client side, and it would be too harsh on network traffic if we were to do this server side, so essentially the idea is to allow CSQC to manipulate the SSQC entities specifically for this purpose.
Prospective mentors: divVerent, tZork
Effort level: medium
Knowledge required: C

### Loadable mutators

Basically, a dynamic linking system for progs. Additionally to the regular game code, additional game code can be loaded from extra files. These link to the main game code by field/function names, and also have a special initialization function the engine calls at load time. This, with our existing “mutator system”, will provide a full equivalent to Unreal Engine’s “mutators”.
Prospective mentors: divVerent
Effort level: medium
Knowledge required: C

### Implementing a statistics system for Xonotic

We would like to be able to let players keep track of their scores, progress and achievements using a website. We can already generate a lot of output from the game and store that in a centralized way, so this would mainly involve creating a web frontend that ties in with our other webpages and databases.
Prospective mentors: merlijn, detrate, Antibody
Effort level: medium to high
Knowledge required: Databases and some web language like PHP / Python

### Soft Particles and (real) Cel Shading for the engine

Simple effects which need a **real** (defered shadow one won’t work) depth buffer to work properly, they’re also generally light on resources and wouldn’t be very harmful to real time performance.
Prospective mentors: Samual, divVerent, perhaps LordHavoc
Effort level: medium
Knowledge required: C, OpenGL experience, GLSL

### Better player and movement prediction with physics

Right now our player prediction really isn’t all that good, it mismatches a lot and doesn’t account for a lot of things which it needs to. If we could expand upon it and improve it for things such as ladders/hook etc then it would be really fantastic.
Prospective mentors: divVerent, LordHavoc
Effort level: Medium to high
Knowledge required: C and probably some networking knowledge

### Scoreboard re-write/rebase upon new hud code

The current scoreboard code is quite outdated and simply doesn’t fit the new panelhud very well. Remaking a lot of its structure and incorporate it as a separate “page” for the HUD will integrate it better. That in and of itself would open up new possibilities for the HUD, and allow easier extending of the scoreboard for gamemode specific tweaks.
Prospective mentors: Samual, FruitieX
Effort level: Low to medium
Knowledge required: C and some 2D rendering

### Dynamic menu rendering and controls

Improve the current menu system by allowing controls on the menu to be changed in real time (such as strings for buttons or even hiding/showing controls dynamically), so that dialogs can be created and changed dynamically from the code for use in game. The biggest use for this would be to have CSQC menus for things like voting or hud\_setup, which allows a cleaner a way of implementing these with better extendibility.
Prospective mentors: Samual, divVerent
Effort level: Medium
Knowledge required: C

### BOCC

We currently use the FTEQCC project to compile our gamecode, which has quite a few problems. Mainly it lacks ways of implementing more complex optimizations and it doesn’t have very good support for some basic functions like arrays. We have a new project which in its current state cannot yet compile all the gamecode, but allows for better ways of implementing the DP1 assembler and more optimizations. This project would mainly focus on making BOCC work for all of our gamecode, and if possible some minor optimizations.
Prospective mentors: Blub\\0, divVerent
Effort Level: Probably high
Knowledge required: C / C++

### g\_warmup\_allguns 2:

Currently warmup mode gives you every normal weapon, and we would like it to only give the weapons which are available on that map. Right now the weapons are set up for warmup before it is known which weapons are available, so it would probably involve some alternative or work around. This would mainly be useful for competitive play, where warmup mode is pretty default before starting a match.
Prospective mentors: Samual, divVerent
Effort level: low to medium
Knowledge required: QuakeC / C

### Blender for Mappers

Basically, various tools/scripts (or, code changes in Blender) for mappers to efficiently work in Blender that can be easily called from the Blender user interface. Possibilities include: first person shooter-like camera movement (like Radiant has, with forward, backward, strafe left, strafe right, and mouse turning); “brush objects” (quick tools to make a cube, and deform it to put in the appropriate place); texture alignment (mappers typically prefer XY/YZ/ZX axis projections of the texture, Blender can currently do this, but it is quite complex to set up); q3 shader to Blender material import; but also: using Blender to generate lightmaps for an existing .bsp file (possibly done using q3map2’s export-to-obj feature).
Prospective mentors: divVerent
Effort level: low to high, depending on subtask
Knowledge required: Blender, Python, possibly C++

### New bot AI

Our current bots are not very smart, and mappers have to add many waypoints in order to make them move around a map at all. It would be good if the AI could be simplified and be more fun to play against bots. The AI should also be easily extendible for new gamemodes where different objectives can be defined.
Propective mentors: tZork, divVerent
Effort level: medium to high
Knowledge required: AI, QuakeC / C

