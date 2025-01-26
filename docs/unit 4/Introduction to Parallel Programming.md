# Introduction to Parallel Programming

Parallel algorithm Design

- Identify portions that can be run concurrently

- Map concurrent pieces of work onto multiple processes

- Distribute data

- Manage access to shared data

- Synchronize at various stages

## Preliminaries

### Decomposition, Tasks and Dependency Graphs

**decomposition**: dividing a computation into smaller parts

**task**: main computation is divided into tasks. Regarded as indivisible

#### Dense matrix-vector multiplication

![](images/2025-01-26-11-35-52-image.png)

- In this case all tasks are independent

- But if they're dependent, we make: **task-dependency graph**

- It's a Directed Acyclic Graph which decides the relative order of execution

#### Database query processing

![](images/2025-01-26-11-39-59-image.png)

![](images/2025-01-26-11-40-26-image.png)

### Granularity, Concurrency, and Task-Interaction

**granularity**: size of the decomposed tasks

**fine-grained**: large number of small tasks

**coarse-grained**: small number of large tasks

**degree of concurrency**: Maximum number of tasks that can be executed simultaneously at any time. Eg: For the database example it's 4

**average degree of concurrency**: average number of tasks that can run concurrently over the entire execution

![](images/2025-01-26-11-50-57-image.png)

average degree of concurrency of:

- a: 2.33 (63/27)

- b: 1.88 (64/34)

Usually, as granularity increases, degree of concurrency increases

**critical path**: A feature of dependency graph that determines the average degree of concurrency

**critical path length**: sum of weights of nodes along the critical path, where weight is the amount of work associated with it

In the above graphs:

- a: 27

- b: 34

shorter critical path means higher concurrency

**task interaction**

**task-interaction graph**: shows interaction between tasks

#### Sparse matrix-vector multiplication

A sparse matrix x a dense vector

We make ith task the "owner" of A[i, \*] and b[i]

But others also need b[i], so this task is responsible for sending it to the others

### Processes and Mapping

**process**: abstract entity that executes a task

**mapping**: assigning tasks to processes

Good mapping:

- Independent tasks on different processes

- Execute tasks on the crititical path as soon as possible

- Minimise interactions

### Processes vs Processors

Process: abstraction

Processor: hardware

## Decomposition Techniques

### Recursive Decomposition

- Used for divide and conquer

- Eg: quick sort

#### Finding minimum in an array

**Serial algorithm**:

![](images/2025-01-26-12-13-34-image.png)

**Recursive algorithm**:

![](images/2025-01-26-12-15-38-image.png)

![](images/2025-01-26-12-15-48-image.png)

### Data Decomposition

Two step process:

- Partition the data

- Use the data partition to induce a partition of computation

**Partitioning output data**: Often each element of output an be calculated independently

#### Matrix Multiplication

![](images/2025-01-26-12-20-51-image.png)

#### Computing frequencies of itemsets in a transaction database

![](images/2025-01-26-13-22-35-image.png)

**Partitioning input**: Eg: sorting, finding max/min or sum of an array etc

![](images/2025-01-26-14-56-49-image.png)

**Partitioning both Input and Output data**

**Partitioning Intermediate data**

### Exploratory Decomposition

- Partition the search space into smaller parts and search each part concurrently

#### The 15 puzzle problem

![](images/2025-01-26-15-05-44-image.png)

- First few levels of configurations are generated serially until the search tree has sufficient number of leaf nodes.

- Now each node is assigned to a task to explore further until atleast one of them find a solution

- It's different from data decomposition because in data decomposition every process does work that is needed in the output. 

- In exploratory decomposition, when one process finds a solution, all others can be terminated.

### Speculative Decomposition

- Similar to branch prediction

- But does wasteful work

- A slightly less wasteful approach: Only most promising branch is taken up in parallel with the condition

#### Parallel Discrete Event Simulation

![](images/2025-01-26-15-14-26-image.png)

- At first glance it appears totally sequential

- But later components can assume an input and start evaluation

- When input becomes available, part of, or all the work required would've already been completed

- Different from exploratory in this way: In exploratory, even a serial algorithm would eventually do all the work that a parallel algorithm does

- In speculative: A parallel algorithm does extra work that a serial algorithm wouldn't do because the serial algorithm would know the correct input

### Hybrid Decompositions

![](images/2025-01-26-15-35-40-image.png)

## Characteristics of Tasks and Interactions

### Characteristics of Tasks

**1. Task Generation**:

- Static

- Dynamic

**2. Task size**

- Uniform

- Non uniform

- Knowledge of task size

- Size of data

### Characteristics of Inter-Task Interactions

**1. Static vs Dynamic** (can be known beforehand or not)

**2. Regular vs Irregular** (spatial structure)

**3. Read only vs Read write**

**4. One-way vs Two-way** (explicitly supplied or not)


