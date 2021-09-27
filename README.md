# Linear-Programming
Hard coded linear program optimization with verbose working. 

## Requirements
All code was written in a Python 3 Jupyter notebook.

Numpy was used for matrix operations although the second cell in Jupyter includes an attempt without numpy mostly as a Proof of Concept (although there are issues with this, see Floating Point Errors)

## Algorithm
Objective of program was to minimize a linear objective function subject to linear constraints.

Simplex algorithm was used where pivot column was chosen based on smallest index. Stalling pivots (no decrease in objective function) are used in this algorithm, with the requirement that the pivot column index must be smaller than the previous column. This prevents cycling and also ensures that when searching for initial BFS (Basic Feasible Solution), the final tableau (which corresponds to the initial BFS for the primal problem) for the artificial problem pivots away from columns of artificial variables. Tableau format used is further explained in https://en.wikipedia.org/wiki/Simplex_algorithm

## Usage
For tableaus in canonical form with an intial BFS, create a `list_of_vars` which should be a list of the column numbers of variables BFS is on and then run `solve_canon(tableau,list_of_vars,1)`.

For general tableaus without BFS, run `solve_general(tableau)`

If using the first cell in the notebook (i.e. code that uses numpy), tableaus should be `np.array(tableau)`. There are some examples of tests in the cells that I ran to troubleshoot. 

## Floating point errors
There were issues with floating point inaccuracies leading to cells which were theoretically 0 but ended up with very small numbers. This caused a problem when checking if a cell was 0. My fix for this issue was to round cells which have small numbers (absolute value<10^-4) to 0. This may cause inaccuracies based on your linear program and this value should be adjusted via the `rdzero()` function at the beginning of the code. This issue was *not* addressed in the second cell.
