Key Hunt (KH)
=============

![](http://pics.nexuizninjaz.com/images/6498jb823699s0xkz726.jpg)
![](http://pics.nexuizninjaz.com/images/wwkcbz3r5gtyuhwi.jpg)

Object of the Game
------------------

Key Hunt is a round-based game mode normally played with 3 teams, but 2 or 4 teams are also possible.

In each round, one player of each team gets a key. The goal of each round is to collect all the keys and gather up to score a lot of points. The first team to reach the score goal (default: 1000) wins the match.

Gameplay
--------
The game is played in seamless rounds. At the beginning of a round, one player per team gets a key in the color of the own team. The player who got the key (called “key carrier”) will see a message and the team mates will instantly see the position of the allied key carrier.

A few seconds after the beginning of a round, the positions of all keys will be revealed to everyone in the HUD and radar.

To win a round (and score big), your team has to grab all the keys and join them together. As soon as a team has all the keys, they must meet. If a single player collects all the keys, the team also wins the round.

It is possible that a key is destroyed or lost during a round (e.g. by dropping it into the abyss or a deathtrap). The key carrier who lost or destroyed the key will lose the round for the team. The color of the key does not matter. This can happen for one of two reasons:

1. The key carrier destroyed/lost the key due to own clumsiness: The team is “punished” by rewarding all other teams with a few points. This will appear as “destroyed” in the scoreboard
2. An opponent pushed the key carrier violently into the abyss or a deadly liquid which destroyed the key. This awards the attacking team some points. This will be counted under “pushes” in the scoreboard

Finally, you can drop a key by pressing the “Drop flag/key” control. It's [F] by default.

Scoring
-------

In Key Hunt, the score depends on the number of teams in the game. As of 0.8.2, the scoring (by default) is as follows:

| Action                                | 4 teams       | 3 teams | 2 teams | Notes                                              |
|:-------------------------------------:|:-------------:|:-------:|:-------:|:--------------------------------------------------:|
| Gather all keys                       | +300          | +200    | +100    |                                                    |
| Make enemy team destroy key           | +60           | +60     | +60     | E.g. by pushing key carrier into abyss             |
| Enemy team acidentally destroyed key  | +17 or +16*   | +25     | +50     | Awarded to each team that did *not* lose the round |
| Collect key                           | +3            | +3      | +3      | Only counts if the previous carrier of the key was an enemy |
| Kill enemy key carrier                | +2            | +2      | +2      |                                                    |
| Kill other enemy                      | +1            | +1      | +1      |                                                    |
| Suicide/teamkill                      | -1            | -1      | -1      |                                                    |

\* = This is a known bug in 0.8.2. See [issue #2344](https://gitlab.com/xonotic/xonotic-data.pk3dir/issues/2344)

### Custom scoring

It's possible for servers to change the scoring by setting [CVars](CVars) (`g_balance_keyhunt_score_*`).

Helpful Hints and Tips
----------------------

- Some maps can contain powerups like “[Strength](Powerups#strength)” or “[Shield](Powerups#shield)”. They can be useful tools to win a match!
- When you got a key but you're low on health, it can be useful to give the key to your team mates by dropping it
- [Binds](Binds) are very useful to coordinate the team.
