# AIO: Unofficial editorial

## Intro

This editorial is intended to give you a significant pointer towards solving the problems, such that most people should be able to figure out the details in the implementation of the algorithms. However, some prerequisite knowledge is not included on here (for instance, how graphs are represented in code). 

## Q1: Vases

The minimum number of flowers you need for the 3 vases to be different is 6, because you have to put 1 flower in the first vase, 2 flowers in the second vase, and 3 flowers in the third vase. Any remaining flowers can be put in the third vase, and there will still be a unique number of flowers in each vase.

## Q2: RPS

Win as many games as you can, then try to draw as many games as you can. The remaining games must be lost.

## Q3: Hiring Monks

The observation to make is that to fill up K master jobs, you always want to hire the K monks with the highest skill level. Similarly, to fill up K student jobs, you always want to hire the K monks with the lowest skill level. This will always be optimal (figuring out why is left as an exercise to the reader). 

Sort the monks' skill levels, as well as the professions' skill requirements, then start from the ends of the sorted array to fill up as many master jobs as possible, and then fill up as many student jobs as possible with the remainder. If you manage to fill up all the jobs, then you have the maximum possible.

## Q4: Medusa's snakes

Given a venom level x, it is easy to determine if it is possible to take letters of a given snake's DNA and create a snake with that venom level. Simply take x S letters, followed by x N letters, and so on. In fact this is always produces an optimal solution in O(N) time.

We could simply use this function to check for every possible value of x, and take the maximum in O(N^2) time. However, we can narrow down on the maximum venom level, in an even faster way, by binary searching the answer. This kind of binary search is very special and more generalised than the kind of binary search often first explained in computer science (I will describe it briefly here).

The idea of this generalised binary search is that you have a sequence of numbers that starts with 1, ends with a 0 and changes from 1 to 0 at exactly 1 location. You want to find the location with the fewest number of queries. If you query a location and get a 0, you know that the turning point must be to the left. The reverse is true for getting a 1. Hence, by querying the middle location, you can easily narrow down on the number of possible locations by half and perform binary search on the half you know the turning point is in.

In conclusion, the algorithm is O(N log N).

*Footnote: There is actually a linear time solution for Medusa's snakes, which involves dynamic programming with optimisations. It could be a good solving exercise to find this solution.*

## Q5: Evading Capture

This is a graph theory problem. I won't talk about the implementation details in representing graphs, or the details of the various standard graph algorithms.

The observation for this problem is that you can get from a city A to a city B in K hops if and only if the shortest path from A to B with the same *parity* as x is less than or equal to K. By parity, I mean that if two numbers are both odd or both even, they have the same parity. This is easy to prove, because you can get to a location, and stay there by repeatedly going to an adjacent city and back.

Create an undirected graph, with two nodes per city. Each node stores the city you are at, and also whether you took an odd number of steps to get to the city. To build the graph, if cities A and B are adjacent, then A-odd should connect to B-even and A-even should connect to B-odd.

Perform breadth-first search on the graph to work out shortest paths. Then, for each city, determine from the observation if it is reachable within exactly K steps by checking the relevant nodes.

## Q6: Lollipops, Sweets and Chocolates II

For any given value of R, you are able to determine the number of stores within range of each house, and tally them up in linear time using a two pointers technique. It may seem that this problem is trivially binary-searchable, but upon closer inspection, simply matching the labels of the result with the labels required in the input is not a decision problem we can turn into binary search.

Consider a candidate t for the value of R. Observe that as t increases the sum of all labels increases. We can hence binary search for the value of t that gives the same label sum as the sum of the given labels. Then we check for that t if the labels are exactly the same as required. Note that any group of values for t which have the same sum of labels will have the same labels as each other.
