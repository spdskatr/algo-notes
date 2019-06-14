# Algorithms Notes (The Appendix)

Subsections are in no particular order. Obviously a hash table data structure would be the best way to go, but `std::unordered_map` doesn't even work on orac lmao

## General

### Binary Search (The Superior) Algorithm

Maximises x for which decision(x) is true given that decision is a monotonic decision problem

```cpp
int lo = 0, hi = MAX + 1;
while (lo + 1 < hi) {
    int mid = (lo + hi) / 2;
    if (decision(mid)) lo = mid;
    else hi = mid;
}
// Answer is stored in lo
```

## Euclidean Algorithm

Standard vanilla Euclidean algorithm.

```cpp
int gcd(int x, int y) {
	while (y != 0) {
		int temp = y;
		y = x%temp;
		x = temp;
	}
	return x;
}
```

## Graph Theory

### DFS!

#### Articulation Points

```cpp
int N, seen[MAX_N], in[MAX_N], val[MAX_N], cp[MAX_N], c;
vector<int> adj[MAX_N];

void dfs(int x, int par) {
    seen[x] = 1;
    val[x] = in[x] = c++;
    int ch = 0;
    for (int v : adj[x]) {
        if (par == v) continue;
        if (seen[v]) val[x] = min(val[x], in[v]);
        else {
            dfs(v, x);
            val[x] = min(val[x], val[v]);
            if (val[v] >= in[x] && par != -1) cp[x] = 1;
            ch++;
        }
    }
    if (par == -1 && ch > 1) cp[x] = 1;
}
```

#### Topological Sort

##### Kahn's algorithm

```cpp
vector<int> graph[MAX_V], S, top_sort;
int deps[MAX_V];
for (int i = 1; i <= V; i++) {
    for (int j = 0; j < graph[i].size(); j++) {
        deps[graph[i][j]]++;
    }
}
for (int i = 1; i <= V: i++) if (deps[i] == 0) S.push_back(i);
while (!S.empty()) {
    int u = s.back(); s.pop_back();
      top_sort.push_back(u);
    for (int i = 0; i < graph[u].size(); i++) {
        if (--deps[graph[u][i]] == 0) S.push_back(graph[u][i]);
    }
}
if (top_sort.size() != V) assert(false && "Graph contains cycle");
```

##### DFS Topological Sort

```cpp
vector<int> graph[MAX_V], top_sort;
int state[MAX_V];

void dfs(int x) {
    if (state[x] == 2) return;
    if (state[x] == 1) assert(false && "Graph contains cycle");
    state[x] = 1;
    for (int i = 0; i < graph[x].size(); i++) dfs(graph[x][i]);
    state[x] = 2;
    top_sort.push_back(x);
}

for (int i = 1; i <= V; i++) dfs(i);

reverse(top_sort.begin(). top_sort.end());
```

### Disjoint Set Union (affectionately named Union-Find)

With path compression
```cpp
int uf[MAX_V];
void ms(int x) { uf[x] = x; }
int f(int x) { if (uf[x] == x) return x; return uf[x] = f(uf[x]); }
void u(int x, int y) { uf[f(x)] = f(y); }
```

### Kruskal&apos;s algorithm for Minimum Spanning Tree

Uses Union-Find (I prefer Kruskal's because it's the fastest one I can code up)
```cpp
pair<int, int> edges[MAX_E];
// order edges by weight ascending
for (int i = 1; i <= V; i++) ms(i);
for (int i = 0; i < E; i++) {
    if (f(edges[i].first) != f(edges[i].second)) {
        // Add edges[i] to minumum spanning tree
        u(edges[i].first, edges[i].second);
    }
}
```

### Maximum Bipartite Matching in O(VE)

Ford-Fulkerson algorithm (Max flow) used for O(VE) max bipartite matching

```cpp
// Graph stores edge ids for directed edges
// Each directed edge e u -> v has to[e] = v and act[e] = 1 if 1 in residual graph
// A+B+1 is the sink node
int dfs(int x, vector<int> &path) {
    if (x == A+B+1) return 1;
    for (int i = 0; i < graph[x].size(); i++) if (act[graph[x][i]] && !seen[to[graph[x][i]]]) {
        seen[to[graph[x][i]]] = 1; // ?
        if (dfs(to[graph[x][i]], path)) {
            path.push_back(graph[x][i]);
            return 1;
        }
    }
    return 0;
}

int max_flow(int s, int t) {
    int ans = 0;
    while (1) {
        vector<int> path;
        memset(seen, 0, sizeof(seen));
        int r = dfs(s, path);
        if (!r) break;
        for (int i = 0; i < path.size(); i++) {
            act[path[i]] ^= 1;
            act[path[i]^1] ^= 1;
        }
        ans++;
    }
    return ans;
}
```

