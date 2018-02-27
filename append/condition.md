## CONDITION NUMBER

**Author:** Claire Romney

**Language:** C++

**Description/Purpose:** This function will calculate the condition number of a matrix.

**Input:** 
        
        int n = size of matrix

**Output:** The function will output a double condition number

**Usage/Example:**

        condition(int n)
        n = 3
 
Output from the lines above:

        5.82835
  
**Implementation/Code:** The following is the code for condition()

    double condition(int n) {
	    Matrix A(n, n, 0);
	    for (int i = 0; i < n - 1; i++) {
		    A.setVecUnit(i, i, -2);
		    A.setVecUnit(i, i + 1, 1);
		    A.setVecUnit(i + 1, i, 1);
	    }
	    A.setVecUnit(n - 1, n - 1, -2);
	    double min = inverseIteration(A);
	    double max = powerIteration(A);
    	return (abs(max) / abs(min));
    }

* Inverse Power Method: [inverseIteration()](inversemethod.md)
* Power Method: [powerIteration()](powermethod.md)
