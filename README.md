# Amazon Web Services HPC Cluster Toolkit

## Software Prerequisities 
- Linux Unbuntu
- Java Virtual Machine
- Apache Maven

## Build the project

## AWS Cluster Toolkit Options

- one
- two

## Create new cluster

## Configure the user
Consider that your cluster name is 'test' the user is 'test'.
- Set the password
```sudo passwd test```
- Login as local user
```sudo login test```

## Test MPI Program
- Create new MPI program
```vim hello.c```
- HelloWorld MPI program
```
#include <mpi.h>
#include <stdio.h>

int main(int argc, char** argv) {
    // Initialize the MPI environment
    MPI_Init(NULL, NULL);

    // Get the number of processes
    int world_size;
    MPI_Comm_size(MPI_COMM_WORLD, &world_size);

    // Get the rank of the process
    int world_rank;
    MPI_Comm_rank(MPI_COMM_WORLD, &world_rank);

    // Get the name of the processor
    char processor_name[MPI_MAX_PROCESSOR_NAME];
    int name_len;
    MPI_Get_processor_name(processor_name, &name_len);

    // Print off a hello world message
    printf("Hello world from processor %s, rank %d"
           " out of %d processors\n",
           processor_name, world_rank, world_size);

    // Finalize the MPI environment.
    MPI_Finalize();
}
```
- Compile the MPI program 
```mpicc hello.c -o hello```
- Copy on all cluster machine the compiled program
```scp hello IP_SLAVE```
- Run the program on the cluster
```mpirun -np 4 --host MASTER,IP_SLAVE1,IP_SLAVE2 hello```