### Least Common Ancestor

Jump pointers for O(log n) online

```cpp
void dfs(int x, int par) {
    tin[x] = c++;
    jp[x][0] = par;
    for (int i = 0; i < graph[x].size(); i++) 
        if (graph[x][i].S != par) {
            dfs(graph[x][i].S, x);
        }
    tout[x] = c++;
}

// Precalc
dfs(1, 1);
for (int i = 1; i < 17; i++) {
    for (int j = 1; j <= N; j++) {
        jp[j][i] = jp[jp[j][i-1]][i-1];
    }
}

int isanc(int u, int v) {
    return tin[u] <= tin[v] && tout[u] >= tout[v];
}

int lca(int a, int b) {
    int res = -2069696969;
    if (isanc(a, b)) return a;
    if (isanc(b, a)) return b;
    for (int i = 16; i >= 0; i--) {
        if (!isanc(jp[a][i], b)) a = jp[a][i];
    }
    return jp[a][0];
}
```

### Shortest Path Problem

#### Dijkstra&apos;s algorithm
O(E log V)

```cpp
typedef pair<int, int> ENTRY;
typedef pair<int, int> EDGE;
vector<EDGE> graph[MAX_V];
int dists[MAX_V], seen[MAX_V];

priority_queue<ENTRY, vector<ENTRY>, greater<ENTRY>> pq;

// Algorithm
for (int i = 0; i < MAX_V; i++) dists[i] = INF;
dists[source] = 0;

pq.push({ dists[source], source });
while (!pq.empty()) {
    ENTRY e = pq.top();
    pq.pop();
    int u = e.second;
    if (seen[u]) continue;
    seen[u] = 1;
    for (int i = 0; i < graph[u].size(); i++) {
        int v = graph[u][i].first;
        int w = graph[u][i].second;
        if (dists[u] + w < dists[v]) {
            dists[v] = dists[u] + w;
            pq.push({ dists[v], v });
        }
    }
}
```

#### Bellman-Ford Algorithm
O(VE)

```cpp
pair<int, pair<int, int> > EDGE_STRUCT;
EDGE_STRUST edges[MAX_E];
// Algorithm
for (int i = 1; i <= V; i++) dists[i] = INF;
dists[source] = 0;

for (int i = 0; i < V - 1; i++) {
    for (int j = 0; j < E; j++) {
        int w = edges[j].first;
        int u = edges[j].second.first;
        int v = edges[j].second.second;
        if (dists[u] + w < dists[v]) {
            dists[v] = dists[u] + v;
        }
    }
}

// Check for negative weight cycles
for (int i = 0; i < E; i++) {
    int w = edges[i].first;
    int u = edges[i].second.first;
    int v = edges[i].second.second;
    if (dists[u] + w < dists[v]) {
        // Graph contains negative-weight cycle
    }
}
```

#### Floyd-Warshall Algorithm

O(V^3) all pairs shortest paths

```cpp
// Init distance matrix
memset(dists, 0x3f, sizeof(dists));
for (int i = 0; i < V; i++) dists[i][i] = 0;
for (int i = 0; i < E; i++) dists[a[i]][b[i]] = dists[b[i]][a[i]] = w[i];

for (int mid = 0; mid < V; mid++)
    for (int u = 0; u < V; u++)
        for (int v = 0; v < V; v++) 
            dists[u][v] = min(dists[u][v], dists[u][mid] + dists[mid][v]);
```



## Ranges and Trees

### Prefix sum

1. O(1) range increment

