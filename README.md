# Dijkstra-s-Algorithm
// STL implementation of Prim's algorithm for MST
#include<bits/stdc++.h>
using namespace std;
# define INF 10000000000000000

// iPair ==> Integer Pair
typedef pair<long long, int> iPair;

// This class represents a directed graph using
// adjacency list representation
class Graph
{
	int V; // No. of vertices

	// In a weighted graph, we need to store vertex
	// and weight pair for every edge
	list< pair<long long, int> > *adj;

public:
	Graph(int V); // Constructor

	// function to add an edge to graph
	void addEdge(int u, int v, int w);

	// Print MST using Prim's algorithm
	void primMST(int src);
};

// Allocates memory for adjacency list
Graph::Graph(int V)
{
	this->V = V;
	adj = new list<iPair> [V];
}

void Graph::addEdge(int u, int v, int w)
{
	adj[u].push_back(make_pair(v, w));
	adj[v].push_back(make_pair(u, w));
}

// Prints shortest paths from src to all other vertices
void Graph::primMST(int src)
{
	// Create a priority queue to store vertices that
	// are being preinMST. This is weird syntax in C++.
	// Refer below link for details of this syntax
	// http://geeksquiz.com/implement-min-heap-using-stl/
	priority_queue< iPair, vector <iPair> , greater<iPair> > pq;

	 

	// Create a vector for keys and initialize all
	// keys as infinite (INF)
	vector<long long> key(V, INF);

	// To store parent array which in turn store MST
	

	// To keep track of vertices included in MST
	vector<bool> inMST(V, false);

	// Insert source itself in priority queue and initialize
	// its key as 0.
	pq.push(make_pair(0, src));
	key[src] = 0;

	/* Looping till priority queue becomes empty */
	while (!pq.empty())
	{
		// The first vertex in pair is the minimum key
		// vertex, extract it from priority queue.
		// vertex label is stored in second of pair (it
		// has to be done this way to keep the vertices
		// sorted key (key must be first item
		// in pair)
		int u = pq.top().second;
		pq.pop();

		inMST[u] = true; // Include vertex in MST

		// 'i' is used to get all adjacent vertices of a vertex
		list< pair<long long, int> >::iterator i;
		for (i = adj[u].begin(); i != adj[u].end(); ++i)
		{
			// Get vertex label and weight of current adjacent
			// of u.
			int v = (*i).first;
			int weight = (*i).second;

			// If v is not in MST and weight of (u,v) is smaller
			// than current key of v
			if (inMST[v] == false && key[v] >(long long) weight+key[u])
			{
				// Updating key of v
				key[v] = (long long)weight+key[u];
				pq.push(make_pair(key[v], v));
				
			}
		}
	}

	// Print edges of MST using parent array
	for (int i = 0; i < V; ++i)
		printf("%lld ",key[i]);
		printf("\n");
}

// Driver program to test methods of graph class
int main()
{
	int t;
	scanf("%d",&t);
	
	while(t-->0)
	{
	    
	int n,k,x,m,s,a,b,c;
	scanf("%d %d %d %d %d ",&n,&k,&x,&m,&s);
	
	Graph g(n);
	
	for(int i=0;i<k-1;i++)
	for(int j=i+1;j<k;j++)
	g.addEdge(i,j,x);
	
	for(int r=0;r<m;r++)
	{
	    scanf("%d %d %d",&a,&b,&c);
	    g.addEdge(a-1,b-1,c);
	}
	g.primMST(s-1);
	
	}
	    
	    return 0;
}
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
