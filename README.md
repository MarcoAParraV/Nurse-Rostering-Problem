# Nurse-Rostering-Problem
Comparative study of penalty-based and repair-based evolutionary algorithms for the Nurse Rostering Problem using the official GPost benchmark.

# Evolutionary Algorithms for the Nurse Rostering Problem

This repository contains a Jupyter notebook that implements and compares two evolutionary algorithms for the Nurse Rostering Problem using the official GPost benchmark instance.

The notebook studies two constraint-handling strategies under the same experimental setup:

- **Penalty EA:** infeasible rosters remain in the population and receive a large hard-constraint penalty.
- **Repair EA:** offspring are repaired before evaluation, then scored with the same penalized fitness function.

Both algorithms use the same solution representation, initialization method, fitness function, selection, crossover, mutation, elitism, population size, and evaluation budget. This makes the comparison focused specifically on the effect of constraint handling.

## Problem

The Nurse Rostering Problem assigns employees to shifts over a planning horizon while satisfying hard constraints and minimizing weighted soft-constraint violations. In the GPost instance, the roster includes 8 employees over 28 days, with daily coverage requirements for day and night shifts.

## Features

- Parses and evaluates the official GPost benchmark.
- Validates the evaluator against the published reference solution with objective value 5.
- Implements a shared evolutionary algorithm framework.
- Compares penalty-based and repair-based constraint handling.
- Reports fitness, hard violations, soft penalty, feasibility rate, and runtime.
- Includes convergence and comparison plots.
- Displays the best roster found by the repair-based method.

## Technologies

- Python
- NumPy
- pandas
- matplotlib
- Jupyter Notebook

## Purpose

This notebook is intended as an educational and experimental implementation of evolutionary optimization for nurse scheduling. It highlights how constraint-handling choices can affect feasibility, solution quality, and computational cost in a benchmark scheduling problem.
