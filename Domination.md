Domination (DOM)
================

Object of the Game
------------------

In domination, the goal is to capture and hold all control points on the map. Domination is similar to [Onslaught](Onslaught) but capturing a control point is easier in Domination, and in Domination points are given for holding a control point, and there is no generator. Rarely are maps made exclusively for Domination, generally an existing [CTF](Capture_the_Flag) or [TDM](Team_Deathmatch) map receives Domination features.

Map Entities
------------

A domination map must have at the very least 4 entities.

### dom\_team

dom\_team entites declare the teams available in the game and what models are shown when they take a control point. To create it, right click and go to “domination\>dom\_team”. There must be at least 3 per map: Two teams and one empty team (for when the control point is not taken).

    // entity 244
    {
    "classname" "dom_team"
    "origin" "-24.000000 0.000000 96.000000"
    "message" "Blue team has captured a control point"
    "model" "models/domination/dom_blue.md3"
    "netname" "^4Blue Team^3"
    "noise" "domination/claim.wav"
    "noise1" "domination/claim.wav"
    "cnt" "13"
    }
    // entity 245
    {
    "classname" "dom_team"
    "origin" "16.000000 0.000000 96.000000"
    "cnt" "4"
    "message" "Red team has captured a control point"
    "model" "models/domination/dom_red.md3"
    "netname" "^1Red Team^3"
    "noise" "domination/claim.wav"
    "noise1" "domination/claim.wav"
    }
    // entity 246
    {
    "classname" "dom_team"
    "origin" "-8.000000 0.000000 128.000000"
    "model" "models/domination/dom_unclaimed.md3"
    }

These are the three dom\_team entites you must have on your map. It does not matter where they are placed. The first two examples here declare two dom teams: blue and red. The third declares the “empty team”. It is best to copy these verbatim into your map, as their structure does not change (of course, the coordinates do change depending on where you placed them).

### dom\_controlpoint

These are the actual control points that players will capture. They do not have any required fields, but it is often useful to name them. Here is an example of a declaration of a dom\_controlpoint entity in the .map file.

    "classname" "dom_controlpoint"
    "origin" "0.000000 2240.000000 608.000000"
    "message" " has captured ^1Red Base^3"

The key here is the “message” field, which allows you to set the message shown when a controlpoint is captured. Generally, the format of this is " has captured CONTROLPOINTNAME". You can also use color codes in these messages, as shown in the above example.

Helpful Hints and Tips
----------------------

-   _(Insert Hints Here)_

List of Demos and Videos
------------------------

-   Demo: _(Insert Demo or Video Here)_
-   Players: _(Insert Player Names Here)_
-   Key Points: _(Insert key points in match here)_
