## ROW SWAPPER

**Author:** Claire Romney

**Language:** C++

**Description/Purpose:** This function will swap rows to help solve LU Factorization

**Input:**

	Matrix A = Matrix to swap rows
  int i = column to start with
	
**Output:** The function will output the matrix that would multiply with A to get the row swaps

**Usage/Example:**

	rowSwapper(Matrix A, int i)

Output from the lines above:

  No output. Just a sub function for lufactorization()
    
**Implementation/Code:** The following is the code for rowSwapper()

  Matrix rowSwapper(Matrix A, int i) {
	  Matrix L(A.getCol());
	  int max = 0;
	  int maxRow = 0;
	  for (int j = i; j < A.getRow(); j++) {
		  if (abs(A.getVecUnit(j, i)) > max) {
			  max = abs(A.getVecUnit(j, i));
			  maxRow = j;
		  }
	  }
	  if (maxRow != i) {
		  L = (A.swapRow(i, maxRow)) * L;
	  }
	  return L;
  }

