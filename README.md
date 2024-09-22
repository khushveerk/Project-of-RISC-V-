# Project-of-RISC-V-
# Write a code for multiplication of two matrices using RISC V instructions:- 

# Matrix dimensions
M = 2  # number of rows in matrix A
N = 3  # number of columns in matrix A and number of rows in matrix B
P = 4  # number of columns in matrix B

# Matrix A
A:
    .word 1 2 3 4 5 6

# Matrix B
B:
    .word 7 8 9 10 11 12 13 14 15 16 17 18

# Result matrix C
C:
    .space 8 * M * P

# Multiply matrices A and B
main:
    li t0, M  # load number of rows in matrix A
    li t1, N  # load number of columns in matrix A and number of rows in matrix B
    li t2, P  # load number of columns in matrix B

#Initialize loop counters
  li t3, 0  # i = 0
  li t4, 0  # j = 0
  li t5, 0  # k = 0

loop_i:
    # Initialize sum for current element of C
    li t6, 0

loop_j:
    # Load elements from A and B
    lw t7, A(t3)  # load A[i, k]
    lw t8, B(t4)  # load B[k, j]

 #Multiply elements and add to sum
  mul t9, t7, t8
  add t6, t6, t9

  #Increment k and check if we've reached the end of the row
   addi t5, t5, 1
   blt t5, t1, loop_j

  Store result in C
    sw t6, C(t3, t4)

   Increment j and check if we've reached the end of the column
    addi t4, t4, 1
    blt t4, t2, loop_i

   Increment i and check if we've reached the end of the matrix
    addi t3, t3, 1
    blt t3, t0, loop_i

  #Exit program
  li a0, 0
  jr ra 


  This code assumes that the matrices are stored in memory as arrays of words, with each element of the matrix stored in a separate word. The matrices are multiplied using three nested loops, with the innermost loop performing the dot product of a row of matrix A and a column of matrix B.
    
