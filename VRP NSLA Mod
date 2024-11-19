
reset;

param n; /*number of hubs*/
param v; /*number of vehicles */

set N:=1..n; /*set of nodes that the tour must visit*/
set N0:=0..n;/*set of customer nodes plus depot*/

param w{N};
param c{N0,N0}; /* Distance associated with going from i to j */
param Number_of_Vehicles;
var y{N}; /* Variable to keep track of load of vehicle on route up to customer i */
var x{N0,N0} binary; /*1 if customer j is visited after i */
var Y{N0} binary; /*opening a hub at library j*/

minimize cost: sum{i in N0, j in N0} c[i,j]*x[i,j]; /*objective is to minimize total tour cost */


subject to incoming {j in N}: sum{i in N0: i != j} x[i,j] =1; /*Each node has one link coming into it*/
subject to outgoing {i in N}: sum{j in N0: j != i} x[i,j] = 1; /*Each node has one link going out of it */
subject to maximum_number_of_vehicles: sum{j in N} x[0,j] <= v; /*Each node has one link going out of it */
subject to initial_load {i in N}: y[i]>=w[i];
 

data NSLSVRP.dat;

option solver cplex;
solve;
let Number_of_Vehicles := sum{j in N}(x[0,j]);
display y, x, cost, Number_of_Vehicles;
