# lokesh pentyala
###### goa 
i love **beaches** and it has a lot of beaches and the **sunset** is lovely to watch

************************************
# directions to times square newyork
1. bus to kansas from maryville
2. flight to new york
3. bus to times square via Grand Central Parkway

#  unordered list
* camera
* shorts 
* t-shirts

***Link to About me***
<https://github.com/lokesh62/assignment2-pentyala/blob/main/Aboutme.md.txt>

***************************************

# FOOD AND DRINKS!!
This table shows you the food and drinks that you should try at **MARYVILLE**

|food/drinks | Location | Amount |
| ---        | ---      | ---    |
| meatballs  | subway   | $6     |
| icecream   | K&K      | $4     |
| wings      | kfc      | $8     |
| sandwich   | Bagels   | $7     |

**********************
# quotes
>As you think, so shall you become.

*Bruce Lee*

>Where there is love there is life.

*Mahatma Gandhi*

**********************
# code fencing

>In graph theory and computer science, the lowest common ancestor (LCA) of two nodes v and w in a tree or directed acyclic graph (DAG) T is the lowest (i.e. deepest) node that has both v and w as descendants, where we define each node to be a descendant of itself (so if v has a direct connection from w, w is the lowest common ancestor).

<https://en.wikipedia.org/wiki/Lowest_common_ancestor>
```
struct LCA {
    vector<int> height, euler, first, segtree;
    vector<bool> visited;
    int n;

    LCA(vector<vector<int>> &adj, int root = 0) {
        n = adj.size();
        height.resize(n);
        first.resize(n);
        euler.reserve(n * 2);
        visited.assign(n, false);
        dfs(adj, root);
        int m = euler.size();
        segtree.resize(m * 4);
        build(1, 0, m - 1);
    }

    void dfs(vector<vector<int>> &adj, int node, int h = 0) {
        visited[node] = true;
        height[node] = h;
        first[node] = euler.size();
        euler.push_back(node);
        for (auto to : adj[node]) {
            if (!visited[to]) {
                dfs(adj, to, h + 1);
                euler.push_back(node);
            }
        }
    }

    void build(int node, int b, int e) {
        if (b == e) {
            segtree[node] = euler[b];
        } else {
            int mid = (b + e) / 2;
            build(node << 1, b, mid);
            build(node << 1 | 1, mid + 1, e);
            int l = segtree[node << 1], r = segtree[node << 1 | 1];
            segtree[node] = (height[l] < height[r]) ? l : r;
        }
    }

    int query(int node, int b, int e, int L, int R) {
        if (b > R || e < L)
            return -1;
        if (b >= L && e <= R)
            return segtree[node];
        int mid = (b + e) >> 1;

        int left = query(node << 1, b, mid, L, R);
        int right = query(node << 1 | 1, mid + 1, e, L, R);
        if (left == -1) return right;
        if (right == -1) return left;
        return height[left] < height[right] ? left : right;
    }

    int lca(int u, int v) {
        int left = first[u], right = first[v];
        if (left > right)
            swap(left, right);
        return query(1, 0, euler.size() - 1, left, right);
    }
};
```
   

