# Watering

Global warming is a rather *hot* topic these days, especially for those precious strawberry bushes that have been growing in Bessie's garden. Exposed to the scorching temperatures of the 2019 climate, the bushes have not been doing quite well, and most of them are quite dehydrated. Luckily, Farmer John has installed an elaborate sprinkler system that can provide relief for her dying plants.

Bessie's strawberry garden consists of a long line of $N$ strawberry bushes planted exactly 1 metre apart, with the first bush planted at position 1. Therefore, strawberry bush $i$ would also be planted at position $i$. Farmer John's sprinkler system consists of a long pipe with $M$ different sprinklers at different positions. In particular, the $i$-th hose is at position $x_i$ and has a *range* of $r_i$. A sprinkler with a range of $r$ can water all plants that are within $r$ metres of it in either direction. Given the number of strawberry bushes, and the positions of the sprinklers, determine the total number of Bessie's strawberry bushes that Farmer John can keep alive with his sprinkler system.

## Input

The first line of input contains two integers, $N$ and $M$.

The following $M$ lines contain two integers each. Line $i+1$ contains the integers $x_i$ and $r_i$, describing the position and range of the $i$-th sprinkler. The sprinklers will be given in ascending order of position.

## Output

Output a single integer: the total number of Bessie's strawberry bushes that Farmer John can keep alive with his sprinkler system.

## Subtasks and Constraints

For all subtasks, $N \le 1000000000, M \le 100000$.

For subtask 1 (10 pts), $M = 1$.

For subtask 2 (30 pts), $N, M \le 1000$

For subtask 3 (60 pts), no further constraints.