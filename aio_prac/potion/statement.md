# Potion

In his secret underground lab, the eccentric Dr. Yes is conducting yet another crazy science experiment. This time, he is brewing a potion that, when drunk, causes people to understand computational geometry. The ingredients for this potion are actually quite simple - $N$ litres of peach juice mixed with $N​$ litres of garlic juice. However, during brewing, the ratio of peach juice to garlic juice has to be so carefully controlled, that ingredients can only be added 1 litre at a time.

Dr. Yes' recipe for the potion can be described as a series of $2N$ steps, with each step being either to add exactly 1 litre of peach juice, or exactly 1 litre of garlic juice. Dr. Yes tells you that if the potion is brewed correctly, the amount of peach juice in the brew will always be at least as much as the amount of garlic juice at any point in time.

Unfortunately, his arch-nemesis Dr. No has taken his recipe book, and changed exactly one of the steps in his recipe! Dr. Yes wants you to help him recover his original recipe, by telling him the number of possible places that Dr. No could possibly have changed his recipe.

## Input

The first line of input contains the integer $N$, the number of litres of peach and garlic juice in the final potion.

The second line of input contains $2N$ uppercase letters, representing Dr. Yes' recipe. The steps are listed in chronological order, with the letter `P` representing to add 1 litre of peach juice, and the letter `G` representing to add 1 litre of garlic juice.

## Output

You must output a single integer: the number of possible places that Dr. No could possibly have changed Dr. Yes' recipe. If it is not possible, output 0.

### Sample Input 1

```
3
PGGGPG
```

### Sample Output 1

```
2
```

### Explanation

Dr. No could have changed the second step, and the original recipe would be `PPGGPG`.

Dr. No could have changed the third step, and the original recipe would be `PGPGPG`.

Note that Dr. No could not have changed the first or fifth steps, as that would mean that there aren't exactly 3 litres of peach and garlic juice at the end. He could not have changed the fourth of sixth steps either, as that would mean at some points of the original recipe, there would be less peach juice than garlic juice.

## Subtasks and Constraints

For all subtasks, $1 \le N \le 1000000$.

For subtask 1 (30 pts), $N \le 1000$.

For subtask 2 (70 pts), no further constraints.
