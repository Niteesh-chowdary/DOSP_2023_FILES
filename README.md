# [COP5615] DOSP Project 3

## Team members

- Akash Kumar Kondaparthi (UFID: 70319809)
- Mayur Sai Yaram (UFID: 29880249)
- Niteesh Chowdary Takkellapati (UFID: 69959715)
- Sri Sai Srivatsa Yerrapragada (UFID: 38090923)

## Steps to run the program

1. Move to the project directory
2. Run the following command to build the project: `dotnet build`
3. Run the following command to execute the program: `donet run <numNodes> <topology> <algorithm>`

## Gossip algorithm

The Gossip Algorithm is a method for spreading information across a network of participants (actors) in a distributed system. It mimics the social activity of gossiping, where a piece of information (or rumor) is spread through casual, randomized exchanges between individuals.

In the gossip protocol, our aim is to propagate message(s) across all the nodes in a network. Our gossip implementation has two main components, the counter and the topology. The counter keeps track of all the nodes that have converged.
It also terminates the whole system whenever all the nodes converge. The topology describes the arrangement of all the nodes in the system. In our implementation, whenever a node receives a message for the first time(Initialization), we are starting a scheduler to invoke that actor periodically. At every round, the actor selects a random neighbor and spreads the message until either the whole system is converged or when a particular node is terminated.
We have set up the convergence and termination condition as following:

- Convergence condition: The node is said to converged when it receives the message atleast once. The entire system converges when all the nodes recieve the message at least once.
- Termination condition: Upon convergence, a node keeps transmitting a messgae until it has received that message upto nine times. Keeping an actor alieve after its convergence aids in achieving the convergence of the whole system. Siimultaneously, the termination condition helps in efficiently managing the network overhead caused by the actor space. It is imperative that the more the number of nodes, the more is the overhead on the network.

#### What is working?

All the topologies have successfully converged various number of nodes.
Gossip algorithm supports all the topologies with larger Number of Nodes. But Push Sum take exponentially large time to converge when number of nodes in the network are greater than 1000 nodes.

#### The largest network we managed to deal with for each type of topology is as follows:

| Topology     | Largest network size |
| ------------ | -------------------- |
| Line         | 10000                |
| 2D           | 10000                |
| Imperfect 2D | 10000                |
| 3D           | 10000                |
| Imperfect 3D | 10000                |
| Full         | 10000                |

### GOSSIP ALGORITHM CONVERGENCE GRAPH:

![Time Taken for Convergence vs Number of Nodes ](https://github.com/Niteesh-chowdary/DOSP_2023_FILES/blob/main/GossipGraph.png)

## PushSum algorithm

The Push-Sum Algorithm is a distributed computing technique used for calculating aggregate values (like sum, average) across a network of nodes.

- State Variables: Each actor in the network maintains two quantities, s and w. Initially, s is set to the actor's own value (often its identifier), and w is set to 1.
- Operation: The algorithm operates in rounds. In each round, each actor sends half of its state (s, w) to a randomly selected neighbor and retains the other half.
- Update on Receive: Upon receiving a message (s, w) from another actor, an actor updates its own state by adding the received values to its respective s and w.
- Estimation: The ratio s/w at any actor at any given time provides an estimate of the aggregate value (e.g., sum) across the network.
- Convergence: An actor considers the algorithm to have converged if its s/w ratio changes insignificantly over several consecutive rounds. This threshold is typically a small value like 10^-10. Once convergence is reached, the actor ceases to participate in further computations.

The Push-Sum Algorithm is notable for its ability to provide accurate estimates of global properties (like sum or average) in a distributed network without centralized coordination. It is robust against network changes but requires careful handling of the convergence criteria to avoid premature termination.

#### The largest network we managed to deal with Push Sum for each type of topology is as follows:

| Topology     | Largest network size |
| ------------ | -------------------- |
| Line         | 1100                 |
| 2D           | 1500                 |
| Imperfect 3D | 1500                 |
| Full         | 1500                 |

### PUSH SUM ALGORITHM CONVERGENCE GRAPH:

![Time Taken for Convergence vs Number of Nodes ](https://github.com/Niteesh-chowdary/DOSP_2023_FILES/blob/main/PushsumGraph.png)
