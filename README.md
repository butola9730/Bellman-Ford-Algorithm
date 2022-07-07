# Bellman-Ford-Algorithm
#include<iostream>
#include<stdio.h>
using namespace std;
#include<conio.h>
#define INFINITY 999
struct node
{
    int cost;
    int value;
    int from;
}a[5];
void addEdge(int am[][5],int src,int dest,int cost)
{
     am[src][dest] = cost;
     return;
}
void bel(int am[][5])
{
    int i, j, k, c = 0, temp;
    a[0].cost = 0;
    a[0].from = 0;
    a[0].value = 0;
    for (i = 1; i < 5; i++)
    {
        a[i].from = 0;
        a[i].cost = INFINITY;
        a[i].value = 0;
    }
    while (c < 5)
    {
        int min = 999;
        for (i = 0; i < 5; i++)
        {
            if (min > a[i].cost && a[i].value == 0)
            {
                min = a[i].cost;
            }
            else
            {
                continue;
            }
        }
        for (i = 0; i < 5; i++)
        {
            if (min == a[i].cost && a[i].value == 0)
            {
                break;
            }
            else
            {
                continue;
            }
        }
        temp = i;
        for (k = 0; k < 5; k++)
        {
            if (am[temp][k] + a[temp].cost < a[k].cost)
            {
                a[k].cost = am[temp][k] + a[temp].cost;
                a[k].from = temp;
            }
            else
            {
                continue;
            }
        }
        a[temp].value = 1;
        c++;
    }
    cout<<"Cost"<<"\t"<<"Source Node"<<endl; 
    for (j = 0; j < 5; j++)
    {
        cout<<a[j].cost<<"\t"<<a[j].from<<endl;
    }
}
int main()
{
    int n, am[5][5], c = 0, i, j, cost;
    for (int i = 0; i < 5; i++)
    {
        for (int j = 0; j < 5; j++)
        {
            am[i][j] = INFINITY;
        }
    }
    while (c < 8)
    {
        cout<<"Enter the source, destination and cost of edge\n";
        cin>>i>>j>>cost;
        addEdge(am, i, j, cost);
        c++;
    }
    bell(am);
    getch();
}

#by python

class Graph:



    def __init__(self, vertices):

        self.M = vertices   # Total number of vertices in the graph

        self.graph = []     # Array of edges



    # Add edges

    def add_edge(self, a, b, c):

        self.graph.append([a, b, c])



    # Print the solution

    def print_solution(self, distance):

        print("Vertex Distance from Source")

        for k in range(self.M):

            print("{0}\t\t{1}".format(k, distance[k]))



    def bellman_ford(self, src):



        distance = [float("Inf")] * self.M

        distance[src] = 0



        for _ in range(self.M - 1):

            for a, b, c in self.graph:

                if distance[a] != float("Inf") and distance[a] + c < distance[b]:

                    distance[b] = distance[a] + c



        for a, b, c in self.graph:

            if distance[a] != float("Inf") and distance[a] + c < distance[b]:

                print("Graph contains negative weight cycle")

                return



        self.print_solution(distance)



g = Graph(5)

g.add_edge(0, 1, 2)

g.add_edge(0, 2, 4)

g.add_edge(1, 3, 2)

g.add_edge(2, 4, 3)

g.add_edge(2, 3, 4)

g.add_edge(4, 3, -5)



g.bellman_ford(0)
