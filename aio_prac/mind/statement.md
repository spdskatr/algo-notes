# Mind Games

A little known fact about Spud is that despite being nothing more then a personified potato, he is in fact very *psychically sensitive*. In other words, his thoughts can be influenced by devices such as psychic discombobulators. What exactly a psychic discombobulator does is, in fact, irrelevant. What is relevant, however, is that Nim has managed to get her hands on one, and she is going to use it for her own evil purposes!

Spud's thought processes can be modelled as a network of N mind states (numbered from 1 to N), connected by M thought pathways. A mind state X is able to transform into a mind state Y, and vice versa, if there exists a thought pathway from X to Y. Nim, with her psychic discombobulator, can psychically cause Spud's mind state to transform any number of times, as long as during each transformation, the mind states are connected through thought pathways. A *transformation path* from X to Y is a sequence of mind states such that it starts at X, ends at Y, each mind state appears at most once, and each adjacent pair of mind states is connected by a thought pathway.

Nim has Q start and end points for transformation paths that she is considering. She would like to know, for each start and end point, the number of *unavoidable states*. An unavoidable state from X to Y is defined as a mind state that exists in every possible valid transformation path from X to Y. Write up a computer program to help Nim with her problem.

## Input

The first line of input contains three integers, $N$, $M$ and $Q$.

The next $M$ lines contain two integers each. The $i$-th of these lines contains the integers $a_i$ and $b_i$, indicating that the $i$-th transformation path connects the mind states $a_i$ and $b_i$. You are guaranteed that there is at most 1 thought pathway between any two mind states, and no thought pathway connects a mind state to itself.

The next Q lines contain two integers each. The $i$-th of these lines contains the integers $x_i$ and $y_i$, indicating that Nim wants you to count the number of unavoidable states from $x_i$ to $y_i$ for the $i$-th query. It is guaranteed that $x_i$ != $y_i$.

## Output

Output Q lines. The $i​$-th line should contain the number of unavoidable states from $x_i​$ to $y_i​$.

### Sample Input 1

```
6 6 3
1 2
2 3
3 4
1 4
4 5
5 6
1 3
2 5
4 6
```

### Sample Output 1

```
2
3
4
```

### Explanation

In the first query, there are two possible transformation paths: 1 2 3 and 1 4 3. States 1 and 3 are therefore unavoidable.

In the second query, there are two possible transformation paths: 2 3 4 5 and 2 1 4 5. States 2, 4 and 5 are therefore unavoidable.

In the third query, there is only one possible transformation path: 4 5 6. All three states are therefore unavoidable.

## Subtasks and Constraints

For all subtasks, $2 \le N, M \le 200000$, $1 \le Q \le 100000​$.

For subtask 1 (5 pts), $N, M \le 8$, $Q = 1$.

For subtask 2 (35 pts), $N, M, Q \le 1000​$.

For subtask 3 (35 pts), $N, M \le 1000$.

For subtask 4 (25 pts), no further constraints.
