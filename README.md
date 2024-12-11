# League of Legends: The Impact of Objectives on Game Results
by Samuel Cho (sjc006@ucsd.edu)

---

## Introduction

[League of Legends](https://en.wikipedia.org/wiki/League_of_Legends) is a massively popular multiplayer online battle arena game developed and published by Riot Games. The game currently has millions of active players, which can be largely attributed to its thriving competitive esports scene. Tournaments are held every year where top players compete for substantial prize pools with millions of fans watching worldwide. The dataset I analyzed comes from [Oracle's Elixir](https://oracleselixir.com/tools/downloads), and consists of match data from professional games played in 2022, including extensive statistics on player and team performances, as well as game results.

League of Legends is a 5 versus 5 player game split into three lanes, where the objective of is to defeat the enemy team by destroying their "Nexus," a structure located behind enemy defenses. In order to increase the chances of doing so, teams must take key objectives to gain an advantage over their opponents. One of the most crucial objectives is killing the "Baron," the most powerful monster in League of Legends. The Baron spawns 20 minutes into the game and respawns 6 minues after it has been killed. When a team kills the Baron, they are granted buffs such as increased damaged, ability power, and strengthed allied minions. Consequently, killing the first Baron is often a deciding factor in the outcome of the game, making it a top priority for both teams. Therefore, my analysis focuses on the key objectives of League of Legends so that new and aspiring players can better understand the importance of objectives and how they affect the outcome of a game. More specifically, this analysis aims to answer the question: **How impactful is killing the first Baron on the result of the game?**

### Introducing the Dataset

The dataset has a total of 150180 rows and 161 columns. For each match, there are ten rows for each of the ten individual players and two rows for each of the two teams. An explanation of the columns relevant to my analysis and are shown below:

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
| `firstdragon` | whether or not team killed the first dragon, monsters that give small buffs when killed (0 if no, 1 if yes) |
| `dragons` | total number of dragons killed per team |
| `firstherald` | whether or not team killed the first herald, a monster captured after killed and redeployable to break towers (0 if no, 1 if yes) |
| `firstbaron` | whether or not team killed the first baron (0 if no, 1 if yes) |
| `barons` | number of barons killed per team|
| `towers` | number of towers broken per team. towers are breakable structures that defend Nexus, |
| `inhibitors` | number of inhibitors broken per team. inhibitors are breakable structure that spawns buffed minions in the lane in which it was broken |

---

## Data Cleaning and Exploratory Data Analysis

### Data Cleaning

The dataset The first step in cleaning the dataset was dropping the columns pertaining to players, rather than teams. This is because my analysis focuses on which teams won and what objectives they took. Next, I looked at the `datacompleteness` column and found that rows with values of `partial` for `datacompleteness` were missing values for the columns `firstdragon`, `dragons`, `firstherald`, `firstbaron`, `barons`, `towers`, `inhibitors`, which are all relevant to my analysis. As a result, I dropped the rows where `datacompletness` is `partial`, leaving me with only rows where `datacompletness` is `complete`. Then I kept only the rows relevant to my analysis: `gameid`, `side`, `result`, `kills`,	`firstdragon`,	`dragons`, `firstherald`, `firstbaron`, `barons`, `towers`,	`inhibitors`. Finally, I converted the binary columns to booleans, where values of 0 correspond to False and values of 0 correspond to True.

The head of the cleaned DataFrame is below:

| gameid                | side   | result   |   kills | firstdragon   |   dragons | firstherald   | firstbaron   |   barons |   towers |   inhibitors |
|:----------------------|:-------|:---------|--------:|:--------------|----------:|:--------------|:-------------|---------:|---------:|-------------:|
| ESPORTSTMNT01_2690210 | Blue   | False    |       9 | False         |         1 | True          | False        |        0 |        3 |            0 |
| ESPORTSTMNT01_2690210 | Red    | True     |      19 | True          |         3 | False         | False        |        0 |        6 |            1 |
| ESPORTSTMNT01_2690219 | Blue   | False    |       3 | False         |         1 | True          | False        |        0 |        3 |            0 |
| ESPORTSTMNT01_2690219 | Red    | True     |      16 | True          |         4 | False         | True         |        2 |       11 |            2 |
| ESPORTSTMNT01_2690227 | Blue   | True     |      14 | True          |         4 | False         | True         |        1 |       11 |            2 |

### Univariate Analysis

For my univariate analysis, I decided to look at the distributions of different objectives to get a better understanding of the amount of objectives taken by team per game.

First I plotted a histogram of the distribution of Barons killed.

<iframe
  src="assets/fig-baron-kills.html"
  width="800"
  height="430"
  frameborder="0"
></iframe>

This histogram is right skewed and shows that zero and one were the most common number of barons killed. This makes sense as the majority of the time, a team either kills no barons and loses or kills one baron and wins shortly after, making it less common for more than one baron to be killed a game.

Then I plotted a histogram of the distribution of dragons killed. Killing dragons is another objective where similar to Baron's, provides the team that kills a dragon small buffs such as increased damage or armor.

<iframe
  src="assets/fig-dragon-kills.html"
  width="800"
  height="430"
  frameborder="0"
></iframe>

The histogram is slightly normal and right skewed, showing that the most common number of dragons killed ranges from one to four. This is reasonable as dragons are an objective that spawn more frequently and do not give as significant of a buff as Barons, meaning more are killed a game.

I also plotted the distribution of towers broken. Towers are powerful structures that protect the Nexus. Layers of towers must be broken in order to be able to reach and destroy the Nexus.

<iframe
  src="assets/fig-towers-broken.html"
  width="800"
  height="430"
  frameborder="0"
></iframe>

The plot follows a bimodal distribution as there are two distinct peaks. This is most likely due to the fact that losing teams are likely to break from a range of one to five turrets a game (first peak) while winning teams are likely to break from a range of 8 to 11 towers a game (second peak).

Lastly, I plotted the distribution of inhibitors broken. Inhibitors are another very important objective. There is one inhibitor for each of the three lanes, located closer to the Nexus. Breaking an inhibitor causes "Super Minions," which are far stronger than regular minions, to spawn in the lane in which the inhibitor was broken.

<iframe
  src="assets/fig-inhibitors-broken.html"
  width="800"
  height="430"
  frameborder="0"
></iframe>

The histogram is right skewed, similar to the distribution of Baron kills. Zero inhibitors broken is the most common because losing teams most often break no inhibitors at all, while winning teams break at least one, which can be seen in the plot as the height of bar corresponding to zero inhibitors broken is approximately the same height as the bars for one and 2 inhibitors broken, which correspond to winning teams.

### Bivariate Analysis

For my bivariate analysis, I decided to create visualizations to show how different objectives affects different statistics related to the game result.

I plotted a grouped bar plot of the distribution of teams that won or lost based on whether or not the first baron was killed.

<iframe
  src="assets/fig-firstbaron-result.html"
  width="800"
  height="430"
  frameborder="0"
></iframe>

The plot clearly shows that teams that killed the first baron won more times than lost. Consequently, the teams that did not kill the first baron lost more times than won.

Next, I plotted the distribution of the number of kills per team based on whether or not the first baron was killed.

<iframe
  src="assets/fig-firstbaron-kills.html"
  width="800"
  height="430"
  frameborder="0"
></iframe>

As expected, the plot shows that teams that killed the first baron had a higher average number of kills. This aligns with the fact that Baron provides teams with buffs that make it easier to win fights.

Similarly, I plotted the distribution of the number of kills per team based on the number of towers broken.

<iframe
  src="assets/fig-tower-kills.html"
  width="800"
  height="430"
  frameborder="0"
></iframe>

There is a clear increase in the number of kills as the number of towers broken increases. This is consistent with the fact that the more kills a team has, the more towers they can break as enemies would not be able to defend them while waiting to respawn.

### Interesting Aggregates

| result   |   barons |   dragons |   firstbaron |   firstdragon |   firstherald |   inhibitors |   kills |   towers |
|:---------|---------:|----------:|-------------:|--------------:|--------------:|-------------:|--------:|---------:|
| False    |  0.22331 |   1.44926 |     0.142629 |      0.422802 |      0.417059 |     0.118528 |  9.4759 |  2.86095 |
| True     |  1.127   |   3.04406 |     0.804745 |      0.57701  |      0.582659 |     1.75108  | 19.7113 |  9.24572 |

This pivot table is indexed by the `result` and has the averages of the columns `dragons`, `barons`, `towers`, `inhibitors`, `firstdragon`, `firstherald`, `firstbaron`. The columns `firstbaron`, `firstdragon`, and `firstherald` show that 80% of teams that killed the first baron won the game and 58% of teams that killed the first dragon or killed the first herald won the game. Although these winrates are all positive for teams that are the first to kill monster objectives, the winrate for `firstbaron` is much higher, indicating that is the most important and game changing monster objective. Also note that teams that lose, on average, kill close to zero Barons and break close to zero inhibitors. On the other hand, `dragons` shows that losing teams kill at least 1 dragon on average, which suggests that killing one dragon is not as significant as killing one baron. Additionally, the `towers` column shows that winning teams break far more towers than losing teams, with an approximate difference of 6.39 on average.


## Assessment of Missingness

### NMAR Analysis

I believe that the column `ban5` is NMAR, or not missing at random, because there seems to be no apparent trend or association with any other columns. Therefore, the missingness of the `ban5` column depends on the value of `ban5` itself. What this means is that `ban5` could be missing because a team either purposely chose to not ban a fifth champion, or they simply forgot to. An additonal column, `prefer_to_ban`, for example, can be obtained which is True for teams that prefer banning champions and False for teams that do not prefer banning champions. This would make `ban5` MAR on `prefer_to_ban`, instead of NMAR.

### Missing Dependency

In the original dataset, I found that missingness of column `pick1` seemed to 