## MATRIX INFINITY NORM

**Author:** Claire Romney

**Language:** C++

**Description/Purpose:** This function will compute the infinity norm of a matrix

**Input:**

	Matrix A = matrix
	
**Output:** The function will output the infinity norm as a double

**Usage/Example:**

	matrixInfNorm(Matrix A)
  A = { {1, 2, 3}, {8, 4, 7}, {2, 1, 5} }

Output from the lines above:

	19
    
**Implementation/Code:** The following is the code for matrixInfNorm()

    double matrixInfNorm(Matrix A) {
	    double max = 0;
	    for (int i = 0; i < A.getRow(); i++) {
		    double sum = 0;
		    for (int j = 0; j < A.getCol(); j++) {
		    	sum += A.getVecUnit(i, j);
	    	}
		    if (sum > max) {
		    	max = sum;
	    	}
    	}
	    return max;
    }
