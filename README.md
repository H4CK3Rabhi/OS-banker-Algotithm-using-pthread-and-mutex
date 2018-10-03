# OS-banker-Algotithm-using-pthread-and-mutex

Implimentation of banker's algorithm. OS project .


The banker’s algorithm is a resource allocation and deadlock avoidance algorithm that tests for safety by simulating the allocation for predetermined maximum possible amounts of all resources, then makes an “s-state” check to test for possible activities, before deciding whether allocation should be allowed to continue. Following Data structures are used to implement the Banker’s Algorithm: Let ‘n’ be the number of processes in the system and ‘m’ be the number of resources types.

# Available
It is a 1-d array of size ‘m’ indicating the number of available resources of each type. 	Available[ j ] = k means there are ‘k’ instances of resource type Rj

# Max
It is a 2-d array of size ‘n*m’ that defines the maximum demand of each process in a system. 	Max[ i, j ] = k means process Pi may request at most ‘k’ instances of resource type Rj.

#Allocation 
It is a 2-d array of size ‘n*m’ that defines the number of resources of each type currently allocated to each process. 	Allocation[ i, j ] = k means process Pi is currently allocated ‘k’ instances of resource type Rj

# Need
It is a 2-d array of size ‘n*m’ that indicates the remaining resource need of each process. 	Need [ i, j ] = k means process Pi currently allocated ‘k’ instances of resource type Rj 	Need [ i, j ] = Max [ i, j ] – Allocation [ i, j ]

Allocationi specifies the resources currently allocated to process Pi and Needi specifies the additional resources that process Pi may still request to complete its task. Banker’s algorithm consist of Safety algorithm and Resource request algorithm Resource Request Algorithm This describes the behavior of the system when a process makes a resource request in the form of a request matrix. The steps are:

If number of requested instances of each resource is less than the need (which was declared previously by the process), go to step 2.
If number of requested instances of each resource type is less than the available resources of each type, go to step 3. If not, the process has to wait because sufficient resources are not available yet.
Now, assume that the resources have been allocated. Accordingly do, Available = Available - Requesti Allocation(i) = Allocation(i) + Request(i) Need(i) = Need(i) - Request(i)
This step is done because the system needs to assume that resources have been allocated. So there will be less resources available after allocation. The number of allocated instances will increase. The need of the resources by the process will reduce. That's what is represented by the above three operations. After completing the above three steps, check if the system is in safe state by applying the safety algorithm. If it is in safe state, proceed to allocate the requested resources. Else, the process has to wait longer.

# Safety Algorithm

Let Work and Finish be vectors of length m and n, respectively. Initially,
Work = Available
Finish[i] =false for i = 0, 1, ... , n - 1. This means, initially, no process has finished and the number of available resources is represented by the Available array.
Find an index i such that both
Finish[i] ==false
Needi <= Work If there is no such i present, then proceed to step 4. It means, we need to find an unfinished process whose need can be satisfied by the available resources. If no such process exists, just go to step 4.
Perform the following:
Work = Work + Allocation;
Finish[i] = true; Go to step 2. When an unfinished process is found, then the resources are allocated and the process is marked finished. And then, the loop is repeated to check the same for all other processes. If Finish[i] == true for all i, then the system is in a safe state. That means if all processes are finished, then the system is in safe state
