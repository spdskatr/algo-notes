# Problem Set: Binary Search

*Note: These problems don't have modules or test cases, they are purely here for mental solving. Have fun!*

## Part 1

| Time     | Memory |
| -------- | ------ |
| 1 second | 256MB  |

Tennis Ball is exploring an abandoned museum in Yoyle City. The museum consists of N floors, numbered from 1 to N. The i-th floor stores i artifacts. He is interested in investigating the advanced ancient technology rumoured to be hidden inside.

As Tennis Ball knows nothing about the artifacts inside each floor, and the 20000-year-old holographic information kiosk has run out of exotic matter (rendering it useless), he predicts that the probability that an artifact has a *technology level* equal to k is roughly (1/2)^k. That is, half of the artifacts have technology level 0, a quarter have technology level 1, an eighth have technology level 2 and so on. 

Tennis Ball wants to collect at least p artifacts with technology level at least t. He doesn't want to run up too many flights of stairs (the elevators are broken) or run across too many floors, so he will only go to the minimum floor possible such that the expected number of artifacts on that floor with technology level at least t is greater than or equal to p. Given N, p and t, help Tennis Ball calculate this floor.

### Subtasks + Constraints

For all subtasks, 1 <= N <= 10^18, 1 <= p <= 10^18, 1 <= t <= 60

You are guaranteed that such a floor always exists.

For subtask 1 (20 pts), t = 1

For subtask 2 (30 pts), p = 1.

For subtask 3 (50 pts), no further constraints.

## Part 2

| Time     | Memory |
| -------- | ------ |
| 1 second | 256MB  |

Tennis Ball has arrived on the 15,616,011,011,279th floor. He has found N exhibits that catch his interest. The i-th of these exhibits has technology level t_i and volume v_i. Considering, being on the 15,616,011,011,279th floor, he is now roughly 0.68 light-years away from the surface of the Earth, Tennis Ball only wants to make 1 trip. He has a trolley that can hold up to C units of volume, and wants to take the artifacts that will optimise the sum of all the technology levels of the artifacts he takes back. Since he doesn't want to be taking back boring stone-age technology, he also wants to avoid taking artifacts with low technology levels.

Given the number of artifacts, and the technology level and volume of each, Help Tennis Ball maximise the sum of the technology levels of the artifacts he finds, while also maximising the lowest level artifact in the set of items Tennis Ball takes. Output both these values.

### Subtasks + Constraints

1 <= N <= 2000

1 <= t_i, v_1 <= 2000

1 <=  C <= 2000

You will receive 40% of the points if you answer the maximum sum of technology levels correctly, even if you do not answer the second question correctly.

## Part 3

