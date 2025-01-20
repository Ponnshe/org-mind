
# Table of Contents

1.  [Objective](#org889bb13)
2.  [Fleeting](#org739ff55)
    1.  [Python](#orgb725879)
        1.  [Planning](#org1a0f4ec)
        2.  [Implementation](#orga1a29c1)



<a id="org889bb13"></a>

# Objective

Write a function named printTable() that takes a list of lists of strings and
displays it in a well-organized table with each column right-justified.
Assume that all the inner lists will contain the same number of strings.
For example, the value could look like this:
tableData = [['apples', 'oranges', 'cherries', 'banana'],
             ['Alice', 'Bob', 'Carol', 'David'],
             ['dogs', 'cats', 'moose', 'goose']]
Your printTable() function would print the following:
   apples Alice  dogs
  oranges   Bob  cats
 cherries Carol moose
   banana David goose


<a id="org739ff55"></a>

# Fleeting


<a id="orgb725879"></a>

## Python


<a id="org1a0f4ec"></a>

### Planning

I will have to parse the lists twice. The first iteration is to get the lenght of the largest string in the sub-lists in order to use that value to justify. I will create a list with the lenght of the main list. Then I will extract for each sub-list the greater value of the length of each component of the sublist. For example:

*given col<sub>widths</sub> the list of the greatest values of each sublist*

the `col_width[0]` will save the greatest value of the first sub-list, `col_width[1]` the second sub-list and so on.

After that I will have to iterate the lists like this: first element of the first list, first element of the second list, etc. (this computational inefficient, but I can't see other way) to print the table.

-   [X] Get the greatest lenght of each sublist
-   [X] Print the table xd
    
    So this could be a code:

    def print_table(table_data):
        col_width = [0] * len(table_data)
        num_columns = len(table_data)
        num_rows = len(table_data[0]) #This works because I assume all lists contain the same number of strings
        for col in range(num_columns):
            for row in range(num_rows):
                if len(table_data[col][row]) > col_width[col]:
                    col_width[col] = len(table_data[col][row])
    
        for row in range(num_rows):
            for col in range(num_columns):
                print(table_data[col][row].rjust(col_width[col]), end="| ")
            print("\n")


<a id="orga1a29c1"></a>

### Implementation

The planning code was good, it mets the requirements, but it is not good enough, so I justa add some formatting to the table.
\#+begin<sub>src</sub> python
def print<sub>table</sub>(table<sub>data</sub>):
    col<sub>width</sub> = [0] \* len(table<sub>data</sub>)
    num<sub>columns</sub> = len(table<sub>data</sub>)
    num<sub>rows</sub> = len(table<sub>data</sub>[0]) #This works because I assume all lists contain the same number of strings
    for col in range(num<sub>columns</sub>):
        for row in range(num<sub>rows</sub>):
            if len(table<sub>data</sub>[col][row]) > col<sub>width</sub>[col]:
                col<sub>width</sub>[col] = len(table<sub>data</sub>[col][row])

total<sub>justify</sub> = 0
for i in col<sub>width</sub>:
    total<sub>justify</sub> += i

    print ("".rjust(total<sub>justify</sub>+3\*num<sub>columns</sub>+1, "-"))
    for row in range(num<sub>rows</sub>):
        print("| ", end="")
        for col in range(num<sub>columns</sub>):
            print(table<sub>data</sub>[col][row].rjust(col<sub>width</sub>[col]), end=" | ")
        print("")
        print ("".rjust(total<sub>justify</sub>+3\*num<sub>columns</sub>+1, "-"))
\#+end<sub>src</sub>>