```
for 2d prefix sum, to change a range [x1, x2], [y1, y2] by x

change x1,     y1     by x
change x1,     y2 + 1 by -x
change x2 + 1, y1     by -x
change x2 + 1, y2 + 1 by -x

for 3d prefix sum, to change a range [x1, x2], [y1, y2], [z1, z2] by x

change x1,     y1,     z1     by x
change x1,     y1,     z2 + 1 by -x
change x1,     y2 + 1, z1     by -x
change x2 + 1, y1,     z1     by -x
change x1,     y2 + 1, z2 + 1 by x
change x2 + 1, y1,     z2 + 1 by x
change x2 + 1, y2 + 1, z1     by x
change x2 + 1, y2 + 1, z2 + 1 by -x
```

2. O(1) Range sum of a rectangle [x1, x2], [y1, y2]

```cpp
int rect(int x1, int x2, int y1, int y2) {
    return ps[x2][y2] - ps[x1 - 1][y2] - ps[x2][y1 - 1] + ps[x1 - 1][y1 - 1];
}
```

3. O(1) range sum of a rectangular prism [x1, x2], [y1, y2], [z1, z2]

```cpp
int prism(int x1, int x2, int y1, int y2, int z1, int z2) {
    return ps[x2][y2][z2]
           - ps[x2][y2][z1 - 1] - ps[x2][y1 - 1][z2] - ps[x1 - 1][y2][z2]
           + ps[x2][y1 - 1][z1 - 1] + ps[x1 - 1][y2][z1 - 1] + ps[x1 - 1][y1 - 1][z2]
           - ps[x1 - 1][y1 - 1][z1 - 1];
}
```

#### Fenwick Tree (Binary Indexed Tree)

Note: Fenwick trees can also be used for O(log n) range update and O(log n) point query by making a tree of the difference array

```cpp
int ft[SIZE];
int lsb(int x) { return x & -x; }
int fps(int i) {
    int ans;
    for (ans = 0; i > 0; i -= lsb(i)) ans += ft[i];
    return ans;
}
void finc(int i, int x) {
    for (; i < SIZE; i += lsb(i)) ft[i] += x;
}
```

### Self-balancing Binary Search Tree

In C++, SBBSTs are implemented as `std::set` and `std::map`.  They can be used for a bunch of different things, some of which speed up implementation a lot

#### Actually implementing a SBBST, featuring Treap

The primary method for balancing BSTs is to use a technique called rotation. Rotating a binary search tree essentially changes the root of the tree to any node you want. There are 2 types of rotation operations:

```python
# Pseudocode for left rotate - makes right child the new root
def left_rotate(root):
    new_right = root->right->left
    old_right = root->right
    root->right = new_right
    old_right->left = root
    root.update_invariant()
    old_right.update_invariant()
    return old_right
   
# Pseudocode for right rotate - makes left child the new root
def right_rotate(root):
    new_left = root->left->right
    old_left = root->left
    root->left = new_left
    old_left->right = root
    root.update_invariant()
    old_left.update_invariant()
    return old_left
```

A Treap with random values as the keys can also be called a randomised binary search tree and runs in **expected O(log n)**. The idea is to maintain a BST with respect to the keys and a heap with respect to the values. Treaps rely on 2 utility functions, merge and split.

```python
# Pseudocode for merge operation on 2 subtreaps
def merge(root1, root2):
    if root1 does not exist: return root2
    if root2 does not exist: return root1
    if root1.value > root2.value:
        root1->right = merge(root1->right, root2)
        root1.update_invariant()
        return root1
    else:
        root2->left = merge(root1, root2->left)
        root2.update_invariant()
        return root2

# Pseudocode for split at point x operation for 2 subtreaps
def split(root, x, &l, &r):
    if root does not exist: l = r = null
    if x < root.key:
        split(root->left, x, l, root->left)
        r = root
    else:
        split(root->right, x, root->right, r)
        l = root
    root.update_invariant()
```



#### _\_gnu\_pbds::tree

The GNU Policy Based Data Structures library implements SBBSTs with augmentation capabilities. I'm pretty sure you won't need to know how to augment crap like this but i'll show you how to invoke the already provided order statistic tree.

```cpp
#include <ext/pb_ds/assoc_container.hpp>
#include <ext/pb_ds/tree_policy.hpp>
using namespace __gnu_pbds;

typedef tree<int, null_type, less<int>, rb_tree_tag, tree_order_statistics_node_update> OS;

OS set1;

// Functionality identical to std::set except for 2 added methods:
// find_by_order(k): returns iterator to element at index k
// order_of_key(n): returns number of items strictly less than n
set1.insert(2);
set1.find_by_order(0);  // returns iterator to element with value 2
set1.order_of_key(2);   // returns 0
set1.order_of_key(3);   // returns 1
```



