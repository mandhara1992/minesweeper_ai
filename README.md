# minesweeper_ai
A minesweeper AI with an accuracy of 80% for easy mode, written in Java
To represent the board, I have used the 2-dimensional arrays which will contain the value of the number of neighboring mines and -1 if the cell itself is a mine. Whenever the computer queries the user, it will get a value which will be stored in that cell of the board. Then it will compare the value with the neighboring cells. If by comparing it finds that the neighboring cells are clear, i.e. they don’t have mines, it will enter those into the clearNodes list. If it finds that these cells have mines, it will enter those nodes into the mineNodes list. The last case will be when the computer is unsure about those cells given the information at that point. It will enter those cells into the unsureNodes list. Initially, the program starts with the top left corner of the board and then will expand the nodes accordingly. The interactive version of the game is Command Line based. 
Whenever we uncover a cell, we also get the value stored in it which is the clue for that cell’s neighbors. The computer queries user for a cell through its coordinates and the user has to enter the value of that cell i.e. the number of cells adjacent to it which have mines. The AI adds this information to its knowledge base and then infers from it and correctly guesses (most of the times) the next cell to be uncovered.   
The two most obvious rules for the solution to minesweeper are: 
1. If the value of a cell is equal to the sum of unexplored neighbours and neighbours that are mines, all those unexplored neighbors will contain mines and the knowledge base will be updated accordingly. Those neighbours will be removed from the unsureNodes list so that we don’t explore it again.  
2. If the value of a cell is equal to the number of its neighbors which have mines, all the other neighbors are clear i.e. don’t contain mines and are safe to explore.  3. Whenever there are no cases left for above 2 rules, we check whether a cell has unsure neighbors which are subsets of some other cell’s neighbors. If that happens, we subtract the equations and are left with some additional information that can get us the values of some unsure cells. 
The computer will uncover most of the cells using rules 1 and 2. It will enter the cells into the clearNodes list and mineNodes list accordingly. The next node to be uncovered will be done using Queue concept.
For a fairly easy board, it will uncover most of the cells using the above 2 rules. As the number of mines increase, the solver based only on the above 2 rules will struggle and will have to go for the third case as shown next.  
Whenever there are no more cells in the clearNodes list, it will try to apply Rule 3. It will form a list for a clue node whose neighbors are unsure nodes and then check if those neighbors are subsets of any other clue node. The solver will check if there are any subsets of neighbors of a cell in neighbors of another cell. 
For example,
1 A 
1 B 
D C 
Neighbors of (1,0) - Neighbors of (0,0) = Clue at (1,0) – Clue at (0,0) (A, B, C, D) – (A, B) = 1-1  (C, D) = 0
The condition for surety is as follows: a. If the RHS of the equation is 0, all the variables remaining are clear cells. In this case C and D are clear cells. b. If the value at RHS is equal to the number of variables in the LHS of the equation, all the variables have mines.  Whenever it encounters a case in which the above two conditions fail, the equation is added to the knowledge base. The rule 3 is then applied to the updated knowledge base.

Performance-
Level                                  Win percentage 
Easy (10x10 - 9 mines)                    ~82% 
Intermediate (16x16 - 40 mines)           ~22% 
Hard (16x30 - 99 mines)                Unable to win but uncovering ~60% of total number of mines. 
 
 
