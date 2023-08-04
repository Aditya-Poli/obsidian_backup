![image](https://assets.leetcode.com/users/images/c34e062c-8e9c-4b89-b711-884be7576a1a_1645851920.0703163.gif)![image](https://assets.leetcode.com/users/images/fcda8541-fcd0-44c6-b65a-324c09c95223_1643608046.9153721.gif)

I can say this is the best Article Ever created over on LeetCode regarding Graph. And this article is inspired from `TakeYouForward` and a lot of thanks to **@striver_79**

---

---

It's not an language specific article. Trust me, you will learn a lot. Right now it's written in **Java** but trust me it will never be a issue.

---

---

`So, with that let's start.`  
Hello, my fellow programmer's today I'm going to teach you how you can become _master's_ in **Graph**

If you want to become master, then you have to follow some **rules**, only after that you can become **Magician** or called **Master's in Graph**  
`Rules:`

- Bring up your **pen** and a fresh **new notebook** where you have to write all of these thing's which I will teach you **right now**.
- If you had started learning graph, then **don't quit**. Here's why, **ask yourself** this question when you feel about to quit, `"If you had to leave, then why you had start?"`
- Look back again at above 2 rule's

Remember : If you don't sacrifice for what you want, what you want become sacrify!

---

---

```
                                                            # Introduction to Graph
```

> A graph data structure is a collection of nodes that have data and are connected to other nodes.

**Let's try to understand this through an example.** On facebook, everything is a node. That includes User, Photo, Album, Event, Group, Page, Comment, Story, Video, Link, Note...anything that has **data is a node.**

Every relationship is an **edge** from one **node** to another. Whether you post a photo, join a group, like a page, etc., a new edge is created for that **relationship**.

![image](https://assets.leetcode.com/users/images/4d5d51f5-bd72-4545-b1f9-a4e8d0bf6a06_1659197642.251449.png)

All of facebook is then a collection of these nodes and edges. This is because `facebook uses a graph data structure to store its data.`

More precisely, a **graph is a data structure (V, E) that consists of**

- A collection of **vertices V**
- A collection of **edges E**, represented as ordered **pairs of vertices (u,v)**

And generally there are **2 types** of Graphs :- **`Undirected Graph`** and **`Directed Graph`**

![image](https://assets.leetcode.com/users/images/25e090a1-061c-4798-a18b-35beedd49912_1659197361.0471368.png)

**Terms used in Graph :-**

- **Adjacency:** A vertex is said to be adjacent to another vertex if there is an edge connecting them. Vertices 2 and 3 are not adjacent because there is no edge between them.
    
- **Path:** A sequence of edges that allows you to go from vertex A to vertex B is called a path. 0-1, 1-2 and 0-2 are paths from vertex 0 to vertex 2.
    
- **Directed Graph:** A graph in which an edge (u,v) doesn't necessarily mean that there is an edge (v, u) as well. The edges in such a graph are represented by arrows to show the direction of the edge.
    
- **Undirected Graph:** A graph in which an edge (u,v) mean's that there is an edge (v, u) and they are bi-directional.
    

**`Storing our Graph in Data Structure:`**

There are two ways to store Graph in a Data Structure.

1. **`Adjacency Matrix`** :- An adjacency matrix is a **2D array of V x V vertices**. Each row and column represent a vertex. If the value of any element `a[i][j]` is **1**, it represents that there is an edge connecting **vertex i** and **vertex j**.  
    Let's understand how we store data in matrix.

- First of all, create a matrix of **`n + 1 X n + 1`**
- And Intially our 2-D Array will be filled with `0`
- Since it is an **undirected graph**, for edge `(0,2)`, we also need to mark edge `(2,0)`
- And as weight of the edge is not given, we'll mark it with `1`  
    ![image](https://assets.leetcode.com/users/images/b7830ab9-3107-4d7a-9128-02462511ff97_1659199266.728581.png)

Let's look at code:-

**Java :-**

```java
import java.io.*;

class himalik {
	public static void main (String[] args) {
		int n = 3, m = 3; 
		int adj[][] = new int[n+1][n+1]; 
		
		// edge 1---2
		adj[1][2] = 1;
		adj[2][1] = 1; 
		
		
		// edge 2---3
		adj[2][3] = 1; 
		adj[3][2] = 1; 
		
		
		// adge 1--3
		adj[1][3] = 1;
		adj[3][1] = 1; 
		
	}
}
```

There'fore General Representation :-

```
adj[u][v] = 1
adj[v][u] = 1
```

**Disadvantage of using Adjacency Matrix** : Edge lookup(checking if an edge exists between vertex A and vertex B) is extremely fast in adjacency matrix representation but we have to **reserve space** for every possible link between all **`vertices(V x V), so it requires more space.`**  
For example the range of matrix we have given is **10^5** then, `10^5 X 10^5` will be out of bound [M.L.E]

2. To Optimise it we use >> **`Adjacency List`** : An adjacency list represents a graph as an array of **linked lists**. The index of the array represents a vertex and each element in its linked list represents the other vertices that form an edge with the vertex.  
    Let's understand how we store data in list, taken an example.  
    ![image](https://assets.leetcode.com/users/images/afc47dd7-966d-416e-87c6-629958bf5885_1659200461.7267952.png)

Let's look at code:-

**Java**

```java
import java.io.*;
import java.util.*; 

class himalik {
	public static void main (String[] args) {
		int n = 3, m = 3; 
		ArrayList<ArrayList<Integer> > adj = new ArrayList<>();
		
		for (int i = 0; i <= n; i++) 
			adj.add(new ArrayList<Integer>());
		
		// edge 1---2
		adj.get(1).add(2); 
		adj.get(2).add(1);
		
		
		adj.get(u).add(v);
		adj.get(v).add(u);
		
		// edge 2---3
		adj.get(2).add(3);
		adj.get(3).add(2);
		
		
		// adge 1--3
		adj.get(1).add(3);
		adj.get(3).add(1);
		
		
		for (int i = 1; i < n; i++) { 
			for (int j = 0; j < adj.get(i).size(); j++) { 
				System.out.print(adj.get(i).get(j)+" "); 
			} 
			System.out.println(); 
		}
		
	}
}
```

There'fore General Representation :-

```
adj.get(u).add(v) = 1
adj.get(v).add(u) = 1
```

An adjacency list is efficient in terms of storage because we only need to store the values for the edges. For a graph with millions of vertices, this can mean a lot of saved space.

**Space Complexity :-**

- **`For Undirected Graph :-`** BigO(N + 2 * E), where N is node & E is edge
    
- **`For Directed Graph :-`** BigO(N + E), where N is node & E is edge
    

```
                                                        # Connected Components In A Graph
```

A connected component is the **portion** of a **graph** in which there is a path from each vertex to another vertex.  
You can think it like this, when a graph is broken into several components, but those components are connected through vertex.

![image](https://assets.leetcode.com/users/images/9e9a588f-7620-4741-8067-7e49c3b320df_1659248974.499082.png)

**Let's break this graph into components,**

![image](https://assets.leetcode.com/users/images/c87beced-9b0b-41bf-b4cf-4dbd577b7337_1659249077.1561084.png)

```
Now, to Traverse this disconnected graph and check it's components. We gonna have one "visited [] array"
       -------------------------------------
vis[] =| 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 |
       -------------------------------------
index=>	 0   1   2   3   4   5   6   7   8
```

For the traversing we going to use either **`dfs`** OR **`bfs`**

The basic code will be like:-

```java
for(int i = 0; i < n; i++){
	if(!vis[i]){
		"dfs" OR "bfs"
	}
}
```

```
                                                         # Breadth-First Search (BFS)
```

BFS is a traversing algorithm where you should start traversing from a selected node (source or starting node) and traverse the graph layerwise thus exploring the neighbour nodes (nodes which are directly connected to source node). You must then move towards the next-level neighbour nodes.

A standard BFS implementation puts each vertex of the graph into one of two categories:

1. **Not Visited** --> An array with all values initialised with 0.
2. **Visited** --> An array with values updated from 0 to 1.

_The purpose of the algorithm is to mark each vertex as visited while avoiding cycles._

**The algorithm works as follows:**

- Start by putting any one of the graph's vertices at the **back of a queue**.
    
- Take the **front** item of the **queue** and **add** it to the **visited list**.
    
- Create a list of that vertex's adjacent nodes. **Add** the **ones** which aren't in the **visited list** to the **back of the queue**.
    
- Keep **repeating** steps 2 and 3 until the **queue is empty**.
    

**`Let's understand with an Example:`**

![image](https://assets.leetcode.com/users/images/247b22be-3353-4e44-a4fc-81a9cace0a09_1659263140.6649172.png)  
![image](https://assets.leetcode.com/users/images/13470171-fee5-4ca6-b356-12cf02407189_1659263278.4332829.png)  
![image](https://assets.leetcode.com/users/images/e4e820b0-6c8f-4bad-b2eb-9e6e33826233_1659263501.4634109.png)  
![image](https://assets.leetcode.com/users/images/424ec154-b889-4298-b984-5f97d45e0811_1659263796.2142274.png)  
![image](https://assets.leetcode.com/users/images/51f230cd-b025-4146-b983-924c54a12cca_1659263953.4639285.png)  
![image](https://assets.leetcode.com/users/images/5c63d692-2637-4986-9b62-92325c203d6d_1659264056.8107362.png)  
![image](https://assets.leetcode.com/users/images/1f3fda4e-1351-4037-adc9-24d955d88e19_1659264279.0527284.png)  
![image](https://assets.leetcode.com/users/images/5f1c2709-8aec-4a24-ac85-0a3f2ec19544_1659264296.8361673.png)

**Now, let's code it up:**

**Java**

```java
// { Driver Code Starts
// Initial Template for Java
import java.util.*;
import java.lang.*;
import java.io.*;
class GFG {
    public static void main(String[] args) throws IOException {
        BufferedReader br =
            new BufferedReader(new InputStreamReader(System.in));
        int T = Integer.parseInt(br.readLine().trim());
        while (T-- > 0) {
            String[] s = br.readLine().trim().split(" ");
            int V = Integer.parseInt(s[0]);
            int E = Integer.parseInt(s[1]);
            ArrayList<ArrayList<Integer>> adj = new ArrayList<>();
            for (int i = 0; i < V; i++) adj.add(i, new ArrayList<Integer>());
            for (int i = 0; i < E; i++) {
                String[] S = br.readLine().trim().split(" ");
                int u = Integer.parseInt(S[0]);
                int v = Integer.parseInt(S[1]);
                adj.get(u).add(v);
                // adj.get(v).add(u);
            }
            Solution obj = new Solution();
            ArrayList<Integer> ans = obj.bfsOfGraph(V, adj);
            for (int i = 0; i < ans.size(); i++)
                System.out.print(ans.get(i) + " ");
            System.out.println();
        }
    }
}
// } Driver Code Ends


class Solution {
    // Function to return Breadth First Traversal of given graph.
    public ArrayList<Integer> bfsOfGraph(int V, ArrayList<ArrayList<Integer>> adj) {
        // Code here
        ArrayList<Integer> bfs = new ArrayList<>();
        boolean vis[] = new boolean[V + 1];
        Queue<Integer> q = new LinkedList<>();
                
                q.add(0);
                vis[0] = true;
                
                while(!q.isEmpty()){
                    Integer node = q.poll();
                    bfs.add(node);
                    
                    for(Integer it : adj.get(node)){
                        if(vis[it] == false){
                            q.add(it);
                            vis[it] = true;
                        }
                    }
                }
        return bfs;
    }
}
```

ANALYSIS :-

- **Time Complexity :-** **`BigO(N+E)`** where N = Nodes , E = travelling through adjacent nodes
    
- **Space Complexity :-** **`BigO(N+E) + O(N) + O(N)`** where Space for adjacency list, visited array, queue data structure
    

```
                                                                     # Depth-First Search (DFS)
```

Depth First Traversal is a traversal technique/algorithm, used to traverse through all the nodes in the given graph.

It starts traversal through any one of its neighbour nodes and explores the farthest possible node in each path/branch and then starts Back-tracking.

Backtracking happens when the DFS algorithm reaches a particular node that has no neighbours to visit further, once it reaches that node with no neighbours to be visited it’ll backtrack to its previous node (say N) and from this node N algorithm will start searching for unvisited neighbour nodes and starts visiting them.

**Approach:**

- Start with a **random** node from **graph**
    
- Make an **array** to keep track of **visited** nodes, once visited **mark** that node as **visited**
    
- **Print** this current node
    
- Get neighbour nodes and perform above steps **recursively** for each node **deeply/depthly** if node is **unvisited**.
    

**Let's understand with an example:**

![image](https://assets.leetcode.com/users/images/1e9f0f2e-6148-4f24-96ae-bf6aef19358f_1659265809.7410023.png)  
![image](https://assets.leetcode.com/users/images/06633920-7e22-406f-8455-17cb3d5b9cd3_1659265915.2750406.png)  
![image](https://assets.leetcode.com/users/images/879978e7-3694-42e5-9b2a-b8fcc408ef71_1659266030.0933847.png)  
![image](https://assets.leetcode.com/users/images/f3e3d696-b8ad-4fc6-9f8b-5bc700a88f44_1659266321.223954.png)  
![image](https://assets.leetcode.com/users/images/b838cc89-bd12-4cf3-81c6-6685a3d6b40d_1659266523.455421.png)  
![image](https://assets.leetcode.com/users/images/1dc93203-ba0b-4a51-9b95-92356c4be2a6_1659266587.854001.png)  
![image](https://assets.leetcode.com/users/images/776d0df2-a724-40a6-adb8-e284beb1837d_1659266681.1965463.png)  
![image](https://assets.leetcode.com/users/images/b0ed307a-d188-4d1a-9422-90f32289cebe_1659266769.7699058.png)  
![image](https://assets.leetcode.com/users/images/2a5f146c-cdf2-4747-a073-83d091403266_1659266893.7918634.png)  
![image](https://assets.leetcode.com/users/images/47d55a43-244f-4c30-86d8-1c54a5c59e7a_1659266931.791352.png)

**Now, let's code it up:**

**Java**

```java
// { Driver Code Starts
// Initial Template for Java
import java.util.*;
import java.lang.*;
import java.io.*;
class GFG {
    public static void main(String[] args) throws IOException {
        BufferedReader br =
            new BufferedReader(new InputStreamReader(System.in));
        int T = Integer.parseInt(br.readLine().trim());
        while (T-- > 0) {
            String[] s = br.readLine().trim().split(" ");
            int V = Integer.parseInt(s[0]);
            int E = Integer.parseInt(s[1]);
            ArrayList<ArrayList<Integer>> adj =
                new ArrayList<ArrayList<Integer>>();
            for (int i = 0; i < V; i++) adj.add(new ArrayList<Integer>());
            for (int i = 0; i < E; i++) {
                String[] S = br.readLine().trim().split(" ");
                int u = Integer.parseInt(S[0]);
                int v = Integer.parseInt(S[1]);
                adj.get(u).add(v);
                adj.get(v).add(u);
            }
            Solution obj = new Solution();
            ArrayList<Integer> ans = obj.dfsOfGraph(V, adj);
            for (int i = 0; i < ans.size(); i++)
                System.out.print(ans.get(i) + " ");
            System.out.println();
        }
    }
}
// } Driver Code Ends


class Solution {
    // Function to return a list containing the DFS traversal of the graph.
    public ArrayList<Integer> dfsOfGraph(int V, ArrayList<ArrayList<Integer>> adj) {
        // Code here
        ArrayList<Integer> dfsStore = new ArrayList<>();
        boolean vis[] = new boolean[V + 1];
        
        for(int i = 0; i < V; i++){
            if(vis[i] == false){
                dfs(i, vis, adj, dfsStore);
            }
        }
        return dfsStore;
    }
    public void dfs(int node, boolean vis[], ArrayList<ArrayList<Integer>> adj, ArrayList<Integer> dfsStore){
        dfsStore.add(node);
        vis[node] = true;
        
        for(Integer i : adj.get(node)){
            if(vis[i] == false){
                dfs(i, vis, adj, dfsStore);
            }
        }
    }
}
```

ANALYSIS :-

- **Time Complexity :-** **`BigO(N+E)`** Where N is the time taken for visiting N nodes and E is for travelling through adjacent nodes.
    
- **Space Complexity :-** **`BigO(N+E) + O(N) + O(N)`** where Space for adjacency list, Array,Auxiliary space.
    

```
                                                       # Detect A Cycle In Undirected Graph {B F S}
```

In this we have to check wether a **cycle** present in **Undirected graph.**

`Intuition :-`  
The intuition behind this is to check for the visited element if it is found again, this means the **cycle is present** in the given undirected graph.

![image](https://assets.leetcode.com/users/images/e1109808-d07d-442f-b8d2-535b4841fca5_1659271970.9416413.png)

`Approach :-`

**For the first component,** firstly we insert the first element of the graph by marking it as visited in the Queue having prev of the first element as -1. Now we pop out that element and traverse the adjacent element list for that and then insert the elements in the Queue and continue the process until no adjacent element is found for the present element. Here, we can see that no loop is formed. `So, we return false for the first component.`

![image](https://assets.leetcode.com/users/images/d24348c7-cfa2-4e73-a606-edd801aa6d35_1659271952.7609158.png)

**For the second component,** a similar process will be done as we have done for the first component. Here we will be able to see that when we come to 7, 8 is one of the next adjacent ones which matters to us, and also, it is already marked as positive. This means someone is linked already with this element. `So, it forms a loop and we return true finally.`

![image](https://assets.leetcode.com/users/images/1f0865d5-ce47-4cd3-834a-a9aa91db37b3_1659272982.6236727.png)

**Now, let's code it up:**

**Java**

```java
import java.util.*;
import java.lang.*;
import java.io.*;
class GFG
{
    public static void main(String[] args) throws IOException
    {
       
            int V = 5;
            ArrayList<ArrayList<Integer>>adj = new ArrayList<>();
            for(int i = 0; i < V; i++)
                adj.add(i, new ArrayList<Integer>());
                adj.get(0).add(1);
                adj.get(0).add(2);
                adj.get(2).add(3);
                adj.get(1).add(3);
                adj.get(2).add(4);

            Solution obj = new Solution();
            boolean ans = obj.isCycle(V, adj);
            if(ans)
                System.out.println("Yes");
            else
                System.out.println("No");
        }
    }


class Node {
    int first;
    int second;
    public Node(int first, int second) {
        this.first = first;
        this.second = second; 
    }
}
class himalik
{
   static boolean checkForCycle(ArrayList<ArrayList<Integer>> adj, int s,
            boolean vis[])
    {
       Queue<Node> q =  new LinkedList<>(); //BFS
       q.add(new Node(s, -1));
       vis[s] =true;
       
       while(!q.isEmpty())
       {
           int node = q.peek().first;
           int par = q.peek().second;
           q.remove(); 
           
           for(Integer it: adj.get(node))
           {
               if(vis[it]==false)  
               {
                   q.add(new Node(it, node));
                   vis[it] = true; 
               }
        
               else if(par != it) return true;
           }
       }
       
       return false;
    }
    public boolean isCycle(int V, ArrayList<ArrayList<Integer>> adj)
    {
        boolean vis[] = new boolean[V];
        Arrays.fill(vis,false);
        for(int i=0;i<V;i++)
            if(vis[i]==false) 
                if(checkForCycle(adj, i,vis)) 
                    return true;
    
        return false;
    }
}
```

ANALYSIS :-

- **Time Complexity :-** **`BigO(N+E)`** Where N is the time taken and E is for traveling through adjacent nodes overall.
    
- **Space Complexity :-** **`BigO(N+E) + O(N) + O(N)`** where space for adjacent list , array and queue
    

```
                                                           # Detect A Cycle In Undirected Graph {D F S}
```

So, the problem description is same as above one.

**To solve this we going to** run a for loop from the first node to the last node and check if the node is visited. If it is not visited then call the function recursively which goes into the depth as known as DFS search and if you find a cycle you can say that there is a cycle in the graph.

- Basically calling the isCyclic function with number of nodes and passing the graph  
    Traversing from 1 to number of nodes and checking for every node if it is unvisited
    
- If the node is unvisited then call a function checkForCycle, that checks if there is a cycle and returns true if there is a cycle.
    
- Now the function checkForCycle has the node and previous of the parent node. It will also have the visited array and the graph that has adjacency list
    
- Mark it as visited and then traverse for its adjacency list using a for loop.
    
- Calling DFS traversal if that node is unvisited call recursive function that checks if its a cycle and returns true
    
- If the previously visited node and it is not equal to the parent we can say there is cycle again and will return true
    
- Now if you have traveled for all adjacent nodes and all the DSF have been called and it never returned true that means we have done the DSF call entirely and now we can return false, that mean there is no DSF cycle
    

![image](https://assets.leetcode.com/users/images/259b1908-d94f-4efa-8265-136e23ae7e3b_1659431883.9888065.png)  
![image](https://assets.leetcode.com/users/images/39c79a00-3899-4544-b861-8cce48409e27_1659431919.7921681.png)

**Now, let's code it up:**

**Java**

```java
// { Driver Code Starts
import java.util.*;
import java.lang.*;
import java.io.*;
class GFG {
    public static void main(String[] args) throws IOException {
        BufferedReader br =
            new BufferedReader(new InputStreamReader(System.in));
        int T = Integer.parseInt(br.readLine().trim());
        while (T-- > 0) {
            String[] s = br.readLine().trim().split(" ");
            int V = Integer.parseInt(s[0]);
            int E = Integer.parseInt(s[1]);
            ArrayList<ArrayList<Integer>> adj = new ArrayList<>();
            for (int i = 0; i < V; i++) adj.add(i, new ArrayList<Integer>());
            for (int i = 0; i < E; i++) {
                String[] S = br.readLine().trim().split(" ");
                int u = Integer.parseInt(S[0]);
                int v = Integer.parseInt(S[1]);
                adj.get(u).add(v);
                adj.get(v).add(u);
            }
            Solution obj = new Solution();
            boolean ans = obj.isCycle(V, adj);
            if (ans)
                System.out.println("1");
            else
                System.out.println("0");
        }
    }
}// } Driver Code Ends


class Solution {
    // Function to detect cycle in an undirected graph.
    public boolean isCycle(int V, ArrayList<ArrayList<Integer>> adj) {
        // Code here
        boolean vis[] = new boolean[V + 1];
        Arrays.fill(vis, false);
        
        for(int i = 0; i < V; i++){
            if(vis[i] == false){
                if(cycleDFS(i, -1, vis, adj)) return true;
            }
        }
        return false;
    }
    public boolean cycleDFS(int node, int par, boolean vis[], ArrayList<ArrayList<Integer>> adj){
        vis[node] = true;
        for(Integer i : adj.get(node)){
            if(vis[i] == false){
                if(cycleDFS(i, node, vis, adj) == true) return true; 
            }
            else if(i != par) return true;
        }
        return false;
    }
}
```

ANALYSIS :-

- **Time Complexity :-** **`BigO(N)`**
    
- **Space Complexity :-** **`BigO(N)`**
    

```
                                                  # Biparite Graph (B F S)
```

`Definition :-`  
A bipartite graph (or bigraph) is a graph whose vertices can be divided into two disjoint and independent sets and , that is every edge connects a vertex in to one in. _**Source :- Wikipedia**_  
![image](https://assets.leetcode.com/users/images/05d42fcb-1763-438a-bfc6-0840139e173f_1659362907.0554354.png)

**Okay so in simple terms**, A bipartite graph is possible if the graph coloring is possible using two colors such that vertices in a set are colored with the same color. Note that it is possible to color a cycle graph with even cycle using two colors. For example, see the following graph.  
![image](https://assets.leetcode.com/users/images/e2e59252-a23c-458a-bb73-175a5282ad64_1659362968.7233508.png)

**It is not possible to color a cycle graph with odd cycle using two colors.**  
![image](https://assets.leetcode.com/users/images/24883bda-7d9b-4f01-8872-9e6d120bc839_1659363005.0999663.png)

So, with the help of an example, let's see whether a **graph** is **bipartite** or not.

To, solve it we gonna use the help of **Queue** and a **color array**

![image](https://assets.leetcode.com/users/images/167788d3-e342-4bf4-9530-e76e6a846108_1659363985.4452362.png)  
![image](https://assets.leetcode.com/users/images/b6725e87-32ae-4183-b9ae-06f9d0777053_1659364453.8620756.png)  
![image](https://assets.leetcode.com/users/images/e0d1c226-149b-4c31-b30a-b6bc006d4fe5_1659364621.5654886.png)  
![image](https://assets.leetcode.com/users/images/b58df9d2-0557-49e8-bdac-4c3159a950b0_1659364740.4230244.png)  
![image](https://assets.leetcode.com/users/images/c80cd27e-2d9e-40b6-808c-7ea6c53677a7_1659365001.6937263.png)  
![image](https://assets.leetcode.com/users/images/48f7b7d8-ccde-4386-a563-fa8812da62c3_1659365135.3009722.png)  
![image](https://assets.leetcode.com/users/images/377efe0b-2e86-4f57-a8cd-e10266dc2bce_1659365396.6079266.png)  
![image](https://assets.leetcode.com/users/images/a95a1239-5c6c-4cec-a137-e679ff7b18e6_1659365532.7522397.png)

**Now, let's code it up:**

**Java**

```java
// { Driver Code Starts
import java.util.*;
import java.lang.*;
import java.io.*;
class GFG
{
    public static void main(String[] args) throws IOException
    {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int T = Integer.parseInt(br.readLine().trim());
        while(T-->0)
        {
            String[] S = br.readLine().trim().split(" ");
            int V = Integer.parseInt(S[0]);
            int E = Integer.parseInt(S[1]);
            ArrayList<ArrayList<Integer>> adj = new ArrayList<>();
            for(int i = 0; i < V; i++){
                adj.add(new ArrayList<Integer>());
            }
            for(int i = 0; i < E; i++){
                String[] s = br.readLine().trim().split(" ");
                int u = Integer.parseInt(s[0]);
                int v = Integer.parseInt(s[1]);
                adj.get(u).add(v);
                adj.get(v).add(u);
            }
            Solution obj = new Solution();
            boolean ans = obj.isBipartite(V, adj);
            if(ans)
                System.out.println("1");
            else System.out.println("0");
       }
    }
}// } Driver Code Ends


class himalik
{
    public boolean isBipartite(int V, ArrayList<ArrayList<Integer>>adj)
    {
        // Code here
        int color[] = new int[V + 1];
        Arrays.fill(color, -1);
        
        for(int i = 0; i < V; i++){
            if(color[i] == -1){
                if(!bfs(i, color, adj)) return false;
            }
        }
        return true;
    }
    public boolean bfs(int node, int color[], ArrayList<ArrayList<Integer>>adj){
        Queue<Integer> q = new LinkedList<>();
        q.add(node);
        color[node] = 1;
        
        while(!q.isEmpty()){
            int nde = q.poll();
            for(Integer i : adj.get(nde)){
                if(color[i] == -1){
                    q.add(i);
                    color[i] = 1 - color[nde];
                }
                else if(color[i] == color[nde]) return false;
            }
        }
        return true;
    }
}
```

ANALYSIS :-

- **Time Complexity :-** **`BigO(N+E)`** Where N is the time taken and E is for traveling through adjacent nodes overall.
    
- **Space Complexity :-** **`BigO(N+E) + O(N) + O(N)`** where space for adjacent list , array and queue
    

```
                                                  # Biparite Graph (D F S)
```

**The Definition & explanation is same as given above for BFS, only what the difference is we'll solve this recursively!**

Well, using recursion. we going to also take up the help of **color array.**

![image](https://assets.leetcode.com/users/images/6f62d326-db27-4ee5-b11a-829e45a87e56_1659369564.638326.png)

**Now, let's code it up:**

**Java**

```java
// { Driver Code Starts
import java.util.*;
import java.lang.*;
import java.io.*;
class GFG
{
    public static void main(String[] args) throws IOException
    {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int T = Integer.parseInt(br.readLine().trim());
        while(T-->0)
        {
            String[] S = br.readLine().trim().split(" ");
            int V = Integer.parseInt(S[0]);
            int E = Integer.parseInt(S[1]);
            ArrayList<ArrayList<Integer>> adj = new ArrayList<>();
            for(int i = 0; i < V; i++){
                adj.add(new ArrayList<Integer>());
            }
            for(int i = 0; i < E; i++){
                String[] s = br.readLine().trim().split(" ");
                int u = Integer.parseInt(s[0]);
                int v = Integer.parseInt(s[1]);
                adj.get(u).add(v);
                adj.get(v).add(u);
            }
            Solution obj = new Solution();
            boolean ans = obj.isBipartite(V, adj);
            if(ans)
                System.out.println("1");
            else System.out.println("0");
       }
    }
}// } Driver Code Ends


class himalik
{
    public boolean isBipartite(int V, ArrayList<ArrayList<Integer>>adj)
    {
        // Code here
        int color[] = new int[V + 1];
        Arrays.fill(color, -1);
        
        for(int i = 0; i < V; i++){
            if(color[i] == -1){
                if(!dfs(i, color, adj)) return false;
            }
        }
        return true;
    }
    public boolean dfs(int node, int color[], ArrayList<ArrayList<Integer>>adj){
        // if(color[node] == -1) color[node] = 0;
        
        for(Integer i : adj.get(node)){
            if(color[i] == -1){
                color[i] = 1 - color[node];
                if(!dfs(i, color, adj)) return false;
            }
            else if(color[i] == color[node]) return false;
        }
        return true;
    }
}
```

ANALYSIS :-

- **Time Complexity :-** **`BigO(V+E)`** since in its whole, it is a DFS implementation, V – vertices; E – edges;
    
- **Space Complexity :-** **`BigO(V)`** because, apart from the graph, we maintain a color array.
    

```
                                                  # Cycle Detection In Directed Graph (D F S)
```

A cycle involves at least 2 nodes. The basic intuition for cycle detection is to check whether a node is reachable when we are processing its neighbors and also its neighbors’ neighbors, and so on.  
**Look at this example what I mean**  
![image](https://assets.leetcode.com/users/images/cfe3d7d6-60b1-4885-974f-0eb9409220ff_1659432687.2272131.png)

We can see that 7 is reachable through 8 and 9. We can use the normal DFS traversal with some modifications to check for cycles.

**Now Let's understand it visually:-**  
![image](https://assets.leetcode.com/users/images/b475899f-f5a5-4b30-a92e-d8f9e002ba4a_1659434004.8924425.png)  
![image](https://assets.leetcode.com/users/images/7ea44fb4-34aa-4a58-b879-2937f9b47d21_1659434332.1978254.png)  
![image](https://assets.leetcode.com/users/images/dc367883-4ab8-46ae-854b-f2105ee92844_1659434577.1687574.png)

**Now, let's code it up:**

**Java**

```java
// { Driver Code Starts
import java.util.*;
import java.io.*;
import java.lang.*;

class DriverClass {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int t = sc.nextInt();

        while (t-- > 0) {
            ArrayList<ArrayList<Integer>> list = new ArrayList<>();
            int V = sc.nextInt();
            int E = sc.nextInt();
            for (int i = 0; i < V + 1; i++)
                list.add(i, new ArrayList<Integer>());
            for (int i = 0; i < E; i++) {
                int u = sc.nextInt();
                int v = sc.nextInt();
                list.get(u).add(v);
            }
            if (new Solution().isCyclic(V, list) == true)
                System.out.println("1");
            else
                System.out.println("0");
        }
    }
}// } Driver Code Ends


/*Complete the function below*/

class Solution {
    // Function to detect cycle in a directed graph.
    public boolean isCyclic(int V, ArrayList<ArrayList<Integer>> adj) {
        // code here
        int vis[] = new int[V + 1];
        int dfsVis[] = new int[V + 1];
        Arrays.fill(vis, 0);
        Arrays.fill(dfsVis, 0);
        
        for(int i = 0; i < V; i++){
            if(vis[i] == 0){
                if(cycleDFS(i, vis, dfsVis, adj)) return true;
            }
        }
        return false;
    }
    public boolean cycleDFS(int node, int vis[], int dfsVis[], ArrayList<ArrayList<Integer>> adj){
        vis[node] = 1;
        dfsVis[node] = 1;
        
        for(Integer i : adj.get(node)){
            if(vis[i] == 0){
                if(cycleDFS(i, vis, dfsVis, adj)) return true;
            }
            else if(dfsVis[i] == 1) return true;
        }
        dfsVis[node] = 0;
        return false;
    }
}
```

ANALYSIS :-

- **Time Complexity :-** **`BigO(V+E)`** since in its whole, it is a DFS implementation, V – vertices; E – edges;
    
- **Space Complexity :-** **`BigO(V)`** because, apart from the graph, we have 2 arrays of size V, to store the required information
    

```
                                                  # Topological Sort (D F S)
```

First of all let’s understand Topological Sorting. It means linear ordering of vertices such that there is an edge `u—-> v`, **u** appears before **v** in the ordering.

**Let's take an example,**  
![image](https://assets.leetcode.com/users/images/f82bb7fb-3c31-46c8-9495-49227aa030a9_1659451934.4599547.png)

Some of the possible Topological orders can be:

- `5,4,2,3,1,0`
    
- `4,5,2,3,1,0`
    
- In both cases we can see, that  
    `4->0 ( 4 appears before 0 ) , 5>3 ( 5 appears before 3 ), …`
    
- Similarly there can be **multiple toposorts order for the given graph** but the condition should be if there is an edge `u->v` then **u** should always appear before **v**.
    
- Topological Sorting is applicable only for DAG(Directed Acyclic Graph). **Why is it so?**  
    **Because of the following reasons:**
    
- 1. Specifically, only u->v is not applicable for undirected graphs. It is uncertain if the edge (u-v) lies between u and v or v and u.
- 2. There will always be a dependence factor in a circular graph. You cannot guarantee that the vertices will be arranged linearly.

```
Finally, you now fully get what Topological Sorting is.
To fix the issue, we'll use the DFS (Depth First Search) approach.
Each vertex's neighbouring vertex will be explored for each vertex in turn.
Following exploration, the current vertex will be stored in a data structure to preserve Topo Sort.
```

**We will be using the following data structure to get Topo sort:**

1. **`Visited Vector`** – To store visit of each vertex
2. **`Stack`** – To maintain the topo sort order.  
    ![image](https://assets.leetcode.com/users/images/c2f0f337-7f54-4d84-86fa-ad3456a8d959_1659452683.4804442.png)  
    ![image](https://assets.leetcode.com/users/images/2fd54fb0-7b54-4560-95d7-d6fecdf84bb1_1659452826.7975717.png)  
    ![image](https://assets.leetcode.com/users/images/852d9577-012d-4b23-a5a6-0b07d97e4e2a_1659452958.7029707.png)  
    ![image](https://assets.leetcode.com/users/images/8f8f9470-5eec-4c41-b105-6c5970054522_1659453337.0183005.png)  
    ![image](https://assets.leetcode.com/users/images/b07a40d1-2ac0-4062-a40a-294f2b75e338_1659453525.44481.png)  
    ![image](https://assets.leetcode.com/users/images/de01c694-656f-4199-864a-c425c05adcdf_1659453622.4851377.png)

**Aside from utilising Stack, did you notice anything else?** just because **u** had an edge over **v**. From **u** to **v**, the DFS call will travel. Initial, the first **dfs (v)**, and then **dfs (u)**. Here, we are ensuring that if `u->v`, **v** will be placed onto the stack first, followed by **u**. `This is how the Stack maintains topological order.`

**Now, let's code it up:**

**Java**

```java
// { Driver Code Starts
import java.util.*;
import java.io.*;
import java.lang.*;

class Main {
    public static void main(String[] args) throws IOException {
        BufferedReader read =
            new BufferedReader(new InputStreamReader(System.in));
        int t = Integer.parseInt(read.readLine());

        while (t-- > 0) {
            ArrayList<ArrayList<Integer>> list = new ArrayList<>();
            String st[] = read.readLine().trim().split("\\s+");
            int edg = Integer.parseInt(st[0]);
            int nov = Integer.parseInt(st[1]);

            for (int i = 0; i < nov + 1; i++)
                list.add(i, new ArrayList<Integer>());

            int p = 0;
            for (int i = 1; i <= edg; i++) {
                String s[] = read.readLine().trim().split("\\s+");
                int u = Integer.parseInt(s[0]);
                int v = Integer.parseInt(s[1]);
                list.get(u).add(v);
            }

            int[] res = new Solution().topoSort(nov, list);

            if (check(list, nov, res) == true)
                System.out.println("1");
            else
                System.out.println("0");
        }
    }
    static boolean check(ArrayList<ArrayList<Integer>> list, int V, int[] res) {
        
        if(V!=res.length)
        return false;
        
        int[] map = new int[V];
        for (int i = 0; i < V; i++) {
            map[res[i]] = i;
        }
        for (int i = 0; i < V; i++) {
            for (int v : list.get(i)) {
                if (map[i] > map[v]) return false;
            }
        }
        return true;
    }
}
// } Driver Code Ends


/*Complete the function below*/


class Solution
{
    //Function to return list containing vertices in Topological order. 
    static int[] topoSort(int V, ArrayList<ArrayList<Integer>> adj) 
    {
        // add your code here
        Stack<Integer> st = new Stack<>();
        int vis[] = new int[V + 1];
        Arrays.fill(vis, 0);
        for(int i = 0; i < V; i++){
            if(vis[i] == 0){
                dfs(i, vis, st, adj); 
            }
        }
        int topo[] = new int[V];
        int i = 0;
        while(!st.isEmpty()){
            topo[i++] = st.pop();
        }
        return topo;
    }
    public static void dfs(int node, int vis[], Stack<Integer> st, ArrayList<ArrayList<Integer>> adj){
        vis[node] = 1;
        for(Integer i : adj.get(node)){
            if(vis[i] == 0){
                dfs(i, vis, st, adj);
            }
        }
        st.push(node);
    }
}

```

ANALYSIS :-

- **Time Complexity :-** **`BigO(N+E)`** where N = Number of node , E = Number of Edges
    
- **Space Complexity :-** **`BigO(N) + O(N)`** because, Visited Array and Stack data structure. Both will be using O(N).
    

```
                                                  # Topological Sort (B F S) "OR" KAHN'S ALGORITHM
```

Topological sorting for Directed Acyclic Graph (DAG) is a linear ordering of vertices such that for every directed edge **uv**, vertex **u** comes before **v** in the ordering. Topological Sorting for a graph is not possible if the graph is not a DAG.  
**`For example,`** a topological sorting of the following graph is “_**5 4 2 3 1 0?. There can be more than one topological sorting for a graph. For example, another topological sorting of the following graph is “4 5 2 0 3 1**_″. The first vertex in topological sorting is always a vertex with an in-degree of 0 (a vertex with no incoming edges).

![image](https://assets.leetcode.com/users/images/d805bc3d-4a8b-41b1-a59b-b1f36ab50da7_1659682355.2436984.png)

Now, let's talk about how we can solve this using BFS, or How's Kahn's Algorithm helps us.

So, In this instead of using ~~**visited array**~~ we going to use **array of indegree**. Now some of you may will ask, _dude wait but what is indegree?_

Well I forgot to tell you in the very beginning about degree & indegree!!  
Here's the quick understanding:-

- **OutDegree :-** Outdegree of vertex V is the number of edges which are going out from the vertex V.
- **InDegree :-** Indegree of vertex V is the number of edges which are coming into the vertex V.

So, more you understand this while we solve the problem, **now let's get back to the problem again.**

```
The data Structure we use to solve this problem is:-

> Queue :- The queue will store the "0" indegree vertex only
> Indegree Array :- We will going to have all kind of vertex whose indergree is 0 or greater then 0. 
(If indegree of a vertex is greater then 0, we going to decrement it until 0)
```

**Now, let's understand this problem using an example,**  
![image](https://assets.leetcode.com/users/images/7825a1b4-a2aa-4f11-a3c9-f1254c592a34_1659683518.0405114.png)

- **Our First job is to fill the `indegree array` with the degree as per the node/vertex**  
    ![image](https://assets.leetcode.com/users/images/0aa1c7bc-6b98-48b6-b0f6-602dd10e3837_1659683716.221666.png)
    
- **Now as you can, see we have done that. Now our next job is to push `0` vertex in the `queue` i.e. we have `4 & 5` & after doing that we have to reduce it's adjacent node value by 1. In our case node `4` adjacent are `0 & 1` & node `5` adjacent are `0 & 2`**  
    ![image](https://assets.leetcode.com/users/images/604015ac-a672-4b58-b1d0-4944aa9bae05_1659684236.718819.png)
    
- **Now do the same for node `5`**  
    ![image](https://assets.leetcode.com/users/images/8f05ea04-4937-41e5-a2d2-12d00dfd739d_1659684341.8317804.png)
    
- **Now, next `0` indegree vertex/node we have is `0`**  
    ![image](https://assets.leetcode.com/users/images/3af68b8c-df24-4481-8665-3e47ae20710e_1659684502.964731.png)
    
- **Next is `2` with indegree `0` & it's adjacent is `3` so decrement it value by 1**  
    ![image](https://assets.leetcode.com/users/images/cadd7ca7-6e2b-44d0-8411-df093d7e17f2_1659684642.0986526.png)
    
- **Next is `3` with indegree `0` & it's adjacent is `1` so decrement it value by 1**  
    ![image](https://assets.leetcode.com/users/images/d770f6d8-81ac-4eab-8a26-8eb1502b1cae_1659684739.0699668.png)
    
- **Finally `1` whose indegree is `0` now so, put it into the queue & no one is adjacent to it's**  
    ![image](https://assets.leetcode.com/users/images/9f67df7c-28be-43a8-9ce8-7cd6f3c078e7_1659684844.798641.png)
    

**Now, let's code it up:**

**Java**

```java
// { Driver Code Starts
import java.util.*;
import java.io.*;
import java.lang.*;

class Main {
    public static void main(String[] args) throws IOException {
        BufferedReader read =
            new BufferedReader(new InputStreamReader(System.in));
        int t = Integer.parseInt(read.readLine());

        while (t-- > 0) {
            ArrayList<ArrayList<Integer>> list = new ArrayList<>();
            String st[] = read.readLine().trim().split("\\s+");
            int edg = Integer.parseInt(st[0]);
            int nov = Integer.parseInt(st[1]);

            for (int i = 0; i < nov + 1; i++)
                list.add(i, new ArrayList<Integer>());

            int p = 0;
            for (int i = 1; i <= edg; i++) {
                String s[] = read.readLine().trim().split("\\s+");
                int u = Integer.parseInt(s[0]);
                int v = Integer.parseInt(s[1]);
                list.get(u).add(v);
            }

            int[] res = new Solution().topoSort(nov, list);

            if (check(list, nov, res) == true)
                System.out.println("1");
            else
                System.out.println("0");
        }
    }
    static boolean check(ArrayList<ArrayList<Integer>> list, int V, int[] res) {
        
        if(V!=res.length)
        return false;
        
        int[] map = new int[V];
        for (int i = 0; i < V; i++) {
            map[res[i]] = i;
        }
        for (int i = 0; i < V; i++) {
            for (int v : list.get(i)) {
                if (map[i] > map[v]) return false;
            }
        }
        return true;
    }
}
// } Driver Code Ends


/*Complete the function below*/


class himalik
{
    //Function to return list containing vertices in Topological order. 
    static int[] topoSort(int V, ArrayList<ArrayList<Integer>> adj) 
    {
        // add your code here
        Stack<Integer> st = new Stack<>();
        int vis[] = new int[V + 1];
        Arrays.fill(vis, 0);
        for(int i = 0; i < V; i++){
            if(vis[i] == 0){
                dfs(i, vis, st, adj); 
            }
        }
        int topo[] = new int[V];
        int i = 0;
        while(!st.isEmpty()){
            topo[i++] = st.pop();
        }
        return topo;
    }
    public static void dfs(int node, int vis[], Stack<Integer> st, ArrayList<ArrayList<Integer>> adj){
        vis[node] = 1;
        for(Integer i : adj.get(node)){
            if(vis[i] == 0){
                dfs(i, vis, st, adj);
            }
        }
        st.push(node);
    }
}
```

ANALYSIS :-

- **Time Complexity :-** **`BigO(N+E)`** where N = Number of node , E = Number of Edges
    
- **Space Complexity :-** **`BigO(N) + O(N)`** because, Indegree Array and Queue data structure. Both will be using O(N).
    

---

---

UpComing Topics to be covered :-

---

---

~~1. Biparite Graph[BFS]~~  
~~2. Biparite Graph[DFS]~~  
~~3. Cycle Detection In Directed Graph[DFS]~~  
~~4. Topological Sort[DFS]~~  
~~5. Topological Sort[BFS] a.k.a **Kahn's Algorithm**~~  
6. Cycle Detection In Directed Graph[BFS]  
7. Smallest Distance In Undirected Graph  
8. Shortest Path In a DAG[Direct Acylic Graph]  
9. Shortest Path In Undirected Graph a.k.a **Dijkstra's Algorithm**  
10. Minimum Spanning Tree a.k.a **Prim's Algorithm**  
11. Disjoint Set/ Union By Rank & Path Compression  
12. **Kruskal's Algorithm**
13. Bellman-Ford Algorithm.
14. Floyd-Warshall Algorithm
15. Kosaraju's Algorithm
16. Tarjan's Algorithm

???

So, these 7 topics left to be added in this article to make you **MASTER** & these article will going to be added soon. Thank You for your patience. **:)**

![image](https://assets.leetcode.com/users/images/52a89c09-bc78-4d41-9812-2495f53750ae_1646046931.074265.gif)![image](https://assets.leetcode.com/users/images/e42b717b-1937-4dd3-b10b-97425499b420_1659280317.3472593.gif)

```
And Guy's as always there is a lot to know, a lot to discuss.
"Let me know your thought's in comment." //  All sort of views are welcome :)
```