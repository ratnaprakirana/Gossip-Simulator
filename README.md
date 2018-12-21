# Gossip-Simulator
Gossip type algorithms can be used both for group communication and for aggregate computation.Implemented randomized gossip algorithm for information exchange in distributed network in Elixir. Push sum was implemented in similar fashion. Analysis was done on 6 topologies .
Topologies

Gossip and Push-sum simulator
Instructions
Expected Input

    Number of nodes Non-negative integer
    Topology It must belong to the following list:

    line
    full
    rand2D
    3D
    impLine
    Torus
    Algorithm
    gossip
    push-sum

Sample
Input

For input n = 1200, topology = Imperfect Line and algorithm= Push sum

Elixir lib/topologies.ex 1200  imperfect_line push-sum
Explanation
Gossip Algorithm

A random first node is picked by the main process to initiate the Gossip algorithm. We make a list of all adjacent nodes to this initial node and pick a new random node amongst these and transmit the message. A node stops transmitting the message once it has heard the rumor more than 10 times. If a node receives a message after the 10th time, a new random node is picked from the list of all nodes and the propagation continues. We perform this process continuously for all nodes until convergence is achieved.

Convergence is achieved when all nodes in the topology have received the message at least once.
Push Sum Algorithm

A random node is picked by the main process for push sum algorithm. Initially, state and weight are defined as s = xi = i (that is actor number i has value i, play with other distribution if you so desire) and w = 1. While sending the message half of the s and w are sent to another node, which are the added to their current s and w. A node stops transmitting the message once the ratio (s/w) do not change more than 10^(-10) in 3 consecutive rounds. In this case, a random node is chosen again from the list of all nodes and Push-Sum algorithm is continued.

Convergence is achieved when all nodes in the topology receives the message at least once.
Building Topologies
Full Network: Every actor is a neighbor of all other actors. That is, every actor can talk directly to any other actor.
3D Grid: Actors form a 3D grid. The actors can only talk to the grid neighbors.
Random 2D Grid: Actors are randomly position at x,y coordinates on a [0-1.0]X[0-1.0] square. Two actors are connected if they are within 1 distance to other actors. 
Torus: Actors are arranged in a sphere. That is, each actor has 4 neighbors (similar to the 2D grid) but both directions are closed to form circles.
Line: Actors are arranged in a line. Each actor has only 2 neighbors (one left and one right, unless you are the first or last actor).
Imperfect Line: Line arrangement but one random other neighbor is selected from the list of all actors.
