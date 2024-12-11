# League of Legends: The Impact of Objectives on Game Results
by Samuel Cho (sjc006@ucsd.edu)

---

## Introduction

[League of Legends](https://en.wikipedia.org/wiki/League_of_Legends) is a massively popular multiplayer online battle arena game developed and published by Riot Games. The game currently has millions of active players, which can be largely attributed to its thriving competitive esports scene. Tournaments are held every year where top players compete for substantial prize pools with millions of fans watching worldwide. The dataset I analyzed comes from [Oracle's Elixir](https://oracleselixir.com/tools/downloads), and consists of match data from professional games played in 2022, including extensive statistics on player and team performances, as well as game results.

The objective of the game is to defeat the enemy team by destroying their "Nexus," a structure located their defenses defenses. In order to increase their chances of doing so, teams must take key objectives to gain an advantage over their opponents. One of the most crucial objectives is killing the "Baron," the most powerful monster in League of Legends. The Baron spawns 20 minutes into the game and respawns 6 minues after it has been killed. When a team kills the Baron, they are grated buffs such as increased damaged, ability power, and strengthed allied minions. Consequently, killing the first Baron is often deciding factor in the outcome of the game, making it a top priority for both teams. Therefore, my analysis focuses on the key objectives of League of Legends so that new and aspiring players can better understand the importance of objectives and how they affect the outcome of a game. More specifically, this analysis aims to answer the question: **How impactful is killing the first Baron on the result of the game?**

### Introducing the Dataset

The dataset has a total of 150180 rows and 161 columns. An explanation of the columns relevant to my analysis and are shown below:

| **Column Name** | **Definition** |
| ------------------- | ------------------------------------------------------------ |
| `gameid` | unique identifier for each game |
| `league` | name of professional league that organized tournament |
| `playoffs` | whether or not the game was a playoff game (0 if no, 1 if yes) |
| `side`  | side team was on (Blue or Red) |
| `pick1` | teams first picked champion/character |
| `ban5` | fifth champion team banned |
| `result` | outcome of game (0 if lost, 1 if won) |
| `kills` | total number of kills per team                                   |
| `firstdragon` | whether or not team killed the first dragon (0 if no, 1 if yes) |
| `dragons` | total number of dragons killed per team |
| `firstherald` | whether or not team killed the first herald (0 if no, 1 if yes) |
| `firstbaron` | whether or not team killed the first baron (0 if no, 1 if yes) |
| `barons` | number of barons killed per team|
| `towers` | number of towers broken per team |
| `inhibitors` | number of inhibitors broken per team |

