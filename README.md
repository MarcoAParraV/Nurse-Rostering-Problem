# Nurse-Rostering-Problem
Comparative study of penalty-based and repair-based evolutionary algorithms for the Nurse Rostering Problem using the official GPost benchmark.

# Evolutionary Algorithms for the Nurse Rostering Problem

This repository contains a Jupyter notebook that implements and compares two evolutionary algorithms for the Nurse Rostering Problem using the official **GPost** benchmark.

Both algorithms use the same representation, initialization, fitness function, selection, crossover, mutation, elitism, population size, and evaluation budget. They differ only in their constraint-handling strategy:

- Penalty-based constraint handling
- Repair-based constraint handling

## Approach

This notebook uses a **direct representation**.

Each roster is represented directly as an employee-by-day matrix:

X in {Off, Day, Night}^(8 x 28)

Rows represent employees, columns represent days, and each cell indicates whether the employee is off, assigned to a day shift, or assigned to a night shift.

The GPost instance has:

- 8 employees
- 28 days
- 3 required day-shift employees per day
- 1 required night-shift employee per day

Because the roster is represented directly as a matrix, each solution corresponds directly to a schedule.

## Constraint Handling

The notebook compares two evolutionary algorithms that differ only in how they handle constraints.

### Penalty EA

The Penalty EA allows infeasible rosters to remain in the population. Hard-constraint violations are penalized using a large penalty weight.

The fitness function is:

f(X) = 1,000,000 * hard violations + soft penalty

Since the problem is treated as a minimization problem, lower fitness is better.

### Repair EA

The Repair EA applies a repair operator after crossover and mutation. The repair function attempts to restore feasibility by:

- restoring exact daily coverage;
- reducing violations related to consecutive worked weekends.

After repair, the roster is evaluated with the same penalized fitness function used by the Penalty EA.

## Hard and Soft Constraints

Hard constraints determine whether a roster is feasible. In this benchmark, hard constraints include:

- exactly 3 day shifts and 1 night shift per day;
- at most one shift per employee per day;
- no employee may work more than two consecutive weekends.

Soft constraints determine the quality of a feasible roster. Violating them is allowed, but each violation adds a weighted penalty to the objective.

Soft constraints include:

- maximum total shifts;
- maximum night shifts;
- requested shifts;
- weekly workload ranges;
- complete weekends;
- undesirable work/off patterns;
- undesirable night-shift patterns.

## Features

- Implements two evolutionary algorithms for the Nurse Rostering Problem.
- Uses a direct employee-by-day matrix representation.
- Compares penalty-based and repair-based constraint handling.
- Uses binary tournament selection.
- Uses one-point crossover on the flattened roster matrix.
- Uses random-reset mutation.
- Includes elitism to preserve the best solution found.
- Implements the official GPost soft-penalty function.
- Validates the evaluator against the published GPost reference solution with objective value 5.
- Reports penalized fitness, hard violations, soft penalty, feasibility rate, and runtime.
- Includes convergence plots and constraint-handling comparisons.
- Displays the best roster found.

## Benchmark

The experiment uses the official GPost benchmark instance for the Nurse Rostering Problem.

Source:

https://www.schedulingbenchmarks.org/nrp/

The notebook also checks the published reference solution to confirm that the local evaluator reproduces the known objective value.

## Technologies

- Python
- NumPy
- pandas
- matplotlib
- Jupyter Notebook

## Purpose

This notebook is intended as an educational benchmark of evolutionary algorithms for a constrained scheduling problem. It demonstrates how different constraint-handling strategies, specifically penalty and repair, affect feasibility, solution quality, and computational cost in the Nurse Rostering Problem.
