# sudoku-solver
a C++ program, which solves any solvable sudoku puzzle and prints solution to the terminal.
It can handle unsolvable sudokus as well.
<p align="center">
 <img src="https://github.com/coconut41/sudoku-solver/blob/main/solved_sudoku.png" alt="solved_sudoku_image" width="205" height="210" />
</p>

## how the algorithm works
1) The input board is saved as columns and blocks (3x3 sub-boxes of the grid), and the solve_sudoku method is called.
2) In the solve_sudoku function, it iterates through all rows in the grid and identifies empty cells and missing numbers for each row.
3) For each missing number, it checks if it is not present in its block and column. If only one empty cell satisfies this condition, it safely inserts the number into that cell.
4) If multiple empty cells are valid for a missing number, it saves the number and its row if it has the smallest number of possible insertions among all numbers checked so far.
5) After checking all rows, if at least one number was inserted into the grid, it rechecks all rows. If no number was inserted and there are still empty cells, it needs to make a guess.
6) If a guess is required, it iterates through all possible insertions for the "best number to guess," saves it to the grid, and recursively calls solve_sudoku. If the guess leads to an unsuccessful solution (grid can't be solved), it backtracks and removes the wrongly guessed number from the grid.
7) Once the algorithm finishes iterating and guessing in the solve_sudoku method, it checks if all blocks in the grid have exactly nine elements. If this condition is true, it considers the puzzle solved.

## usage
go to line 177 and set board =  your sudoku board you wish to be solved. Compile and run.<br>
 - Compilation: g++ -g src/sudoku_solve.cpp -o solved
 - execute: ./solved on linux. If on windows then just double click file called 'solved' <br>
 
your grid should meet this format:<br> Grid is a 2d vector containing 9 subvectors with numbers from '1'-'9' (stored as characters). '.'(dot) indicates an empty cell. Example: { {'.','.','.','8','.','.','.','.','9'},{'.','8','7','3','.','.','.','4','.'},{'6','.','.','7','.','.','.','.','.'},{'.','.','8','5','.','.','9','7','.'},{'.','.','.','.','.','.','.','.','.'},{'.','4','3','.','.','7','5','.','.'},{'.','.','.','.','.','3','.','.','.'},{'.','3','.','.','.','1','4','5','.'},{'4','.','.','.','.','2','.','.','1'} }; <br>

for program tests uncoment line 2 (#include"../tests/tests.cpp") and line 175 (test::complete_test(board, blocks, columns);)
