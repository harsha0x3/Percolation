# Percolation

Estimate the percolation threshold via Monte Carlo simulation, using an efficient union–find data structure.

## Overview

This project simulates a percolation system modeled on an *n-by-n* grid to estimate the percolation threshold—the critical probability at which a system percolates. The problem is solved using Monte Carlo simulation and the **WeightedQuickUnionUF** data structure from the Princeton Algorithms library.

This project was completed as part of the [Princeton Algorithms I course](https://coursera.org/learn/algorithms-part1) by Kevin Wayne and Robert Sedgewick.

---

## Contents

* `Percolation.java`: Implements the percolation system using the Weighted Quick Union algorithm with path compression.
* `PercolationStats.java`: Performs multiple Monte Carlo simulations and computes the mean, standard deviation, and 95% confidence interval of the percolation threshold.
* `README.md`: Project documentation.

---

## Requirements

* Java 8 or later
* `algs4.jar` (Princeton Standard Libraries)

To compile and run with the custom Princeton Java environment:

```bash
javac-algs4 Percolation.java PercolationStats.java
java-algs4 PercolationStats n T
```

Where:

* `n` is the grid size (e.g., 200)
* `T` is the number of Monte Carlo experiments (e.g., 100)

---

## Example Usage

```bash
$ java-algs4 PercolationStats 200 100
mean                    = 0.5928
stddev                  = 0.0091
95% confidence interval = [0.5905, 0.5951]
```

---

## Project Details

### Percolation.java

* **Grid model**: Sites are either **open** or **blocked**.
* **Percolates**: System percolates if a connected path of open sites exists from top to bottom.
* **Union–Find**: Uses WeightedQuickUnionUF for connectivity checking.

### API

```java
public class Percolation {
    public Percolation(int n)              // create n-by-n grid, with all sites blocked
    public void open(int row, int col)     // open the site at (row, col)
    public boolean isOpen(int row, int col)// check if the site is open
    public boolean isFull(int row, int col)// check if the site is full (connected to top)
    public int numberOfOpenSites()         // get total number of open sites
    public boolean percolates()            // check if the system percolates
}
```

---

### PercolationStats.java

* Runs `T` independent simulations on an `n-by-n` grid.
* Tracks fraction of open sites when percolation occurs.
* Computes mean, standard deviation, and 95% confidence interval.

### API

```java
public class PercolationStats {
    public PercolationStats(int n, int trials) // perform trials
    public double mean()                       // sample mean
    public double stddev()                     // sample standard deviation
    public double confidenceLo()               // low endpoint of 95% confidence interval
    public double confidenceHi()               // high endpoint of 95% confidence interval
}
```

---

## Development Notes

* Corner case validation: constructor and method arguments are validated against invalid input (e.g., out-of-bounds indices, non-positive dimensions).
* Performance: Designed with amortized constant-time union–find operations.

