## Problem Statement
Use a Genetic Algorithm(GA) to solve the Travelling Salesman Problem (TSP). **Parallelize** the algorithm using **OpenMP**.

## The Travelling Salesman Problem
Given a set of cities, and the distance between each pair of connected cities, the problem is to find the shortest possible route which a salesman can traverse, visiting each city exactly once, and finally returning to the starting city.

## Genetic Algorithm
Genetic Algorithm (GA) is a search-based optimization technique based on the principles of Genetic and Natural Selection, used to solve both constrained and unconstrained problems. Initially we have a collection of possible solutions (population), which undergo mutations and crossovers in subsequent iteration to produce a better fitness value. Fitness values are values assigned at each step to an individual of the population (chromosome), based on the optimization function value that the individual represents. As in natural genetics, the fitter individuals are more likely to mate and produce a fitter individual, thereby improving the fitness function with each iteration (generation). The algorithm is stopped when we reach a stopping criteria. For problems such as the Travelling Salesman, which are considered NP-Hard in nature, the Genetic Algorithm is an efficient tool, and provides a good-enough near-optimal solution (or a set of such solutions), although it doesn’t guarantee the optimal solution.

## Serial Algorithm
The genetic algorithm randomly initialises an initial solution to each member of the population. During each generation, we first select 50% of our best population (with the best fitness value), perform crossover among them to produce the rest 50% of the population. Then we randomly select 20% members from the population, and perform mutation. Finally, we sort the obtained population on the basis of their fitness value, and this goes on to become our next generation.

## Parallel Algorithm
The Genetic Algorithm code for the travelling salesman problem is written in C++, which supports OpenMP (unlike Python). Therefore, the code has been parallelized using OpenMP. At various for loops during one iteration, we can use pragma omp to parallelise the logic. Although we cant parallelise the overall algorithm, since each generation needs the output of the previous generation we can parallelise the various functions inside one generation. The default NUM_THRDS is set to 2.

## Complexity
Genetic Algorithms are stochastic in nature. The complexity depends on the genetic operators, their implementation (which may have a very significant effect on overall complexity), the representation of the individuals and the population, and obviously on the fitness function. Given the usual choices (point mutation, one point crossover, and roulette wheel selection) a Genetic Algorithms complexity is O(g(nm + nm + n)) with g the number of generations, n is the population size and m the size of the individuals. Therefore, the complexity is of the order of O(gnm). This assumes that the fitness function is itself not time consuming, which depends on the application.

## Input Format
The code, both serial and parallel, requires an input file, the first line of which contains the number of vertices in the graph, followed by the several lines, each containing the vertex number, and its coordinates. The name of this input file must be entered as a command line argument while executing the program. Three input files have been added for test purpose.

- Ex. 	DIMENSION\
    3					            ---Three vertices\
    1 55.38 61.93					---Vertex 1 coordinates \
    2 33.20 44.03					---Vertex 2 coordinates \
    3 13.49 41.29					---Vertex 3 coordinates 

## Compilation
```
gcc ga_tsp_serial.c -o gatsp -lm				---For Serial Code
gcc ga_tsp_parallel.c -o gatsp -fopenmp -lm		---For Parallel Code
```

## Execution
```
./gatsp inputfilename.txt					---For both Files
```

## Output Format
Since the number of vertices are large, printing the fitness value at each stage with fill the terminal entirely, and therefore that code has been commented out. The code currently outputs the final population, the solution, and the best path. It also outputs the time taken by the code for execution.
 
## Test Cases
The execution time has been noted for various values of n (number of vertices), g (number of generations), and population size p. The parallel execution time are for 2, 4, and 6 threads respectively.


-   Population: 100\
    Number of iterations: 1000\
    input: 734 cities\
    serial: 53.844 seconds\
    parallel: 2 threads - 28.32 seconds\
    parallel: 4 threads - 16.84 seconds\
    parallel: 6 threads - 17.67 seconds\

-   Population: 100\
    Number of iterations: 2000\
    input: 734 cities\
    serial: 107.13 seconds\
    parallel: 2 threads - 57.90 seconds\
    parallel: 4 threads - 34.12 seconds\
    parallel: 6 threads - 36.55 seconds\

-   Population: 200\
    Number of iterations: 1000\
    input: 734 cities\
    serial: 99.12 seconds\
    parallel: 2 threads - 58.12 seconds\
    parallel: 4 threads - 37.22 seconds\
    parallel: 6 threads - 39.98 seconds