#include <iostream>
#include <vector>

using namespace std;

// Forward declaration for the Node structure
struct Node;

// Function to display available options
void displayOptions()
{
    cout << "Welcome to the E-Z Route Program, please select an option below!" << endl;
    cout << " 1. Explore Routes (Trip Representation)" << endl;
    cout << " 2. Optimize Routes (Shortest Path)" << endl;
    cout << " 3. View Roads (Adjacencies)" << endl;
    cout << " 4. Check Map (Matrix)" << endl;
}

// ExploreRoutes
void displayRoundTrip(Node* ptr, int i);

// Updated printGraph function
void displayConnections(vector<int> adj[], int V, const string& message, bool shortestRoundTrip = false)
{
    for (int v = 1; v < V; ++v)
    {
        cout << "\n" << message << " " << v;
        if (shortestRoundTrip) {
            // Displaying the shortest round trip format
            for (auto x : adj[v])
                cout << " -> " << x;
        } else {
            // Displaying the regular adjacency format
            for (auto x : adj[v])
                cout << " -> " << x;
        }
        printf("\n");
    }
}

// 1 Riverside to 3 Hemet 33
// 1 Riverside to 2 Moreno 16
// 1 Riverside to 4 Perris 24
// 3 Hemet to 4 Perris 30
// 3 Hemet to 2 Moreno 26
// 4 Perris to 2 Moreno 18

// ExploreRoutes OptimizeRoutes
void addEdge(vector<int> adj[], int u, int v)
{
    adj[u].push_back(v);
    adj[v].push_back(u);
}


struct Node {
    int val, cost;
    Node* next;
};

struct Edge {
    int src, dest, weight;
};

// Main workhorse behind code, contains variables and actually creates the "graph"
class Graph
{
    // Function to make Adjacency List
    Node* getAdjListNode(int value, int weight, Node* head)
    {
        Node* newNode = new Node;
        newNode->val = value;
        newNode->cost = weight;
        newNode->next = head;

        return newNode;    
    }

    int N;  // nodes in the graph

public:
    Node **head;

    Graph(Edge edges[], int n, int N)
    {
        head = new Node*[N]();
        this->N = N;

        for (int i = 0; i < N; i++)
            head[i] = nullptr;

        for (unsigned i = 0; i < n; i++)
        {
            int src = edges[i].src;
            int dest = edges[i].dest;
            int weight = edges[i].weight;
            Node* newNode = getAdjListNode(dest, weight, head[src]);

            head[src] = newNode;

            // Makes the graph undirected
            newNode = getAdjListNode(src, weight, head[dest]);
            head[dest] = newNode;
        }
    }

    ~Graph() 
    {
        for (int i = 0; i < N; i++)
            delete[] head[i];

        delete[] head;
    }
};

// ExploreRoutes
void displayRoundTrip(Node* ptr, int i)
{
    cout << "\n Round Trip Exploration " << i;
    while (ptr != nullptr)
    {
        cout << " -> " << ptr->val << " ";
        ptr = ptr->next;
    }
    printf("\n");
}

// OptimizeRoutes
void displayOptimizedPaths(Node* ptr)
{
    while (ptr != nullptr)
    {
        cout << " -> " << ptr->val << " ";
        ptr = ptr->next;
    }
    cout << endl;
}

// CheckMap
void displayCityMap(Node* ptr, int i)
{
    while (ptr != nullptr)
    {
        cout << "(" << i << ", " << ptr->val
            << ", " << ptr->cost << " Miles) ";

        ptr = ptr->next;
    }
    cout << endl;
}

int main()
{
    int choice;

    // Display options initially
    displayOptions();

    cin >> choice;

    if (choice <= 0 || choice >= 5)
    {
        cout << "The option you have chosen does not exist, please select another option 1-4." << endl;
        cin >> choice;
    }

    // ExploreRoutes
    if (choice == 1)
    {
        cout << "Possible Routes: " << endl << "1.Riverside, 2.Moreno, 3.Hemet, 4.Perris" << endl;
        Edge edges[] =
        {
            // pair x, y
            { 1, 2 }, { 1, 3 }, { 1, 4 }, { 3, 4 },
            { 3, 2 }, { 4, 2 }
        };

        // Vertices
        int N = 5;
        int n = sizeof(edges) / sizeof(edges[0]);
        Graph graph(edges, n, N);
        for (int i = 1; i < N; i++)
        {
            cout << i;
          displayRoundTrip(graph.head[i], i);
        }
        cin >> choice;
    }

    // OptimizeRoutes
    if (choice == 2)
    {
        cout << "Locations: " << endl;

        cout << "1.Riverside, 2.Moreno (32 Miles), 3.Hemet (66 Miles), 4.Perris (48 Miles)" << endl;
        int V = 4;
        vector<int> adj[V];
        addEdge(adj, 1, 4);
        addEdge(adj, 1, 3);
        addEdge(adj, 1, 2);

        // Updated function call
        displayConnections(adj, V, "Optimized Connections to Other Cities");

        cin >> choice;
    }

    // View Roads
    if (choice == 3)
    {
        cout << "1.Riverside, 2.Moreno, 3.Hemet, 4.Perris " << endl;
        int V = 5;
        vector<int> adj[V];
        addEdge(adj, 1, 2);
        addEdge(adj, 1, 3);
        addEdge(adj, 1, 4);
        addEdge(adj, 3, 4);
        addEdge(adj, 3, 2);
        addEdge(adj, 4, 2);

        bool isShortestRoundTrip = true;  // Set to false for regular adjacency display

        // Updated function call
        displayConnections(adj, V, "View Roads", isShortestRoundTrip);

        cin >> choice;
    }

    // Check Map
    if (choice == 4)
    {
        cout << "Cities:" << endl << "1.Riverside, 2.Moreno, 3.Hemet, 4.Perris" << endl;
        Edge edges[] =
        {
            // (x, y, w) 1st Vertex, 2nd Vertex, Weight
            { 1, 2, 16 }, { 1, 3, 33 }, { 1, 4, 24 }, { 2, 3, 26 },
            { 3, 4, 30 }, { 4, 2, 18 }
        };

        // Number of vertices
        int N = 5;

        // calculate edges
        int n = sizeof(edges) / sizeof(edges[0]);

        Graph graph(edges, n, N);
        for (int i = 1; i < N; i++)
        {
            // Updated function call
            displayCityMap(graph.head[i], i);
        }
        cin >> choice;
    }

    return 0;
}
