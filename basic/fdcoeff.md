## FINITE DIFFERENCE APPROXIMATIONS

**Author:** Claire Romney

**Language:** C++

**Description/Purpose:** This function will compute the finite difference approximation of an arbitrary order of accuracy for a given derivative.

**Input:**

  int k = Derivative you are approximating
  double xbar = The exact solution
  vector<double> x = the stencil points you are approximating at.
	
**Output:** The function will output the coefficients for the approximations.

**Usage/Example:**

  fdcoeff(int k, double xbar, vector<double> x)
  k = 2
  xbar = 3
  x = {2, 2.5, 3, 3.5, 4}

Output from the lines above:

	{-4, 8, 7.10543e-15, -8, 4}
    
**Implementation/Code:** The following is the code for fdcoeff()

  Matrix fdcoeff(int k, double xbar, vector<double> x) {
	  int n = x.size();
	  Matrix A(n, n, 1);

	  Matrix xrow(n, 1, 0);
	  for (int i = 0; i < n; i++) {
	  	xrow.setVecUnit(i, 0, (x[i] - xbar));
	  }

	  int factorial = 1;
	  for (int i = 1; i < n; i++) {
		  factorial *= i;
		  for (int j = 0; j < n; j++) {
			  A.setVecUnit(i, j, (pow(xrow.getVecUnit(j, 0), i)) / factorial);
		  }
	  }

	  Matrix b(n, 1, 0);
	  b.setVecUnit(k + 1, 0, 1);

	  Matrix c = lufactorization(A, b);
	  return c;
  }

**Link to Matrix Class:** 
  [Matrix](../append/matrix.md)
**Link to lufactorization:**
  [lufactorization()](../append/lufactorization.md)