### Segment Tree

A data structure that supports all O(log n) range and point queries (i.e. point access, point update, range min, range update) Has O(N) space complexity.

As long as combiner function maintains *associativity*, it can be used in a segment tree i.e. $\forall a, b, c \in S,f(a, f(b, c)) = f(f(a, b), c)$

1. Point query/update

```cpp
int seg_q(int lo, int hi, int i, ind ind) {
    // If using lazy propagation
    lu(ind);
    if (lo > i || hi <= i) return -INF;
    if (lo + 1 == hi) return st[ind];
    int mid = (lo + hi) / 2;
    return max(seg_q(lo, mid, i, ind * 2 + 1), seg_q(mid, hi, i, ind * 2 + 2));
}
void seg_set(int lo, int hi, int i, int val, int ind) {
    // If using lazy propagation
    lu(ind);
    if (lo > i || hi <= i) return;
    if (lo + 1 == hi) {
        st[ind] = val;
        return;
    }
    int mid = (lo + hi) / 2;
    seg_set(lo, mid, i, val, ind * 2 + 1);
    seg_set(mid, hi, i, val, ind * 2 + 2);
    // Combiner function here
    st[ind] = max(st[ind*2+1], st[ind*2+2]);
}
```

2. RMQ (here using max as an example, other combiner functions should work as well)

```cpp
int seg_max(int lo, int hi, int left, int right, int ind) {
    // If using lazy propagation
    lu(ind);
    if (hi <= left || lo >= right) return -INF;
    if (hi <= right && lo >= left) return st[ind];
    int mid = (lo + hi) / 2;
    return max(seg_max(lo, mid, left, right, ind * 2 + 1),
               seg_max(mid, hi, left, right, ind * 2 + 2));
}
```

3. Lazy Propagation

```cpp
int lu(int ind) {
    if (lazy[ind] > 0) {
        // Update
        st[ind] = lazy[ind];
        // Propagate to children
        lazy[ind * 2 + 1] = lazy[ind];
        lazy[ind * 2 + 2] = lazy[ind];
        // Reset self
        lazy[ind] = 0;
    }
}

void rset(int lo, int hi, int left, int right, int ind, int val) {
    lu(ind);
    if (hi <= left || lo >= right) return;
    if (hi <= right && lo >= left) {
        st[ind] = val;
        lazy[ind * 2 + 1] = val;
        lazy[ind * 2 + 2] = val;
        return;
    }
    int mid = (lo + hi) / 2;
    rset(lo, mid, left, right, ind * 2 + 1, val);
    rset(mid, hi, left, right, ind * 2 + 2, val);
    st[ind] = max(st[ind * 2 + 1], st[ind * 2 + 2]);
}
```

#### The Iterative Segment Tree Starter Pack

```cpp
void cons() { for (int i = N-1; i > 0; i--) st[i] = max(st[i<<1], st[i<<1|1]); }
void seg_set(int i, int v) { for (st[i += N] = v; i > 1; i >>= 1) st[i>>1] = max(st[i], st[i^1]); }
int seg_min(int l, int r) {
    int res = -INF;
    for (l += N, r += N; l < r; l >>= 1, r >>= 1) {
        if (l&1) res = max(res, st[l++]);
        if (r&1) res = max(res, st[--r]);
    }
    return res;
}
```

### Sparse Table

O(n log n) memory, O(1) range query, (bad update)

Functions can be used in sparse tables if they are *associative* (see segment tree) and *idempotent* i.e. $f(a, f(a, b)) = f(a, b)$

```cpp
int sparse_table[100005][20];
for (int i = 1; i <= N; i++) {
    sparse_table[i][0] = arr[i];
}
for (int e = 1; e < 20; e++) {
    for (int i = 1; i <= N + 1 - (1 << (e-1)); i++) {
        sparse_table[i][e] = max(sparse_table[i][e-1], sparse_table[i+(1<<(e-1))][e-1]);
    }
}
int range_max(int left, int right) {
    long double x = right - left;
    int k = (int)floor(log2l(x));
    return max(sparse_table[left][k], sparse_table[right-(1<<k)][k]);
}
```

