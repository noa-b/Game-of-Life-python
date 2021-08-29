# Conway-s-Game-of-Life.py
the graphic is pretty much absent
import numpy as np
import random

def count_neighbors(y, x, cells): 
  (rows, columns) = cells.shape
  living_neighbors  = 0
  for i in range (y - 1, y + 2):
    for j in range (x - 1, x + 2):
      if x == j and y == i:
        continue
      else:
         if i < rows and  j < columns and i >= 0 and j >= 0:
            # i and j are in the bounderies of cells.
          living_neighbors += cells[i, j]

  return living_neighbors   


def life_calculator(is_alive, living_neighbors): #is_alive --> boolean type, living_neighbors --> integer
  if is_alive and 3 < living_neighbors <= 1:
    return 0
  elif not is_alive and living_neighbors == 3:
    return 1
  else:
    if is_alive:
      return 1
    else:
      return 0  
  
   
def generation(cells):
  (rows, columns) = cells.shape
  for i in range(0, rows):
    for j in range(0, columns):
      cells[i, j] = life_calculator(cells[i, j] == 1, count_neighbors(i, j, cells))
        

#main
rows, columns = (10, 10) 
cells = np.zeros((rows, columns)) 
ones_initial = rows*columns // 3

#-------------------------------------------
# 0 in the cells array means the cell is dead and 1 is alive.
#generation 0. initializing randomly 1 and 0 for each cell
i = 0
while i < ones_initial:
  random_num_row = random.randint(0, rows - 1)
  aran_num_column = random.randint(0, columns - 1)
  
  if cells[random_num_row, aran_num_column] == 0:
    cells[random_num_row, aran_num_column] = 1
    i += 1
#-------------------------------------------------
num_of_gens = int(input("how many generation would you like to be processed? "))
for i in range(0, num_of_gens):
  generation(cells)

print(cells)
