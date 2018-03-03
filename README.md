# NetworkOptimization-IntegerLinearProgramming-CPLEX

In a public transportation network, stations are nodes connected by links such as bus lines or rail facilities. Passengers are routing within the network to reach their destinations. With known Origin-Destination (OD) flows, in the optimal situation, we assume all passengers take the shortest path from origin to destination so that the total passenger distance is minimum. 

The aim of this work is to identify the best network flow distribution based on shortest paths to minimize total passenger distance at status quo; further, if a transfer station is removed from the network due to special events or major maintenance, we need to identify how passengers will reroute within the network and which links and nodes will expect flow increase. 

To solve this network optimization problem, I build a mathematical model named Shortest Path Network (SPN) model, and solve it using linear programming in CPLEX. The study case is the Washington Metropolitan Area Transit Authority (WMATA) metro network with 91 stations, with station-to-station passenger flow in October 2015. The distance matrix is obtained as well. All shortest paths and flow distributions are simultaneously solved to optimality within 12 seconds using CPLEX 12 on an Intel i-7 processor paired with 16 GB of RAM. 

Refer to the file named "Figure_of_Result_WMATA.png", when transfer station #4 is removed from the network, its directly connected station #35 hosts 35,866 more passengers than usual, some nearby indirectly connected stations #3 #7 #17 host 5,300 to 47,405 more passengers, even a faraway station #2 experiences 32 more passengers although the increase is minor compared to others.

The CPLEX input of the real-world WMATA metro network is too large to show in the limit space. Therefore, I use the "Small_Sample_Network.png" with 5 nodes and 3 rail lines to demonstrate my methodology. In the small sample network, for simplicity, all distance among directly connected node pairs is set to be 1, and I assign one passenger to travel between each OD pair. Please refer to the file named "CPLEX_code.lp" for CPLEX inputs.
(Please refer to "Steps_to_implement_optimization_in_CPLEX" if you don't know how to implement the optimization in CPLEX.)

The file named "CPLEX_output.txt" shows the optimization results. Illustrated below is how to interpret the results:



Objective = 3.4000000000e+001

(It means the total network cost is 34 passenger-miles.)



X_01_04_01_03                 1.000000

X_01_04_03_04                 1.000000

(It means the shortest path from node #1 to node #4 is #1-#3-#4.)



ARCFLOW01_03                  3.000000

(It means the arc #1-#3 transports 3 passengers.)



C_NODEFLOW_03                24.000000

(It means node #3 hosts 24 passengers.)




