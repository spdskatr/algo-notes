# Problem - Woody's Poem

*Note: These problems don't have modules or test cases, they are purely here for mental solving. Have fun!*

## Part 1
| Time | Memory |
| --- | --- |
| 1 second | 256MB |

After last time surviving being booted 400 metres into the air and landing on his face, Woody has once again fallen hopelessly in love with Pin. This time, he wants to impress Pin by writing her a love poem consisting only of the letters P, I and N. The poem `p` will be `N` characters in length, and doesn’t have any spaces or line breaks. As he wants to collect statistics for his poem, he asks you to calculate the number of times Pin appears in the poem, that is, the number of times a letter P appears before a letter I which appears before a letter N. In other words, calculate the total number (modulo 1000000007) of `(i, j, k)` where `i < j < k` and `p[i] == ‘P’`, `p[j] == ‘I’` and `p[k] == ‘N’`.

### Subtasks + Constraints

For subtask 1 (10 pts), N <= 200.

For subtask 2 (40 pts), N <= 3000.

For subtask 3 (50 pts), N <= 300000.

### Input format

First line of input will contain N, the number of characters. Second line will contain the N uppercase characters of the poem, each of which is either P, I or N.

```
10
PNIINPPINN
```

### Output format

The first and only line of output should contain a single integer, the number of times Pin appears in the poem, modulo 1000000007.

```
12
```

## Part 2

| Time | Memory |
| --- | --- |
| 1 second | 1GB |

Woody has heard from Tennis Ball that Pin has a favourite number `K`. However, neither Tennis Ball nor Woody knows what her favourite number actually is. Woody is planning on asking Pin's best friend Coiny in the evening. To prepare, he wants you to write a program that outputs the shortest length poem where Pin appears in the poem exactly `K` times.

### Subtasks and Constraints

For Subtask 1 (30 pts), K <= 40.

For Subtask 2 (65 pts), K <= 200.

For Subtask 3 (5 pts), K <= 1000.

### Input format

The first and only line of input will contain K, Pin's favourite number.

```
13
```

### Output format

The first and only line of output should contain the shortest possible poem where Pin appears 

exactly K times. If there are multiple optimal solutions, output any one of them.

```
PPIPININ
```

## Part 3

| Time | Memory |
| --- | --- |
| 3 seconds | 1GB |

**TWO-STEP TASK**

Woody was told by Golf Ball that Pin had left with Needle today to pick yoyleberries for Leafy's cake, and wouldn't return until morning. Seeing as Woody had nothing to do for the rest of the evening, she gave Woody a challenge - turn a message of length `N` into a poem where Pin appears exactly `N` times, such that the message can be decoded from the poem. She asked Woody to implement the functions:

```cpp
void encode(const string &msg, string &poem);

void decode(const string &poem, string &msg);
```

The function `encode` should read in the message `msg` as a parameter and output a valid poem where Pin appears exactly K times. The function `decode` should read in the message `msg` as a parameter and output the original message. No global variables can be shared between the two functions - two different instances of your program will be run to encode and decode messages. Both functions will be called at most 10 times per test case.

### Subtasks + Constraints

For all test cases, `N <= 1000`

### Scoring

Let L be the length of your poem. 

For each test case, you will score:

- 0% if your poem is invalid or if Pin does not appear exactly K times or if `L > 1000*N`
- 20% if `L <= 1000*N`
- 40% if `L <= 100*N`
- On a sliding scale between 40% and 100%, if `10*N < L <= 50*N`
- 100% if `L <= 10*N`

The score for this task will be the average score for each test case.

